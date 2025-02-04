# Description

# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

The Kupona plugin has different tags depending on the type of page
visited.

Plugin supports following `PAGETYPE`: home, category, product, basket,
search, checkout

# Tag example

<https://d31bfnnwekbny6.cloudfront.net/customers/31073.min.js>

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | Kupona            |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `SPECIFIC_KUPONA_TOKEN` with its real value.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.


``` javascript
AWIN.Tracking.Kupona = AWIN.Tracking.Kupona || {};
AWIN.Tracking.Kupona.token = "SPECIFIC_KUPONA_TOKEN";
AWIN.Tracking.Kupona.pagetype = "PAGETYPE_IDENTIFIER";
```





``` javascript
AWIN.Tracking.Kupona = AWIN.Tracking.Kupona || {};
AWIN.Tracking.Kupona.token = "31073";
AWIN.Tracking.Kupona.pagetype = "generic";
```



(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

## Product Page

The plugin does not use the product scraper itself but you could use it
to fetch the ID if you prefer and supply it to the identifier config
variable.


``` javascript
AWIN.Tracking.Kupona.identifier = "ID_OF_THE_PRODUCT";
AWIN.Tracking.Kupona.category = "NAME_OF_CATEGORY";
AWIN.Tracking.Kupona.brand = "BRAND_OF_THE_PRODUCT";
```



Example:


``` javascript
AWIN.Tracking.Kupona.identifier = google_tag_params.prodid[0];
AWIN.Tracking.Kupona.category = google_tag_params.prodCategory[0];
AWIN.Tracking.Kupona.brand = zx_brand;
```



`Travel specific variables`


``` javascript
AWIN.Tracking.Kupona.Travel.startDate = "TRAVEL_START_DATE";
AWIN.Tracking.Kupona.Travel.endDate = "TRAVEL_STOP_DATE"
AWIN.Tracking.Kupona.Travel.destination1 = "TRAVEL_START_DESTINATION";
AWIN.Tracking.Kupona.Travel.destination2 = "TRAVEL_STOP_DESTINATION";
AWIN.Tracking.Kupona.Travel.origin = "TRAVEL_ORIGIN";
```




Example:


``` javascript
AWIN.Tracking.Kupona.Travel.startDate = zx_travel_start_date;
AWIN.Tracking.Kupona.Travel.endDate = zx_travel_stop_date;
AWIN.Tracking.Kupona.Travel.destination1 = zx_travel_start_destination;
AWIN.Tracking.Kupona.Travel.destination2 = zx_travel_stop_destination;
AWIN.Tracking.Kupona.Travel.origin = zx_origin;
```




## Category Page


``` javascript
AWIN.Tracking.Kupona.categoryy = "NAME_OF_CATEGORY";
```



Example:


``` javascript
AWIN.Tracking.Kupona.category = google_tag_params.category;
```



`Travel specific variables`


``` javascript
AWIN.Tracking.Kupona.event = "KUPONA_SPECIFIC_EVENT";
AWIN.Tracking.Kupona.Travel.startDate = "TRAVEL_START_DATE";
AWIN.Tracking.Kupona.Travel.endDate = "TRAVEL_STOP_DATE"
AWIN.Tracking.Kupona.Travel.destination1 = "TRAVEL_START_DESTINATION";
AWIN.Tracking.Kupona.Travel.destination2 = "TRAVEL_STOP_DESTINATION";
```



Example:


``` javascript
AWIN.Tracking.Kupona.event = "205070";
AWIN.Tracking.Kupona.Travel.startDate = zx_travel_start_date;
AWIN.Tracking.Kupona.Travel.endDate = zx_travel_stop_date;
AWIN.Tracking.Kupona.Travel.destination1 = zx_travel_start_destination;
AWIN.Tracking.Kupona.Travel.destination2 = zx_travel_stop_destination;
```




## Search Results Page


``` javascript
AWIN.Tracking.Kupona.category = "USER_SEARCH_TERMS";
```



Example:


``` javascript
AWIN.Tracking.Kupona.category= google_tag_params.searchQ;
```



`Travel specific variables`


``` javascript
AWIN.Tracking.Kupona.event = "KUPONA_SPECIFIC_EVENT";
AWIN.Tracking.Kupona.Travel.startDate = "TRAVEL_START_DATE";
AWIN.Tracking.Kupona.Travel.endDate = "TRAVEL_STOP_DATE"
AWIN.Tracking.Kupona.Travel.destination1 = "TRAVEL_START_DESTINATION";
AWIN.Tracking.Kupona.Travel.destination2 = "TRAVEL_STOP_DESTINATION";
```



Example:


``` javascript
AWIN.Tracking.Kupona.event = "205070";
AWIN.Tracking.Kupona.Travel.startDate = zx_travel_start_date;
AWIN.Tracking.Kupona.Travel.endDate = zx_travel_stop_date;
AWIN.Tracking.Kupona.Travel.destination1 = zx_travel_start_destination;
AWIN.Tracking.Kupona.Travel.destination2 = zx_travel_stop_destination;
```




## Basket Page

Plugin requires product data (productIds) on the basket page. Data can
be supplied to the plugin with array of products (zx_products) or with
the PLT form.

Example:


``` javascript
var zx_products = [];
for (var i = 0; i < google_tag_params.prodid.length; i++) {
    var o = {};
    o.identifier = google_tag_params.prodid[i];
    zx_products.push(o);
}
```




## Checkout Page

Plugin requires product data (productIds and quantitiy) on the checkout
page. If client has Product Level Tracking Implemented on the checkout
page, data will be retrieved automatically. If PLT is not implemented,
data can be supplied to the plugin with array of products (zx_products).

Example:


``` javascript
var zx_products = [];
for (var i = 0; i < google_tag_params.prodid.length; i++) {
    var o = {};
    o.identifier = google_tag_params.prodid[i];
    o.quantity = google_tag_params.quantity[i];
    zx_products.push(o);
}
```




# Example Complete Setup

Example below is written on the basis that there is no PLT implemented
on the checkout page.


``` javascript
AWIN.Tracking.Kupona = AWIN.Tracking.Kupona || {};
AWIN.Tracking.Kupona.token = "31073";
AWIN.Tracking.Kupona.pagetype = "home";

if (document.location.href.match(/cart/i)) {
    AWIN.Tracking.Kupona.pagetype = "basket";
    var zx_products = [];
    for (var i = 0; i < google_tag_params.prodid.length; i++) {
        var o = {};
        o.identifier = google_tag_params.prodid[i];
        zx_products.push(o);
    }
} else if (document.location.href.match(/productdetails\//i)) {
    AWIN.Tracking.Kupona.pagetype = "product";
    AWIN.Tracking.Kupona.identifier = google_tag_params.prodid[0];
} else if (document.location.href.match(/productCategory|catCategory/i)) {
    AWIN.Tracking.Kupona.pagetype = "category";
    AWIN.Tracking.Kupona.category = google_tag_params.category;
} else if (document.location.href.match(/startseite/i)) {
    AWIN.Tracking.Kupona.pagetype = "home";
} else if (AWIN.Tracking.Sale) {
    var zx_products = [];
    for (var i = 0; i < google_tag_params.prodid.length; i++) {
        var o = {};
        o.identifier = google_tag_params.prodid[i];
        o.quantity = google_tag_params.quantity[i];
        zx_products.push(o);
    }
}
```


# Plugin Code

Example below is written on the basis that there is no PLT implemented
on the checkout page.


``` javascript
AWIN.Tracking.Kupona = AWIN.Tracking.Kupona || {};
AWIN.Tracking.Kupona.Travel = AWIN.Tracking.Kupona.Travel || {};
AWIN.Tracking.Kupona.url = AWIN.Tracking.Kupona.url || AWIN.sProtocol + "d31bfnnwekbny6.cloudfront.net/customers/";

(function ($k) {
    if ("undefined" === typeof $k.token) {
        return;
    }

    var pagetype = $k.pagetype || AWIN.Tracking.fetchZxParam('pagetype');

    if (AWIN.Tracking.Sale) {
        pagetype = "checkout";
    } else if ("checkout" === pagetype.toLowerCase()) {
        AWIN.Tracking.Sale = {};
    }

    if ("undefined" === typeof pagetype) {
        return;
    }

    var url = $k.url + $k.token + ".min.js";

    $k.combineProducts = function(products) {
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

    $k.fetchBasketData = function() {
        var products = AWIN.Tracking.getBasketData();
        for (var i = 0; i < products.length; i++) {
            products[i].identifier = products[i].id;
            delete products[i].id;
        }
        return products;
    };

    $k.combineQuantities = function(products) {
        if (typeof products === "string") {
            products = JSON.parse(products);
        }
        var quantities = "";
        var sep = "";

        for (var i = 0; i < products.length; i++) {
            quantities += sep + products[i].quantity;
            sep = ",";
        }

        return quantities;
    };

    switch (pagetype.toLowerCase()) {
        case "checkout" :
            window.kp_order_id = AWIN.Tracking.fetchZxParam('transaction') || AWIN.Tracking.Sale.orderRef;
            window.kp_order_product_ids = $k.combineProducts(AWIN.Tracking.fetchZxParam('products')
                || $k.fetchBasketData());
            window.kp_order_product_quantities = $k.combineQuantities(AWIN.Tracking.fetchZxParam('products')
                || $k.fetchBasketData());
            window.kp_order_total = AWIN.Tracking.fetchZxParam('total_amount') || AWIN.Tracking.Sale.amount;
            break;
        case "category" :
            window.kp_category_id = $k.category || AWIN.Tracking.fetchZxParam('category');
            window.kp_event = $k.event || AWIN.Tracking.fetchZxParam('event') || "";
            window.kp_travel_start_date = $k.Travel.startDate || AWIN.Tracking.fetchZxParam('start_date') || "";
            window.kp_travel_end_date = $k.Travel.endDate || AWIN.Tracking.fetchZxParam('end_date') || "";
            window.kp_travel_destination = $k.Travel.destination1 || AWIN.Tracking.fetchZxParam('destination1') || "";
            window.kp_travel_2_destination = $k.Travel.destination2 || AWIN.Tracking.fetchZxParam('destination2') || "";
            break;
        case "product" :
            window.kp_product_id = $k.identifier || AWIN.Tracking.fetchZxParam('identifier');
            window.kp_product_category_id = $k.category || AWIN.Tracking.fetchZxParam('category');
            window.kp_product_brand = $k.brand || AWIN.Tracking.fetchZxParam('brand');
            window.kp_travel_start_date = $k.Travel.startDate || AWIN.Tracking.fetchZxParam('start_date') || "";
            window.kp_travel_end_date = $k.Travel.endDate || AWIN.Tracking.fetchZxParam('end_date') || "";
            window.kp_travel_destination = $k.Travel.destination1 || AWIN.Tracking.fetchZxParam('destination1') || "";
            window.kp_travel_2_destination = $k.Travel.destination2 || AWIN.Tracking.fetchZxParam('destination2') || "";
            window.kp_travel_origin = $k.Travel.origin || AWIN.Tracking.fetchZxParam('origin') || "";
            break;
        case "basket" :
            window.kp_shoppingcart_product_ids = $k.combineProducts(AWIN.Tracking.fetchZxParam('products')
                || $k.fetchBasketData());
            break;
        case "search" :
            window.kp_site = "search";
            window.kp_category_id = $k.category || AWIN.Tracking.fetchZxParam('category');
            window.kp_event = $k.event || AWIN.Tracking.fetchZxParam('event');
            window.kp_travel_start_date = $k.Travel.startDate || AWIN.Tracking.fetchZxParam('start_date') || "";
            window.kp_travel_end_date = $k.Travel.endDate || AWIN.Tracking.fetchZxParam('end_date') || "";
            window.kp_travel_destination = $k.Travel.destination1 || AWIN.Tracking.fetchZxParam('destination1') || "";
            window.kp_travel_2_destination = $k.Travel.destination2 || AWIN.Tracking.fetchZxParam('destination2') || "";
        case "home" :
            break;
        default:
            return;
    }

    AWIN.Tracking.scriptAppend(url);
})(AWIN.Tracking.Kupona);
```

