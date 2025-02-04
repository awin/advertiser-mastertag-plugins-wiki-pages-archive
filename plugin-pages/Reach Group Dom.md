# Integration requirements

Please be aware plugin should be only utilized upon request of the
partner, when they require to load additional third party scripts.
This plugin is rendered in the inline mode, meaning it has full DOM and
cookie access.

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

The Reach Group plugin has different tags depending on the type of page
visited.

Plugin supports following `PAGETYPE`: category, product, basket,
checkout, generic

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `ReachGroupDom_ADVERTISER_ID` with its real value.

Replace `ReachGroupDom_CAMPAIGN_ID` with its real value.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.


``` javascript
AWIN.Tracking.ReachGroupDom = AWIN.Tracking.ReachGroupDom || {};
AWIN.Tracking.ReachGroupDom.advertiserId = "ReachGroupDom_ADVERTISER_ID";
AWIN.Tracking.ReachGroupDom.campaignId = "ReachGroupDom_CAMPAIGN_ID";
AWIN.Tracking.ReachGroupDom.pagetype = "PAGETYPE_IDENTIFIER";
```





``` javascript
AWIN.Tracking.ReachGroupDom = AWIN.Tracking.ReachGroupDom || {};
AWIN.Tracking.ReachGroupDom.advertiserId = "1234";
AWIN.Tracking.ReachGroupDom.campaignId = "5678";
AWIN.Tracking.ReachGroupDom.pagetype = "generic";
```



(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

## Product Page

The plugin does not use the product scraper itself but you could use it
to fetch the ID if you prefer and supply it to the identifier config
variable.


``` javascript
AWIN.Tracking.ReachGroupDom.identifier = "ID_OF_THE_PRODUCT";
AWIN.Tracking.ReachGroupDom.category = "NAME_OF_CATEGORY";
```



Example:


``` javascript
AWIN.Tracking.ReachGroupDom.identifier = google_tag_params.ecomm_prodid;
AWIN.Tracking.ReachGroupDom.category = google_tag_params.ecomm_prod_category;
```




## Category Page


``` javascript
AWIN.Tracking.ReachGroupDom.category = "NAME_OF_CATEGORY";
```



Example:


``` javascript
AWIN.Tracking.ReachGroupDom.category = google_tag_params.ecomm_category;
```




## Basket Page

Plugin requires product data (productIds and quantities) on the basket
page. Data can be supplied to the plugin with array of products
(zx_products) or with the PLT form.

Example:


``` javascript
var zx_products = [];
for (var i = 0; i < dataLayer[1].ecommerce.basketProducts; i++) {
    var o = {};
    o.identifier = dataLayer[1].ecommerce.basketProducts[i].sku_code;
    o.quantity = dataLayer[1].ecommerce.basketProducts[i].quantity;
    zx_products.push(o);
}
```




## Checkout Page

Plugin requires product data (productIds and quantities) on the checkout
page. If client has Product Level Tracking Implemented on the checkout
page, data will be retrieved automatically. If PLT is not implemented,
data can be supplied to the plugin with array of products (zx_products).

Plugin automatically assigns the pagetype and retrieves the data if
<b>AWIN.Tracking.Sale</b> is present therefore it is not necessary to
add this part in configuration.

Example:


``` javascript
var zx_products = [];
for (var i = 0; i < dataLayer[1].ecommerce.transactionProducts; i++) {
    var o = {};
    o.identifier = dataLayer[1].ecommerce.transactionProducts[i].sku_code;
    o.quantity = dataLayer[1].ecommerce.transactionProducts[i].quantity;
    zx_products.push(o);
}
```




# Example Complete Setup

Example below is written on the basis that there is no PLT implemented
on the checkout page. Product data array is different on the basket and
the checkout page therefore if statement for AWIN.Tracking.Sale has been
added.


``` javascript
AWIN.Tracking.ReachGroupDom = AWIN.Tracking.ReachGroupDom || {};
AWIN.Tracking.ReachGroupDom.advertiserId = "8876";
AWIN.Tracking.ReachGroupDom.campaignId = "1767";
AWIN.Tracking.ReachGroupDom.pagetype = "generic";
var zx_products = [];

if (AWIN.Tracking.Sale) {
    for (var i = 0; i < dataLayer[1].ecommerce.transactionProducts; i++) {
        var o = {};
        o.identifier = dataLayer[1].ecommerce.transactionProducts[i].sku_code;
        o.quantity = dataLayer[1].ecommerce.transactionProducts[i].quantity;
        zx_products.push(o);
    }
} else if (google_tag_params.ecomm_pagetype == "cart") {
    AWIN.Tracking.ReachGroupDom.pagetype = "basket";
    for (var i = 0; i < dataLayer[1].ecommerce.basketProducts; i++) {
        var o = {};
        o.identifier = dataLayer[1].ecommerce.basketProducts[i].sku_code;
        o.quantity = dataLayer[1].ecommerce.basketProducts[i].quantity;
        zx_products.push(o);
    }
} else if (google_tag_params.ecomm_pagetype == "product") {
    AWIN.Tracking.ReachGroupDom.pagetype = "product";
    AWIN.Tracking.ReachGroupDom.identifier = google_tag_params.ecomm_prodid;
    AWIN.Tracking.ReachGroupDom.category = google_tag_params.ecomm_prod_category;
} else if (google_tag_params.ecomm_pagetype == "category") {
    AWIN.Tracking.ReachGroupDom.pagetype = "category";
    AWIN.Tracking.ReachGroupDom.category = google_tag_params.ecomm_category;
}
```


# Plugin Code

``` javascript
AWIN.Tracking.ReachGroupDom = AWIN.Tracking.ReachGroupDom || {};
AWIN.Tracking.ReachGroupDom.url = AWIN.Tracking.ReachGroupDom.url || AWIN.sProtocol + "hal9000.redintelligence.net/retarget";

(function ($r) {
    if ("undefined" === typeof $r.advertiserId || "undefined" === typeof $r.campaignId) {
        return;
    }

    var pagetype = $r.pagetype || AWIN.Tracking.fetchZxParam('pagetype');

    if (AWIN.Tracking.Sale) {
        pagetype = "checkout";
    } else  if ("checkout" === pagetype.toLowerCase()) {
        AWIN.Tracking.Sale = {};
    }

    $r.combineProducts = function(products) {
        if (typeof products === "string") {
            products = JSON.parse(products);
        }

        var output = "";
        var sep = "";

        for (var i = 0; i < products.length; i++) {
            output += sep + products[i].identifier + "|" + products[i].quantity;
            sep = ",";
        }

        return output;
    };

    $r.fetchBasketData = function() {
        var products = AWIN.Tracking.getBasketData();
        for (var i = 0; i < products.length; i++) {
            products[i].identifier = products[i].id;
            delete products[i].id;
        }
        return products;
    };

    var url = $r.url + "?a=" + $r.advertiserId + "&version=1";

    switch (pagetype.toLowerCase()) {
        case "basket" :
            url += "&" + AWIN.Tracking.buildQueryString({
                event: 'basket',
                cat: $r.campaignId,
                items: $r.combineProducts(AWIN.Tracking.fetchZxParam('products') || $r.fetchBasketData()),
                segment: $r.category || AWIN.Tracking.fetchZxParam('category') || ''
            });
            break;
        case "category" :
            url += "&" + AWIN.Tracking.buildQueryString({
                segment: $r.category || AWIN.Tracking.fetchZxParam('category')
            });
            break;
        case "checkout" :
            url += "&" + AWIN.Tracking.buildQueryString({
                event: 'transaction',
                cat: $r.campaignId,
                items: $r.combineProducts(AWIN.Tracking.fetchZxParam('products') || $r.fetchBasketData()),
                segment: $r.category || AWIN.Tracking.fetchZxParam('category') || ''
            });
            break;
        case "search" :
            url += "&" + AWIN.Tracking.buildQueryString({
                segment: "suchergebnisse"
            });
            break;
        case "product" :
            url += "&" + AWIN.Tracking.buildQueryString({
                event: 'view',
                cat: $r.campaignId,
                segment: $r.category || AWIN.Tracking.fetchZxParam('category'),
                items: $r.identifier || AWIN.Tracking.fetchZxParam('identifier')
            });
            break;
        case "registration":
            return;
        case "generic" :
        case "home" :
            break;
        default:
            return;
    }

    AWIN.Tracking.frameAppend(url);
})(AWIN.Tracking.ReachGroupDom);
```

