
# Supported Pages

- Home Page
- Category Page
- Product Page
- Basket Page
- Checkout Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Home Page Configuration


``` javascript
AWIN.Tracking.QDivision = AWIN.Tracking.QDivision || {};
AWIN.Tracking.QDivision.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.QDivision.pagetype = "home";
```




## Category Page Configuration


``` javascript
AWIN.Tracking.QDivision = AWIN.Tracking.QDivision || {};
AWIN.Tracking.QDivision.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.QDivision.pagetype = "category";
AWIN.Tracking.QDivision.category = "CATEGORY_ID";
```




## Product Page Configuration


``` javascript
AWIN.Tracking.QDivision = AWIN.Tracking.QDivision || {};
AWIN.Tracking.QDivision.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.QDivision.pagetype = "product";
AWIN.Tracking.QDivision.brand = "BRAND_ID";
AWIN.Tracking.QDivision.category = "CATEGORY_ID";
AWIN.Tracking.QDivision.identifier = "IDENTIFIER_ID";
```




## Basket Page Configuration


``` javascript
AWIN.Tracking.QDivision = AWIN.Tracking.QDivision || {};
AWIN.Tracking.QDivision.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.QDivision.pagetype = "basket";
AWIN.Tracking.QDivision.identifier = "IDENTIFIER_ID";
```




## Checkout Page Configuration


``` javascript
AWIN.Tracking.QDivision = AWIN.Tracking.QDivision || {};
AWIN.Tracking.QDivision.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.QDivision.pagetype = "checkout";
```




# Related JIRA Ticket

[PROD-6590](https://jira.awin.com/browse/PROD-6590)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/qDivision.js)