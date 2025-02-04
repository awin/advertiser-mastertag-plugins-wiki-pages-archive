# Description

# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

The UseMaxOnsite plugin has different tags depending on the type of page
visited.

Plugin supports following `PAGETYPE`: home, category, product, basket,
search, checkout, generic

# Tag example

<https://www.usermaxserver.de/d.php?ext_domain=1&rt=1&campaignId=9161>

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | UseMaxOnsite      |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `SPECIFIC_UseMaxOnsite_CAMPAIGN_ID` with its real value.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.


``` javascript
AWIN.Tracking.UseMaxOnsite = AWIN.Tracking.UseMaxOnsite || {};
AWIN.Tracking.UseMaxOnsite.campaignId = "SPECIFIC_UseMaxOnsite_CAMPAIGN_ID";
AWIN.Tracking.UseMaxOnsite.pagetype = "PAGETYPE_IDENTIFIER";
```





``` javascript
AWIN.Tracking.UseMaxOnsite = AWIN.Tracking.UseMaxOnsite || {};
AWIN.Tracking.UseMaxOnsite.campaignId = "9161";
AWIN.Tracking.UseMaxOnsite.pagetype = "generic";
```



(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

## Product Page

The plugin does not use the product scraper itself but you could use it
to fetch the ID if you prefer and supply it to the identifier config
variable.


``` javascript
AWIN.Tracking.UseMaxOnsite.identifier = "ID_OF_THE_PRODUCT";
```



Example:


``` javascript
AWIN.Tracking.UseMaxOnsite.identifier = google_tag_params.prodid[0];
```




## Category Page


``` javascript
AWIN.Tracking.UseMaxOnsite.category = "NAME_OF_CATEGORY";
```



Example:


``` javascript
AWIN.Tracking.UseMaxOnsite.category = google_tag_params.category;
```




## Search Results Page


``` javascript
AWIN.Tracking.UseMaxOnsite.searchQuery = "USER_SEARCH_TERMS";
```



Example:


``` javascript
AWIN.Tracking.UseMaxOnsite.searchQuery = google_tag_params.searchQ;
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
for (var i = 0; i < google_tag_params.prodid.length; i++) {
    var o = {};
    o.identifier = google_tag_params.prodid[i];
    zx_products.push(o);
}
```




# Example Complete Setup

Example below is written on the basis that there is no PLT implemented
on the checkout page. Product data array is the same on the basket and
the checkout page.


``` javascript
AWIN.Tracking.UseMaxOnsite = AWIN.Tracking.UseMaxOnsite || {};
AWIN.Tracking.UseMaxOnsite.campaignId = "9161";
AWIN.Tracking.UseMaxOnsite.pagetype = "generic";

if (google_tag_params.pagetype == "cart") {
    AWIN.Tracking.UseMaxOnsite.pagetype = "basket";
} else if (google_tag_params.pagetype == "product") {
    AWIN.Tracking.UseMaxOnsite.pagetype = "product";
    AWIN.Tracking.UseMaxOnsite.identifier = google_tag_params.prodid[0];
    AWIN.Tracking.UseMaxOnsite.category = google_tag_params.prodCategory[0];
} else if (google_tag_params.pagetype == "category") {
    AWIN.Tracking.UseMaxOnsite.pagetype = "category";
    AWIN.Tracking.UseMaxOnsite.category = google_tag_params.category;
} else if (google_tag_params.pagetype == "home") {
    AWIN.Tracking.UseMaxOnsite.pagetype = "home";
} else if (google_tag_params.pagetype == "searchPage") {
    AWIN.Tracking.UseMaxOnsite.pagetype = "search";
    AWIN.Tracking.UseMaxOnsite.searchQuery = google_tag_params.searchQ;
}

var zx_products = [];
for (var i = 0; i < google_tag_params.prodid.length; i++) {
    var o = {};
    o.identifier = google_tag_params.prodid[i];
    zx_products.push(o);
}
```

