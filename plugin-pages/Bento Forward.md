# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

Bento Forward plugin has different tags depending on the type of page
visited.

Plugin supports following `PAGETYPE`: category, product, basket,
checkout, search other

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | BentoForward      |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `BentoForward_CAMPAIGN_ID` with its real value.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.


``` javascript
AWIN.Tracking.BentoForward = AWIN.Tracking.BentoForward || {};
AWIN.Tracking.BentoForward.campaignId = "BentoForward_CAMPAIGN_ID";
AWIN.Tracking.BentoForward.pageType = "PAGETYPE_IDENTIFIER";
```





``` javascript
AWIN.Tracking.BentoForward = AWIN.Tracking.BentoForward || {};
AWIN.Tracking.BentoForward.campaignId = "1234";
AWIN.Tracking.BentoForward.pageType = "other";
```



(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

## Product Page

The plugin does not use the product scraper itself but you could use it
to fetch the ID if you prefer and supply it to the identifier config
variable.


``` javascript
AWIN.Tracking.BentoForward.productId = "ID_OF_THE_PRODUCT";
```



Example:


``` javascript
AWIN.Tracking.BentoForward.productId = google_tag_params.ecomm_prodid;
```




## Category Page


``` javascript
AWIN.Tracking.BentoForward.categoryId = "ID_OF_CATEGORY";
```



Example:


``` javascript
AWIN.Tracking.BentoForward.categoryId = google_tag_params.ecomm_category;
```




## Basket Page

Plugin requires product data (productIds) on the basket page. Data can
be supplied to the plugin with array of products (zx_products) or with
the PLT form.

Example:


``` javascript
var zx_products = [];
for (var i = 0; i < google_tag_manager["GTM-MFSNPS"].dataLayer.get("view_cart").items.length; i++) {
var o = {};
o.identifier = google_tag_manager["GTM-MFSNPS"].dataLayer.get("view_cart").items[i].item_id;
zx_products.push(o);
}
```




## Checkout Page

Plugin requires product data (productIds) on the checkout page. If
client has Product Level Tracking Implemented on the checkout page, data
will be retrieved automatically. If PLT is not implemented, data can be
supplied to the plugin with array of products (zx_products).

Plugin automatically assigns the pagetype and retrieves the data if
<b>AWIN.Tracking.Sale</b> is present therefore it is not necessary to
add this part in configuration.

Example:


``` javascript
var zx_products = [];
for (var i = 0; i < google_tag_manager["GTM-MFSNPS"].dataLayer.get("view_cart").items.length; i++) {
var o = {};
o.identifier = google_tag_manager["GTM-MFSNPS"].dataLayer.get("view_cart").items[i].item_id;
zx_products.push(o);
}
```




## Search Page

Example:


``` javascript
AWIN.Tracking.BentoForward.searchTerm = "SEARCH_TEARM";
```



Example:


``` javascript
AWIN.Tracking.BentoForward.searchTerm = google_tag_params.searchQuery;
```




# Example Complete Setup

Example below is written on the basis that there is no PLT implemented
on the checkout page. Product data array is different on the basket and
the checkout page therefore if statement for <b>AWIN.Tracking.Sale</b>
has been added.


``` javascript
AWIN.Tracking.BentoForward = AWIN.Tracking.BentoForward || {};
AWIN.Tracking.BentoForward.campaignId = "1234";
AWIN.Tracking.BentoForward.pageType = "other";
var zx_products = [];

if (AWIN.Tracking.Sale) {
    for (var i = 0; i < dataLayer[1].ecommerce.transactionProducts; i++) {
        var o = {};
        o.identifier = dataLayer[1].ecommerce.transactionProducts[i].sku_code;
        zx_products.push(o);
    }
} else if (google_tag_params.ecomm_pagetype == "cart") {
    AWIN.Tracking.BentoForward.pageType = "basket";
    for (var i = 0; i < dataLayer[1].ecommerce.basketProducts; i++) {
        var o = {};
        o.identifier = dataLayer[1].ecommerce.basketProducts[i].sku_code;
        zx_products.push(o);
    }
} else if (google_tag_params.ecomm_pagetype == "product") {
    AWIN.Tracking.BentoForward.pageType = "product";
    AWIN.Tracking.BentoForward.productId = google_tag_params.ecomm_prodid;
} else if (google_tag_params.ecomm_pagetype == "category") {
    AWIN.Tracking.BentoForward.pageType = "category";
    AWIN.Tracking.BentoForward.categoryId = google_tag_params.ecomm_category;
}  else if (document.location.href.match(/search/i)) {
    AWIN.Tracking.BentoForward.pageType = "search";
    AWIN.Tracking.BentoForward.searchTerm = google_tag_params.searchQuery;
}
```


# Plugin Code


``` javascript

AWIN.Tracking.BentoForward = AWIN.Tracking.BentoForward || {};
AWIN.Tracking.BentoForward.url = AWIN.Tracking.BentoForward.url
    || AWIN.sProtocol + "pix.hyj.mobi/rt";

(function ($config) {

    var fetchBasketData = function () {
        var products = AWIN.Tracking.fetchZxParam("products") || AWIN.Tracking.getBasketData();
        if (typeof products === "string") {
            products = JSON.parse(products);
        }
        for (var i = 0; i < products.length; i++) {
            products[i].id = (typeof products[i].identifier !== "undefined") ? products[i].identifier : products[i].id;
            delete products[i].identifier;
        }

        return products;
    };

    var getProductsIdFromBasket = function() {
        return fetchBasketData().map(function (product) {
            return product.id;
        }).join(",");
    };

    var pageType = $config.pageType.toLowerCase();
    var campaignId = $config.campaignId;

    if (AWIN.Tracking.Sale) {
        pageType = "checkout";
    } else if ("checkout" === pageType) {
        AWIN.Tracking.Sale = {};
    }

    if (("undefined" === typeof pageType) || "undefined" === typeof campaignId) {
        return;
    }

    var urlParameters = {t: "d", cid: campaignId};

    switch (pageType) {
        case "search":
            urlParameters.action = "l";
            urlParameters.products = $config.searchTerm || "";
            break;
        case "category":
            urlParameters.action = "c";
            urlParameters.id = $config.categoryId || "";
            break;
        case "product":
            urlParameters.action = "p";
            urlParameters.id = $config.productId || "";
            break;
        case "basket":
            urlParameters.action = "w";
            urlParameters.id = $config.productId || getProductsIdFromBasket() || "";
            break;
        case "checkout":
            urlParameters.action = "t";
            urlParameters.orderId = $config.orderId || AWIN.Tracking.Sale.orderRef || "";
            urlParameters.amount = $config.amount || AWIN.Tracking.Sale.amount || "";
            urlParameters.products = $config.products || getProductsIdFromBasket() || "";
            break;
        default:
            urlParameters.action = "s";
            break;
    }

    var url = $config.url + "?" + AWIN.Tracking.buildQueryString(urlParameters);

    AWIN.Tracking.scriptAppend(url, null, null, {async: "async"});
})(AWIN.Tracking.BentoForward);
```

