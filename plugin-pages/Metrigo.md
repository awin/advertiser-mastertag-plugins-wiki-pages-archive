
# Supported Pages

- Home Page
- Product Page
- Category Page
- Basket Page
- Checkout Page
- Registration Page
- Generic Page

# Configuration

Plugin supports Zanox parameters. Refer to the source code for more
details.

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Home Page Configuration


``` javascript
AWIN.Tracking.Metrigo = AWIN.Tracking.Metrigo || {};
AWIN.Tracking.Metrigo.pagetype = "home";
AWIN.Tracking.Metrigo.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Metrigo.source = "SOURCE";
```




## Product Page Configuration


``` javascript
AWIN.Tracking.Metrigo = AWIN.Tracking.Metrigo || {};
AWIN.Tracking.Metrigo.pagetype = "product";
AWIN.Tracking.Metrigo.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Metrigo.source = "SOURCE";
AWIN.Tracking.Metrigo.identifier = "PRODUCT_ID";
```




## Category Page Configuration


``` javascript
AWIN.Tracking.Metrigo = AWIN.Tracking.Metrigo || {};
AWIN.Tracking.Metrigo.pagetype = "category";
AWIN.Tracking.Metrigo.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Metrigo.source = "SOURCE";
AWIN.Tracking.Metrigo.category = "CATEGORY";
```




## Basket Page Configuration


``` javascript
AWIN.Tracking.Metrigo = AWIN.Tracking.Metrigo || {};
AWIN.Tracking.Metrigo.pagetype = "basket";
AWIN.Tracking.Metrigo.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Metrigo.source = "SOURCE";
```




## Checkout Page Configuration


``` javascript
AWIN.Tracking.Metrigo = AWIN.Tracking.Metrigo || {};
AWIN.Tracking.Metrigo.pagetype = "checkout";
AWIN.Tracking.Metrigo.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Metrigo.source = "SOURCE";
```




## Registration Page Configuration


``` javascript
AWIN.Tracking.Metrigo = AWIN.Tracking.Metrigo || {};
AWIN.Tracking.Metrigo.pagetype = "registration";
AWIN.Tracking.Metrigo.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Metrigo.source = "SOURCE";
```




## Generic Page Configuration


``` javascript
AWIN.Tracking.Metrigo = AWIN.Tracking.Metrigo || {};
AWIN.Tracking.Metrigo.pagetype = "generic";
AWIN.Tracking.Metrigo.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Metrigo.source = "SOURCE";
```




## Related JIRA Ticket

[PROD-3209](https://jira.awin.com/browse/PROD-3209)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/metrigo.js)