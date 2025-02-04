# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

Targeting360 plugin has different tags depending on the type of page
visited.

Plugin supports following `PAGETYPE`: category, product, basket,
checkout, home, login (to detag users)

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | Targeting360      |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `Targeting360_ADVERTISER_ID` with its real value.

Replace `Targeting360_FEED_ID` with its real value.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.


``` javascript
AWIN.Tracking.Targeting360 = AWIN.Tracking.Targeting360 || {};
AWIN.Tracking.Targeting360.advertiserId = "Targeting360_ADVERTISER_ID";
AWIN.Tracking.Targeting360.feedId = "Targeting360_FEED_ID";
AWIN.Tracking.Targeting360.pagetype = "PAGETYPE_IDENTIFIER";
```





``` javascript
AWIN.Tracking.Targeting360 = AWIN.Tracking.Targeting360 || {};
AWIN.Tracking.Targeting360.advertiserId = "1234";
AWIN.Tracking.Targeting360.feedId = "5678";
```



(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

## Product Page

The plugin does not use the product scraper itself but you could use it
to fetch the ID if you prefer and supply it to the identifier config
variable.


``` javascript
AWIN.Tracking.Targeting360.identifier = "ID_OF_THE_PRODUCT";
```



Example:


``` javascript
AWIN.Tracking.Targeting360.identifier = google_tag_params.ecomm_prodid;
```




## Category Page


``` javascript
AWIN.Tracking.Targeting360.category = "NAME_OF_CATEGORY";
```



Example:


``` javascript
AWIN.Tracking.Targeting360.category = google_tag_params.ecomm_category;
```




## Basket Page

Plugin requires product data (productIds and quantities) on the basket
page. Data can be supplied to the plugin with array of products
(zx_products) or with the PLT form.

Example:


``` javascript
var zx_products = [];
for (var i = 0; i < google_tag_manager["GTM-MFSNPS"].dataLayer.get("view_cart").items.length; i++) {
var t360tempProdArr = {};
t360tempProdArr.identifier = google_tag_manager["GTM-MFSNPS"].dataLayer.get("view_cart").items[i].item_id;
t360tempProdArr.quantity = google_tag_manager["GTM-MFSNPS"].dataLayer.get("view_cart").items[i].quantity;
zx_products.push(t360tempProdArr);
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

if (AWIN.Tracking.Sale) {
    for (var i = 0; i < google_tag_manager["GTM-MFSNPS"].dataLayer.get("ecommerce").transactionProducts.length; i++) {
        var t360tempProdArr = {};
        t360tempProdArr.identifier = google_tag_manager["GTM-MFSNPS"].dataLayer.get("ecommerce").transactionProducts[i].sku_code;
        t360tempProdArr.quantity = google_tag_manager["GTM-MFSNPS"].dataLayer.get("ecommerce").transactionProducts[i].quantity;
        zx_products.push(t360tempProdArr);
    }
}
```




## Login Page

Example:


``` javascript
if (document.location.href.match(/login/i)) {
    AWIN.Tracking.Targeting360.pagetype = "login";
}
```




# Example Complete Setup

Example below is written on the basis that there is no PLT implemented
on the checkout page. Product data array is different on the basket and
the checkout page therefore if statement for <b>AWIN.Tracking.Sale</b>
has been added.


``` javascript
AWIN.Tracking.Targeting360 = AWIN.Tracking.Targeting360 || {};
AWIN.Tracking.Targeting360.advertiserId = "4876";
AWIN.Tracking.Targeting360.feedId = "3237";

var zx_products = [];

if (AWIN.Tracking.Sale) {
    AWIN.Tracking.Targeting360.pagetype = "checkout";
    for (var i = 0; i < google_tag_manager["GTM-MFSNPS"].dataLayer.get("ecommerce").transactionProducts.length; i++) {
        var t360tempProdArr = {};
        t360tempProdArr.identifier = google_tag_manager["GTM-MFSNPS"].dataLayer.get("ecommerce").transactionProducts[i].sku_code;
        t360tempProdArr.quantity = google_tag_manager["GTM-MFSNPS"].dataLayer.get("ecommerce").transactionProducts[i].quantity;
        zx_products.push(t360tempProdArr);
    }
}
else if (google_tag_params.ecomm_pagetype == "cart") {
    AWIN.Tracking.Targeting360.pagetype = "basket";
    for (var i = 0; i < google_tag_manager["GTM-MFSNPS"].dataLayer.get("view_cart").items.length; i++) {
      var t360tempProdArr = {};
      t360tempProdArr.identifier = google_tag_manager["GTM-MFSNPS"].dataLayer.get("view_cart").items[i].item_id;
      t360tempProdArr.quantity = google_tag_manager["GTM-MFSNPS"].dataLayer.get("view_cart").items[i].quantity;
      zx_products.push(t360tempProdArr);
    }
} else if (google_tag_params.ecomm_pagetype == "product") {
    AWIN.Tracking.Targeting360.pagetype = "product";
    AWIN.Tracking.Targeting360.identifier = google_tag_params.ecomm_prodid;
} else if (google_tag_params.ecomm_pagetype == "category") {
    AWIN.Tracking.Targeting360.pagetype = "category";
    AWIN.Tracking.Targeting360.category = google_tag_params.ecomm_category;
} else if (google_tag_params.ecomm_pagetype == "home") {
    AWIN.Tracking.Targeting360.pagetype = "home";
} else if (document.location.href.match(/login/i)) {
    AWIN.Tracking.Targeting360.pagetype = "login";
}
```


# Plugin Code


``` javascript

AWIN.Tracking.Targeting360 = AWIN.Tracking.Targeting360 || {};
AWIN.Tracking.Targeting360.url = AWIN.Tracking.Targeting360.url || AWIN.sProtocol + "ad.ad-srv.net/retarget?version=1";

(function ($t) {
    var pagetype = $t.pagetype || AWIN.Tracking.fetchZxParam('pagetype');

    if ("undefined" === typeof pagetype) {
        return;
    }

    if (AWIN.Tracking.Sale) {
        pagetype = "checkout";
    } else if ("checkout" === pagetype.toLowerCase()) {
        AWIN.Tracking.Sale = {};
    }

    $t.combineProducts = function(products) {
        if (typeof products === "string") {
            products = JSON.parse(products);
        }
        var identifiers = "";
        var sep = "";

        for (var i = 0; i < products.length; i++) {
            identifiers += sep + products[i].identifier + "|" + products[i].quantity;
            sep = ",";
        }

        return identifiers;
    };

    $t.fetchBasketData = function() {
        var products = AWIN.Tracking.getBasketData();
        for (var i = 0; i < products.length; i++) {
            products[i].identifier = products[i].id;
            delete products[i].id;
        }
        return products;
    };

    var feedId = $t.feedId || AWIN.Tracking.fetchZxParam('feedId');
    var advertiserId = $t.advertiserId || AWIN.Tracking.fetchZxParam('advertiserId');
    var url = $t.url + "&cat=" + feedId + "&a=" + advertiserId;

    var gdpr = $t.gdpr || AWIN.Tracking.fetchZxParam('gdpr');
    var gdpr_consent = $t.gdpr_consent || AWIN.Tracking.fetchZxParam('gdpr_consent');

    switch (pagetype.toLowerCase()) {
        case "checkout" :
            var products = $t.combineProducts(AWIN.Tracking.fetchZxParam('products') || $t.fetchBasketData());
            url += "&event=transaction&items=" + products;
            break;
        case "category" :
            var category = $t.category || AWIN.Tracking.fetchZxParam('category');
            url += "&event=view&items=&segment=" + category;
            break;
        case "product" :
            var productId = $t.identifier || AWIN.Tracking.fetchZxParam('identifier');
            url += "&event=view&items=" + productId;
            break;
        case "basket" :
            var products = $t.combineProducts(AWIN.Tracking.fetchZxParam('products') || $t.fetchBasketData());
            url += "&event=basket&items=" + products;
            break;
        case "login" :
            url += "&demark=1";
            break;
        case "home" :
            break;
        default:
            return;
    }

    if (typeof gdpr !== "undefined") {
        if (gdpr !== null) {
            url += "&gdpr=" + gdpr;
        }
    }

    if (typeof gdpr_consent !== "undefined") {
        if (gdpr_consent !== null) {
            url += "&gdpr_consent=" + gdpr_consent;
        }

    }

    AWIN.Tracking.frameAppend(url);
})(AWIN.Tracking.Targeting360);
```

