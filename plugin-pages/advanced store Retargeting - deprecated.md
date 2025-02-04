# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

The ad4mat plugin has different tags depending on the type of page
visited.

Plugin supports following `PAGETYPE`: home, product, checkout, basket,
category, search, generic

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | ad4mat            |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `SPECIFIC_ad4mat_ADVERTISER_ID` with its real value.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.


``` javascript
AWIN.Tracking.ad4mat = AWIN.Tracking.ad4mat || {};
AWIN.Tracking.ad4mat.adspaceId = "SPECIFIC_AD4MAT_ADVERTISER_ID";
AWIN.Tracking.ad4mat.url = "SPECIFIC_AD4MAT_COUNTRY_URL";
AWIN.Tracking.ad4mat.pagetype = "PAGETYPE_IDENTIFIER";
```





``` javascript
AWIN.Tracking.ad4mat = AWIN.Tracking.ad4mat || {};
AWIN.Tracking.ad4mat.adspaceId = "9161";
AWIN.Tracking.ad4mat.url = "www.ad4mat.de";
AWIN.Tracking.ad4mat.pagetype = "generic";
```



(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

## Product Page

The plugin does not use the product scraper itself but you could use it
to fetch the ID if you prefer and supply it to the identifier config
variable.


``` javascript
AWIN.Tracking.ad4mat.identifier = "ID_OF_THE_PRODUCT";
AWIN.Tracking.ad4mat.category = "NAME_OF_CATEGORY";
```



Example:


``` javascript
AWIN.Tracking.ad4mat.identifier = google_tag_params.prodid[0];
AWIN.Tracking.ad4mat.category = google_tag_params.prodCategory[0];
```




## Category Page


``` javascript
AWIN.Tracking.ad4mat.category = "NAME_OF_CATEGORY";
```



Example:


``` javascript
AWIN.Tracking.ad4mat.category = google_tag_params.category;
```




## Search Results Page


``` javascript
AWIN.Tracking.ad4mat.searchQuery = "USER_SEARCH_TERMS";
```



Example:


``` javascript
AWIN.Tracking.ad4mat.searchQuery = google_tag_params.searchQ;
```




## Basket Page

Plugin requires product data (productIds) on the basket page. Data can
be supplied to the plugin with array of products (zx_products) or with
the PLT form.

Example:


``` javascript
if (dataLayer[2].viewCartItems) {
    var zx_products = [];
    for (var i = 0; i < dataLayer[2].viewCartItems.length; i++) {
        zx_products.push({
        'identifier':dataLayer[2].viewCartItems[i].sku,
        'quantity':dataLayer[2].viewCartItems[i].quantity,
        'amount':dataLayer[2].viewCartItems[i].price});
    }
}
```




## Checkout Page

Plugin requires product data (productIds) on the checkout page. If
client has Product Level Tracking Implemented on the checkout page, data
will be retrieved automatically. If PLT is not implemented, data can be
supplied to the plugin with array of products (zx_products).

Plugin automatically detects pagetype if AWIN.Tracking.Sale is present
on the checkout.

Example:


``` javascript
if (dataLayer[2].viewCheckoutItems) {
    var zx_products = [];
    for (var i = 0; i < dataLayer[2].viewCheckoutItems.length; i++) {
        zx_products.push({
        'identifier':dataLayer[2].viewCheckoutItems[i].sku,
        'quantity':dataLayer[2].viewCheckoutItems[i].quantity,
        'amount':dataLayer[2].viewCheckoutItems[i].price});
    }
}
```




# Example Complete Setup

Example below is written on the basis that there is no PLT implemented
on the checkout page. Product data array is the same on the basket and
the checkout page.


``` javascript
AWIN.Tracking.ad4mat = AWIN.Tracking.ad4mat || {};
AWIN.Tracking.ad4mat.adspaceId = "9161";
AWIN.Tracking.ad4mat.url = "www.ad4mat.de";
AWIN.Tracking.ad4mat.pagetype = "generic";

if (google_tag_params.pagetype == "cart") {
    AWIN.Tracking.ad4mat.pagetype = "basket";
} else if (google_tag_params.pagetype == "product") {
    AWIN.Tracking.ad4mat.pagetype = "product";
    AWIN.Tracking.ad4mat.identifier = google_tag_params.prodid[0];
    AWIN.Tracking.ad4mat.category = google_tag_params.prodCategory[0];
} else if (google_tag_params.pagetype == "category") {
    AWIN.Tracking.ad4mat.pagetype = "category";
    AWIN.Tracking.ad4mat.category = google_tag_params.category;
} else if (google_tag_params.pagetype == "home") {
    AWIN.Tracking.ad4mat.pagetype = "home";
} else if (google_tag_params.pagetype == "searchPage") {
    AWIN.Tracking.ad4mat.pagetype = "search";
    AWIN.Tracking.ad4mat.searchQuery = google_tag_params.searchQ;
}

if (dataLayer[2].viewCartItems) {
    var zx_products = [];
    for (var i = 0; i < dataLayer[2].viewCartItems.length; i++) {
        zx_products.push({
        'identifier':dataLayer[2].viewCartItems[i].sku,
        'quantity':dataLayer[2].viewCartItems[i].quantity,
        'amount':dataLayer[2].viewCartItems[i].price});
    }
}
```


# Plugin Code


``` javascript
AWIN.Tracking.ad4mat = AWIN.Tracking.ad4mat || {};
AWIN.Tracking.ad4mat.url = AWIN.Tracking.ad4mat.url || "www.ad4mat.net";

(function ($a) {
    if ("undefined" === typeof $a.adspaceId) {
        return;
    }

    var pagetype = $a.pagetype || AWIN.Tracking.fetchZxParam('pagetype');

    if (AWIN.Tracking.Sale) {
        pagetype = "checkout";
    } else if ("checkout" === pagetype.toLowerCase()) {
        AWIN.Tracking.Sale = {};
    }

    $a.fetchBasketData = function() {
        var products = AWIN.Tracking.getBasketData();
        for (var i = 0; i < products.length; i++) {
            products[i].identifier = products[i].id;
            delete products[i].id;
        }
        return products;
    };

    $a.combineProducts = function(products) {
        if (typeof products === "string") {
            products = JSON.parse(products);
        }

        var identifiers = "";
        var sep = "";

        for (var i = 0; i < products.length; i++) {
            identifiers += sep + products[i].identifier;
            sep = ",";
        }

        return identifiers;
    };

    var url = AWIN.sProtocol + $a.url;

    if (AWIN.sProtocol === "https://" && $a.url !== "www.ad4mat.de" && $a.url !== "ad4mat.de") {
        url = "https://www.ad4mat.net";
    }

    url += '/ads/js/ck_tracker.php?adspaceId=' + $a.adspaceId + '&mt=1&country=' + $a.url;

    switch (pagetype.toLowerCase()) {
        case "home":
            url += '&sprd=false&catId=home';
            break;
        case "category":
            var category = $a.category || AWIN.Tracking.fetchZxParam('category');
            url += '&sprd=false&catId=' + category;
            break;
        case "product":
            var category = $a.category || AWIN.Tracking.fetchZxParam('category');
            var productId = $a.identifier || AWIN.Tracking.fetchZxParam('identifier');
            url += '&sprd=false&productId=' + productId + '&catId=' + category;
            break;
        case "basket":
            var basket = $a.combineProducts(AWIN.Tracking.fetchZxParam('products') || $a.fetchBasketData());
            url += '&sprd=false&productId=' + basket;
            break;
        case "search":
            var searchName = $a.searchQuery || AWIN.Tracking.fetchZxParam('search_query');
            url += '&sprd=false&searchName=' + searchName;
            break;
        case "checkout":
            var basket = AWIN.Tracking.fetchZxParam('products') || $a.fetchBasketData();
            var revenue = AWIN.Tracking.fetchZxParam('amount') || AWIN.Tracking.Sale.amount;
            var orderId = AWIN.Tracking.fetchZxParam('transaction') || AWIN.Tracking.Sale.orderRef;
            var currency = AWIN.Tracking.fetchZxParam('currency') || AWIN.Tracking.Sale.currency;
            var quantity = 0;

            for (var i in basket) {
                quantity += parseInt(basket[i].quantity || 0, 10);
            }

            url += '&sprd=true&quantity=' + quantity + '&revenue=' + revenue + '&orderId=' + orderId
                + '&currency=' + currency;
            break;
        case "generic":
            url += '&sprd=false';
            break;
    }

    AWIN.Tracking.scriptAppend(url);
})(AWIN.Tracking.ad4mat);
```

