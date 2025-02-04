
# Supported Pages

- Home Page
- Product Page
- Category Page
- Basket Page
- Checkout Page
- Registration Page
- Search Page

# Configuration

Plugin supports Zanox parameters. Refer to the source code for more
details.

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Home Page Configuration


``` javascript
AWIN.Tracking.MyThingsZanox = AWIN.Tracking.MyThingsZanox || {};
AWIN.Tracking.MyThingsZanox.pagetype = "home";
MyThings.Event.Visit = "VISIT"
```




## Basket Page Configuration


``` javascript
AWIN.Tracking.MyThingsZanox = AWIN.Tracking.MyThingsZanox || {};
AWIN.Tracking.MyThingsZanox.pagetype = "basket";
MyThings.Event.Visit = "VISIT"
```




## Category Page Configuration


``` javascript
AWIN.Tracking.MyThingsZanox = AWIN.Tracking.MyThingsZanox || {};
AWIN.Tracking.MyThingsZanox.pagetype = "basket";
AWIN.Tracking.MyThingsZanox.category = "CATEGORY";
MyThings.Event.Visit = "VISIT"
```




## Checkout Page Configuration


``` javascript
AWIN.Tracking.MyThingsZanox = AWIN.Tracking.MyThingsZanox || {};
AWIN.Tracking.MyThingsZanox.pagetype = "checkout";
MyThings.Event.Conversion = "CONVERSION"
```




## Registration Page Configuration


``` javascript
AWIN.Tracking.MyThingsZanox = AWIN.Tracking.MyThingsZanox || {};
AWIN.Tracking.MyThingsZanox.pagetype = "registration";
MyThings.Event.Conversion = "CONVERSION"
```




## Product Page Configuration


``` javascript
AWIN.Tracking.MyThingsZanox = AWIN.Tracking.MyThingsZanox || {};
AWIN.Tracking.MyThingsZanox.pagetype = "product";
AWIN.Tracking.MyThingsZanox.identifier = "IDENTIFIER";
AWIN.Tracking.MyThingsZanox.productName = "PRODUCT_NAME";
AWIN.Tracking.MyThingsZanox.category = "CATEGORY";
AWIN.Tracking.MyThingsZanox.brand = "BRAND";
AWIN.Tracking.MyThingsZanox.price = "PRICE";
AWIN.Tracking.MyThingsZanox.currency = "CURRENCY";
AWIN.Tracking.MyThingsZanox.detailUrl = "DETAUIL_URL";
AWIN.Tracking.MyThingsZanox.imageUrl = "IMAGE_URL";
MyThings.Event.Visit = "VISIT"
```




## Search Page Configuration


``` javascript
AWIN.Tracking.MyThingsZanox = AWIN.Tracking.MyThingsZanox || {};
AWIN.Tracking.MyThingsZanox.pagetype = "search";
AWIN.Tracking.MyThingsZanox.searchCity = "SEARCH_CITY";
AWIN.Tracking.MyThingsZanox.searchCountry = "SEARCH_COUNTRY";
AWIN.Tracking.MyThingsZanox.searchQuery = "SEARCH_QUERY";
AWIN.Tracking.MyThingsZanox.identifier = "IDENTIFIER";
MyThings.Event.Visit = "VISIT"
```




## Related JIRA Ticket

[PROD-3302](https://jira.awin.com/browse/PROD-3302)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/myThingsZanox.js)