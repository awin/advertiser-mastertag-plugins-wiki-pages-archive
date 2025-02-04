
# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

TargetPerformance plugin has different tags depending on the type of
page visited.

Plugin supports following `PAGETYPE`: category, product, basket,
checkout, home, generic

|                  |                   |
|------------------|-------------------|
| **Plugin Type**  | TargetPerformance |
| **Plugin Setup** | See Code Below    |
| **Active**       | Tick the box      |

### Plugin Setup code

The code below goes into the plugin setup field in the tag management
form.

- Replace `CAMPAIGN_ID` with real value supplied by TargetPerformance.
- Replace `ADVERTISER_ID` with value supplied by TargetPerformance.
- Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties
  of the page.


``` javascript
AWIN.Tracking.TargetPerformance = {};
AWIN.Tracking.TargetPerformance.campaignId = "CAMPAIGN_ID";
AWIN.Tracking.TargetPerformance.advertiserId = "ADVERTISERID";
AWIN.Tracking.TargetPerformance.pagetype = "PAGETYPE_IDENTIFIER";
```





``` javascript
AWIN.Tracking.TargetPerformance = AWIN.Tracking.TargetPerformance || {};
AWIN.Tracking.TargetPerformance.advertiserId = "1234";
AWIN.Tracking.TargetPerformance.campaignId = "5678";
AWIN.Tracking.TargetPerformance.pagetype = "generic";
```




## Product Page

The plugin does not use the product scraper itself but you could use it
to fetch the ID if you prefer and supply it to the identifier config
variable.


``` javascript
AWIN.Tracking.TargetPerformance.identifier = "ID_OF_THE_PRODUCT";
```



Example:


``` javascript
AWIN.Tracking.TargetPerformance.identifier = google_tag_params.ecomm_prodid;
```




## Category Page


``` javascript
AWIN.Tracking.TargetPerformance.category = "NAME_OF_CATEGORY";
```



Example:


``` javascript
AWIN.Tracking.TargetPerformance.category = google_tag_params.ecomm_category;
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
the checkout page therefore if statement for <b>AWIN.Tracking.Sale</b>
has been added.


``` javascript
AWIN.Tracking.TargetPerformance = AWIN.Tracking.TargetPerformance || {};
AWIN.Tracking.TargetPerformance.advertiserId = "4876";
AWIN.Tracking.TargetPerformance.feedId = "3237";
AWIN.Tracking.TargetPerformance.pagetype = "generic";
var zx_products = [];

if (AWIN.Tracking.Sale) {
    for (var i = 0; i < dataLayer[1].ecommerce.transactionProducts; i++) {
        var o = {};
        o.identifier = dataLayer[1].ecommerce.transactionProducts[i].sku_code;
        o.quantity = dataLayer[1].ecommerce.transactionProducts[i].quantity;
        zx_products.push(o);
    }
} else if (google_tag_params.ecomm_pagetype == "cart") {
    AWIN.Tracking.TargetPerformance.pagetype = "basket";
    for (var i = 0; i < dataLayer[1].ecommerce.basketProducts; i++) {
        var o = {};
        o.identifier = dataLayer[1].ecommerce.basketProducts[i].sku_code;
        o.quantity = dataLayer[1].ecommerce.basketProducts[i].quantity;
        zx_products.push(o);
    }
} else if (google_tag_params.ecomm_pagetype == "product") {
    AWIN.Tracking.TargetPerformance.pagetype = "product";
    AWIN.Tracking.TargetPerformance.identifier = google_tag_params.ecomm_prodid;
} else if (google_tag_params.ecomm_pagetype == "category") {
    AWIN.Tracking.TargetPerformance.pagetype = "category";
    AWIN.Tracking.TargetPerformance.category = google_tag_params.ecomm_category;
} else if (google_tag_params.ecomm_pagetype == "home") {
    AWIN.Tracking.TargetPerformance.pagetype = "home";
}
```

