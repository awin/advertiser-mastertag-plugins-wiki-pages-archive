
# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

The Remintrex plugin has different tags depending on the type of page
visited.

Plugin supports following `PAGETYPE`: category, product, basket,
checkout, generic

# Tag Plugin

|               |                      |
|---------------|----------------------|
| PluginType:   | Remintrex            |
| Plugin Setup: | "See Code Below"     |
| Active:       | "Tick The Check Box" |


== Plugin setup code == The code below goes into the plugin setup field
in the tag management form.

Replace `PARTNER_CODE` with real values supplied by Remintrex.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.


``` javascript
AWIN.Tracking.Remintrex = {};
AWIN.Tracking.Remintrex.partnerId = "PARTNER_CODE";
AWIN.Tracking.Remintrex.pagetype = "PAGETYPE_IDENTIFIER";
```



Example:


``` javascript
AWIN.Tracking.Remintrex = {};
AWIN.Tracking.Remintrex.partnerId = "7311";
AWIN.Tracking.Remintrex.pagetype = "generic";
```



(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

## Product Page

The plugin does not use the product scraper itself but you could use it
to fetch the ID if you prefer and supply it to the identifier config
variable.


``` javascript
AWIN.Tracking.Remintrex.identifier = "ID_OF_THE_PRODUCT";
```



Example:


``` javascript
AWIN.Tracking.Remintrex.identifier = google_tag_params.prodid[0];
```




## Category Page


``` javascript
AWIN.Tracking.Remintrex.category = "NAME_OF_CATEGORY";
```



Example:


``` javascript
AWIN.Tracking.Remintrex.category = google_tag_params.category;
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

Plugin automatically assigns the pagetype and retrieves the data if
<b>AWIN.Tracking.Sale</b> is present therefore it is not necessary to
add this part in configuration.

# Example Complete Setup


``` javascript
AWIN.Tracking.Remintrex = AWIN.Tracking.Remintrex || {};
AWIN.Tracking.Remintrex.partnerId = "7311";
AWIN.Tracking.Remintrex.pagetype = "generic";

if (google_tag_params.pagetype == "cart") {
    AWIN.Tracking.Remintrex.pagetype = "basket";
    var zx_products = [];
    for (var i = 0; i < google_tag_params.prodid.length; i++) {
        var o = {};
        o.identifier = google_tag_params.prodid[i];
        zx_products.push(o);
    }
} else if (google_tag_params.pagetype == "product") {
    AWIN.Tracking.Remintrex.pagetype = "product";
    AWIN.Tracking.Remintrex.identifier = google_tag_params.prodid[0];
    AWIN.Tracking.Remintrex.category = google_tag_params.prodCategory[0];
} else if (google_tag_params.pagetype == "category") {
    AWIN.Tracking.Remintrex.pagetype = "category";
    AWIN.Tracking.Remintrex.category = google_tag_params.category;
}
```

