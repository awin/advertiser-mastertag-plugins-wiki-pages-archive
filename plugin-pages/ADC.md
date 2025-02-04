
# Integration requirements

<img src="Warning.png" title="Warning.png" width="37"
alt="Warning.png" /> NOTE: This plugin is deprecated.

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

The ADC plugin has different tags depending on the type of page visited.

Plugin supports following `PAGETYPE`: home, category, product, basket,
search, checkout, generic

# Tag example

<https://r.adc-serv.net/zn/data.php?url=&page=product&value=11212&token=9161>

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | ADC               |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `SPECIFIC_ADC_ADVERTISER_ID` with its real value.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.


``` javascript
AWIN.Tracking.ADC = AWIN.Tracking.ADC || {};
AWIN.Tracking.ADC.advertiserId = "SPECIFIC_ADC_ADVERTISER_ID";
AWIN.Tracking.ADC.pagetype = "PAGETYPE_IDENTIFIER";
```





``` javascript
AWIN.Tracking.ADC = AWIN.Tracking.ADC || {};
AWIN.Tracking.ADC.advertiserId = "9161";
AWIN.Tracking.ADC.pagetype = "generic";
```



(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

## Product Page

The plugin does not use the product scraper itself but you could use it
to fetch the ID if you prefer and supply it to the identifier config
variable.


``` javascript
AWIN.Tracking.ADC.identifier = "ID_OF_THE_PRODUCT";
```



Example:


``` javascript
AWIN.Tracking.ADC.identifier = google_tag_params.prodid[0];
```




## Category Page


``` javascript
AWIN.Tracking.ADC.category = "NAME_OF_CATEGORY";
```



Example:


``` javascript
AWIN.Tracking.ADC.category = google_tag_params.category;
```




## Search Results Page


``` javascript
AWIN.Tracking.ADC.searchQuery = "USER_SEARCH_TERMS";
```



Example:


``` javascript
AWIN.Tracking.ADC.searchQuery = google_tag_params.searchQ;
```




## Basket Page

Plugin requires product data (productIds) on the basket page. Data can
be supplied to the plugin with array of products (zx_products) or with
the PLT form.

Example:


``` javascript
var zx_products = [];
for (var i = 0; i < google_tag_params.prodid.length; i++) {
    var adctempProdArr = {};
    adctempProdArr.identifier = google_tag_params.prodid[i];
    zx_products.push(adctempProdArr);
}
```




## Checkout Page

Plugin automatically assigns the pagetype and retrieves the data if
<b>AWIN.Tracking.Sale</b> is present therefore it is not necessary to
add this part in configuration.

# Example Complete Setup


``` javascript

AWIN.Tracking.ADC = AWIN.Tracking.ADC || {};
AWIN.Tracking.ADC.advertiserId = "9161";
AWIN.Tracking.ADC.pagetype = "generic";

if (google_tag_params.pagetype == "cart") {
    AWIN.Tracking.ADC.pagetype = "basket";
    var zx_products = [];
    for (var i = 0; i < google_tag_params.prodid.length; i++) {
        var adctempProdArr = {};
        adctempProdArr.identifier = google_tag_params.prodid[i];
        zx_products.push(adctempProdArr);
    }
} else if (google_tag_params.pagetype == "product") {
    AWIN.Tracking.ADC.pagetype = "product";
    AWIN.Tracking.ADC.identifier = google_tag_params.prodid[0];
    AWIN.Tracking.ADC.category = google_tag_params.prodCategory[0];
} else if (google_tag_params.pagetype == "category") {
    AWIN.Tracking.ADC.pagetype = "category";
    AWIN.Tracking.ADC.category = google_tag_params.category;
} else if (google_tag_params.pagetype == "home") {
    AWIN.Tracking.ADC.pagetype = "home";
} else if (google_tag_params.pagetype == "searchPage") {
    AWIN.Tracking.ADC.pagetype = "search";
    AWIN.Tracking.ADC.searchQuery = google_tag_params.searchQ;
}
```


# Plugin Code

<https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/adc/plugin.js>