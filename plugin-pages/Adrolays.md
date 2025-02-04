
<figure>
<img src="Example.jpg" title="File:Example.jpg" />
<figcaption><a href="File:Example.jpg">File:Example.jpg</a></figcaption>
</figure>

# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

The Adrolays plugin has different tags depending on the type of page
visited.

Plugin supports following `PAGETYPE`: home, category, product, basket,
search, checkout

# Tag example

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | Adrolays          |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `SPECIFIC_ADC_ADVERTISER_ID` with its real value.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.


``` javascript
AWIN.Tracking.Adrolays = AWIN.Tracking.Adrolays || {};
AWIN.Tracking.Adrolays.advertiserId = "SPECIFIC_ADC_ADVERTISER_ID";
AWIN.Tracking.Adrolays.pagetype = "PAGETYPE_IDENTIFIER";
```





``` javascript
AWIN.Tracking.Adrolays = AWIN.Tracking.Adrolays || {};
AWIN.Tracking.Adrolays.advertiserId = "11223344";
AWIN.Tracking.Adrolays.pagetype = "PAGETYPE_IDENTIFIER";
```



(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

## Product Page

The plugin does not use the product scraper itself but you could use it
to fetch the ID if you prefer and supply it to the identifier config
variable.


``` javascript
AWIN.Tracking.Adrolays.identifier = "ID_OF_THE_PRODUCT";

//Supported travel specific variables
AWIN.Tracking.Adrolays.startdate = "TRAVEL_START_DATE";
AWIN.Tracking.Adrolays.enddate = "TRAVEL_STOP_DATE"
AWIN.Tracking.Adrolays.destination1 = "TRAVEL_START_DESTINATION";
AWIN.Tracking.Adrolays.destination2 = "TRAVEL_STOP_DESTINATION";
AWIN.Tracking.Adrolays.origin = "TRAVEL_ORIGIN";
AWIN.Tracking.Adrolays.image = "IMAGE_URL";
```



Example:


``` javascript
AWIN.Tracking.Adrolays.identifier = google_tag_params.prodid[0];
```




## Category Page


``` javascript
AWIN.Tracking.Adrolays.category = "NAME_OF_CATEGORY";

//Supported travel specific variables
AWIN.Tracking.Adrolays.startdate = "TRAVEL_START_DATE";
AWIN.Tracking.Adrolays.enddate = "TRAVEL_STOP_DATE"
AWIN.Tracking.Adrolays.destination1 = "TRAVEL_START_DESTINATION";
AWIN.Tracking.Adrolays.destination2 = "TRAVEL_STOP_DESTINATION";
```



Example:


``` javascript
AWIN.Tracking.Adrolays.category = google_tag_params.category;
```




## Search Results Page


``` javascript
AWIN.Tracking.Adrolays.searchQuery = "USER_SEARCH_TERMS";
```



Example:


``` javascript
AWIN.Tracking.Adrolays.searchQuery = google_tag_params.searchQ;
```




## Basket Page

Plugin requires product data (productIds) on the basket page. Data can
be supplied to the plugin with array of products (zx_products) or with
the PLT form.

Example:


``` javascript
var zx_products = [];
for (var i = 0; i < google_tag_params.prodid.length; i++) {
    var adrolaystempProdArr = {};
    adrolaystempProdArr.identifier = google_tag_params.prodid[i];
    zx_products.push(adrolaystempProdArr);
}
```




## Checkout Page

Plugin requires product data (productIds) on the checkout page. If
client has Product Level Tracking Implemented on the checkout page, data
will be retrieved automatically. If PLT is not implemented, data can be
supplied to the plugin with array of products (zx_products).

Example:


``` javascript
var zx_products = [];
for (var i = 0; i < google_tag_params.prodid.length; i++) {
    var adrolaystempProdArr = {};
    adrolaystempProdArr.identifier = google_tag_params.prodid[i];
    zx_products.push(adrolaystempProdArr);
}
```




# Example Complete Setup


``` javascript

AWIN.Tracking.Adrolays= AWIN.Tracking.Adrolays || {};
AWIN.Tracking.Adrolays.advertiserId = "11223344";
AWIN.Tracking.Adrolays.pagetype = "generic";

if (google_tag_params.pagetype == "cart") {
    AWIN.Tracking.Adrolays.pagetype = "basket";
} else if (google_tag_params.pagetype == "product") {
    AWIN.Tracking.Adrolays.pagetype = "product";
    AWIN.Tracking.Adrolays.identifier = google_tag_params.prodid[0];
} else if (google_tag_params.pagetype == "category") {
    AWIN.Tracking.Adrolays.pagetype = "category";
    AWIN.Tracking.Adrolays.category = google_tag_params.category;
} else if (google_tag_params.pagetype == "home") {
    AWIN.Tracking.Adrolays.pagetype = "home";
} else if (google_tag_params.pagetype == "searchPage") {
    AWIN.Tracking.Adrolays.pagetype = "search";
    AWIN.Tracking.Adrolays.searchQuery = google_tag_params.searchQ;
}

// Basket and checkout page:
var zx_products = [];
    for (var i = 0; i < google_tag_params.prodid.length; i++) {
    var adrolaystempProdArr = {};
    adrolaystempProdArr.identifier = google_tag_params.prodid[i];
    zx_products.push(adrolaystempProdArr);
    }
```

