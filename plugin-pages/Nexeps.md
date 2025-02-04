
# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

The Nexeps plugin has different tags depending on the type of page
visited.

Plugin supports following `PAGETYPE`: category, product, basket,
checkout, generic, search, home

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | Nexeps            |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `Nexeps_CAMPAIGN_ID` with its real value.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.


``` javascript
AWIN.Tracking.Nexeps = AWIN.Tracking.Nexeps || {};
AWIN.Tracking.Nexeps.campaignId = "Nexeps_CAMPAIGN_ID";
AWIN.Tracking.Nexeps.pagetype = "PAGETYPE_IDENTIFIER";
```





``` javascript
AWIN.Tracking.Nexeps = AWIN.Tracking.Nexeps || {};
AWIN.Tracking.Nexeps.campaignId = "1767";
AWIN.Tracking.Nexeps.pagetype = "generic";
```



(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

## Product Page

The plugin does not use the product scraper itself but you could use it
to fetch the ID if you prefer and supply it to the identifier config
variable.


``` javascript
AWIN.Tracking.Nexeps.identifier = "ID_OF_THE_PRODUCT";
```



Example:


``` javascript
AWIN.Tracking.Nexeps.identifier = google_tag_params.ecomm_prodid;
```




## Category Page

The plugin does not use the product scraper itself but you could use it
to fetch the ID if you prefer and supply it to the identifier config
variable.


``` javascript
AWIN.Tracking.Nexeps.category = "ID_OF_THE_CATEGORY";
```



Example:


``` javascript
AWIN.Tracking.Nexeps.category = google_tag_params.ecomm_category;
```




## Search Results Page

The plugin does not use the product scraper itself but you could use it
to fetch the ID if you prefer and supply it to the identifier config
variable.


``` javascript
AWIN.Tracking.Nexeps.search_query = "USER_SEARCH_TERMS";
```



Example:


``` javascript
AWIN.Tracking.Nexeps.searchQuery = google_tag_params.ecomm_sQuery;
```




## Basket Page

Plugin requires product data (productIds) on the basket page. Data can
be supplied to the plugin with array of products (zx_products) or with
the PLT form.

Example:


``` javascript
var zx_products = [];
for (var i = 0; i < dataLayer[1].ecommerce.basketProducts; i++) {
    var o = {};
    o.identifier = dataLayer[1].ecommerce.basketProducts[i].sku_code;
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
for (var i = 0; i < dataLayer[1].ecommerce.transactionProducts; i++) {
    var o = {};
    o.identifier = dataLayer[1].ecommerce.transactionProducts[i].sku_code;
    zx_products.push(o);
}
```




# Example Complete Setup

Example below is written on the basis that there is no PLT implemented
on the checkout page. Product data array is different on the basket and
the checkout page therefore if statement for AWIN.Tracking.Sale has been
added.


``` javascript
AWIN.Tracking.Nexeps = AWIN.Tracking.Nexeps || {};
AWIN.Tracking.Nexeps.campaignId = "1767";
AWIN.Tracking.Nexeps.pagetype = "generic";

var zx_products = [];

if (AWIN.Tracking.Sale) {
    for (var i = 0; i < dataLayer[1].ecommerce.transactionProducts; i++) {
        var o = {};
        o.identifier = dataLayer[1].ecommerce.transactionProducts[i].sku_code;
        zx_products.push(o);
    }
} else if (google_tag_params.ecomm_pagetype == "cart") {
    AWIN.Tracking.Nexeps.pagetype = "basket";
    for (var i = 0; i < dataLayer[1].ecommerce.basketProducts; i++) {
        var o = {};
        o.identifier = dataLayer[1].ecommerce.basketProducts[i].sku_code;
        zx_products.push(o);
    }
} else if (google_tag_params.ecomm_pagetype == "product") {
    AWIN.Tracking.Nexeps.pagetype = "product";
    AWIN.Tracking.Nexeps.identifier = google_tag_params.ecomm_prodid;
} else if (google_tag_params.ecomm_pagetype == "home") {
    AWIN.Tracking.Nexeps.pagetype = "home";
} else if (google_tag_params.ecomm_pagetype == "category") {
    AWIN.Tracking.Nexeps.pagetype = "category";
    AWIN.Tracking.Nexeps.category = google_tag_params.ecomm_category;
} else if (google_tag_params.ecomm_pagetype == "search") {
    AWIN.Tracking.Nexeps.pagetype = "search";
    AWIN.Tracking.Nexeps.search_query = google_tag_params.ecomm_sQuery;
}
```


## JIRA Ticket

[PROD-3177](https://jira.awin.com/browse/PROD-3177)

## Source Code

[View in
Github](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/nexeps.js)