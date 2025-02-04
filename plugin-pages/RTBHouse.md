
# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

The RTB House plugin has different tags depending on the type of page
visited.

Plugin supports following `PAGETYPE`: product, basket, checkout, home

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | RTB House         |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `RTBHouse_TOKEN` with its real value.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.


``` javascript
AWIN.Tracking.RTBHouse = AWIN.Tracking.RTBHouse || {};
AWIN.Tracking.RTBHouse.token = "RTBHouse_TOKEN";
AWIN.Tracking.RTBHouse.pagetype = "PAGETYPE_IDENTIFIER";
```





``` javascript
AWIN.Tracking.RTBHouse = AWIN.Tracking.RTBHouse || {};
AWIN.Tracking.RTBHouse.token = "1234";
AWIN.Tracking.RTBHouse.pagetype = "generic";
```



(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

## Product Page

The plugin does not use the product scraper itself but you could use it
to fetch the ID if you prefer and supply it to the identifier config
variable.


``` javascript
AWIN.Tracking.RTBHouse.identifier = "ID_OF_THE_PRODUCT";
```



Example:


``` javascript
AWIN.Tracking.RTBHouse.identifier = google_tag_params.ecomm_prodid;
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

Plugin automatically assigns the pagetype and retrieves the data if
<b>AWIN.Tracking.Sale</b> is present therefore it is not necessary to
add if statement for checkout page in the configuration.

Plugin requires product data (productIds and quantities) on the checkout
page. If client has Product Level Tracking Implemented on the checkout
page, data will be retrieved automatically. If PLT is not implemented,
data can be supplied to the plugin with array of products (zx_products).

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
AWIN.Tracking.RTBHouse = AWIN.Tracking.RTBHouse || {};
AWIN.Tracking.RTBHouse.token = "1234";
AWIN.Tracking.RTBHouse.pagetype = "generic";

var zx_products = [];

if (AWIN.Tracking.Sale) {
    for (var i = 0; i < dataLayer[1].ecommerce.transactionProducts; i++) {
        var o = {};
        o.identifier = dataLayer[1].ecommerce.transactionProducts[i].sku_code;
        o.quantity = dataLayer[1].ecommerce.transactionProducts[i].quantity;
        zx_products.push(o);
    }
} else if (google_tag_params.ecomm_pagetype == "cart") {
    AWIN.Tracking.RTBHouse.pagetype = "basket";
    for (var i = 0; i < dataLayer[1].ecommerce.basketProducts; i++) {
        var o = {};
        o.identifier = dataLayer[1].ecommerce.basketProducts[i].sku_code;
        o.quantity = dataLayer[1].ecommerce.basketProducts[i].quantity;
        zx_products.push(o);
    }
} else if (google_tag_params.ecomm_pagetype == "product") {
    AWIN.Tracking.RTBHouse.pagetype = "product";
    AWIN.Tracking.RTBHouse.identifier = google_tag_params.ecomm_prodid;
    AWIN.Tracking.RTBHouse.category = google_tag_params.ecomm_prod_category;
} else if (google_tag_params.ecomm_pagetype == "home") {
    AWIN.Tracking.RTBHouse.pagetype = "home";
}
```

