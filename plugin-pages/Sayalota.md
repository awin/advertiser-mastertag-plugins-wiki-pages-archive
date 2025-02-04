
# Integration requirements

<img src="Warning.png" title="Warning.png" width="37"
alt="Warning.png" /> NOTE: This plugin is deprecated.

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

Sayalota plugin has different tags depending on the type of page
visited.

Plugin supports following `PAGETYPE`: category, product, basket,
checkout, generic, home, search

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | Sayalota          |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `Sayalota_ADVERTISER_ID` with its real value.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.


``` javascript
AWIN.Tracking.Sayalota = AWIN.Tracking.Sayalota || {};
AWIN.Tracking.Sayalota.advertiserId = "Sayalota_ADVERTISER_ID";
AWIN.Tracking.Sayalota.pagetype = "PAGETYPE_IDENTIFIER";
```





``` javascript
AWIN.Tracking.Sayalota = AWIN.Tracking.Sayalota || {};
AWIN.Tracking.Sayalota.advertiserId = "1234";
AWIN.Tracking.Sayalota.pagetype = "generic";
```



(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

## Product Page

The plugin does not use the product scraper itself but you could use it
to fetch the ID if you prefer and supply it to the identifier config
variable.


``` javascript
AWIN.Tracking.Sayalota.identifier = "ID_OF_THE_PRODUCT";
```



Example:


``` javascript
AWIN.Tracking.Sayalota.identifier = google_tag_params.ecomm_prodid;
```




## Category Page


``` javascript
AWIN.Tracking.Sayalota.category = "NAME_OF_CATEGORY";
```



Example:


``` javascript
AWIN.Tracking.Sayalota.category = google_tag_params.ecomm_category;
```




## Basket Page

Plugin requires product data (productIds) on the basket page. Data can
be supplied to the plugin with array of products (zx_products) or with
the PLT form.

Example:


``` javascript
var zx_products = [];
for (var i = 0; i < dataLayer[1].ecommerce.basketProducts.length; i++) {
    var o = {};
    o.identifier = dataLayer[1].ecommerce.basketProducts[i].sku_code;
    zx_products.push(o);
}
```




## Checkout Page

Plugin automatically assigns the pagetype and retrieves the data if
<b>AWIN.Tracking.Sale</b> is present therefore it is not necessary to
add this part in configuration.

Example:





# Example Complete Setup


``` javascript
AWIN.Tracking.Sayalota = AWIN.Tracking.Sayalota || {};
AWIN.Tracking.Sayalota.advertiserId = "1234";
AWIN.Tracking.Sayalota.pagetype = "generic";
var zx_products = [];

if (google_tag_params.ecomm_pagetype == "cart") {
    AWIN.Tracking.Sayalota.pagetype = "basket";
    for (var i = 0; i < dataLayer[1].ecommerce.basketProducts.length; i++) {
        var o = {};
        o.identifier = dataLayer[1].ecommerce.basketProducts[i].sku_code;
        o.quantity = dataLayer[1].ecommerce.basketProducts[i].quantity;
        zx_products.push(o);
    }
} else if (google_tag_params.ecomm_pagetype == "product") {
    AWIN.Tracking.Sayalota.pagetype = "product";
    AWIN.Tracking.Sayalota.identifier = google_tag_params.ecomm_prodid;
} else if (google_tag_params.ecomm_pagetype == "category") {
    AWIN.Tracking.Sayalota.pagetype = "category";
    AWIN.Tracking.Sayalota.category = google_tag_params.ecomm_category;
} else if (google_tag_params.ecomm_pagetype == "home") {
    AWIN.Tracking.Sayalota.pagetype = "home";
} else if (google_tag_params.ecomm_pagetype == "search") {
    AWIN.Tracking.Sayalota.pagetype = "search";
    AWIN.Tracking.Sayalota.searchQuery = google_tag_params.search_q;
}
```


# Plugin Code


``` javascript
AWIN.Tracking.Sayalota = AWIN.Tracking.Sayalota || {};
AWIN.Tracking.Sayalota.url = AWIN.Tracking.Sayalota.url || AWIN.sProtocol + "r.adserver01.de/znsa/data.php";

(function($s) {
    if ("undefined" === typeof $s.advertiserId) {
        return;
    }

    var pagetype = $s.pagetype || AWIN.Tracking.fetchZxParam('pagetype');

    if ("undefined" === typeof pagetype) {
        return;
    }

    if (AWIN.Tracking.Sale) {
        pagetype = "checkout";
    } else if ("checkout" === pagetype.toLowerCase()) {
        AWIN.Tracking.Sale = {};
    }

    $s.combineProducts = function(products) {
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

    $s.fetchBasketData = function() {
        var products = AWIN.Tracking.getBasketData();
        for (var i = 0; i < products.length; i++) {
            products[i].identifier = products[i].id;
            delete products[i].id;
        }
        return products;
    };

    var url = $s.url + "?" + AWIN.Tracking.buildQueryString({
        url: document.referrer,
        page: pagetype.toLowerCase(),
        token: $s.advertiserId
    });

    switch (pagetype.toLowerCase()) {
        case 'product':
        case 'home':
            url += "&" + AWIN.Tracking.buildQueryString({
                value: $s.identifier || AWIN.Tracking.fetchZxParam('identifier')
            });
            break;
        case 'category':
            url += "&" + AWIN.Tracking.buildQueryString({
                value: $s.category || AWIN.Tracking.fetchZxParam('category')
            });
            break;
        case 'search':
            url += "&" + AWIN.Tracking.buildQueryString({
                value: $s.searchQuery || AWIN.Tracking.fetchZxParam('search_query')
            });
            break;
        case 'basket':
            url += "&" + AWIN.Tracking.buildQueryString({
                value: $s.combineProducts(AWIN.Tracking.fetchZxParam('products') || $s.fetchBasketData())
            });
            break;
        case 'checkout':
            url += "&" + AWIN.Tracking.buildQueryString({
                value: AWIN.Tracking.fetchZxParam('total_amount') || AWIN.Tracking.Sale.amount
            });
            break;
        default:
            url += "&" + AWIN.Tracking.buildQueryString({
                value: $s.shopName || AWIN.Tracking.fetchZxParam('shop_name') || ""
            });
            break;
    }

    AWIN.Tracking.scriptAppend(url);
})(AWIN.Tracking.Sayalota);
```

