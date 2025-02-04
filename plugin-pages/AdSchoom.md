
# Supported Pages

- Home Page
- Basket Page
- Product Page
- Category Page
- Registration Page
- Checkout Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

This plugin supports Zanox parameters. View the source code for more
details.

Accepted page type values are: **home, category, product, basket,
checkout, registration**.

## Home Page Configuration

``` javascript
AWIN.Tracking.Adschoom = AWIN.Tracking.Adschoom || {};
AWIN.Tracking.Adschoom.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Adschoom.pagetype = "PAGE_TYPE";
```



## Basket Page Configuration

Basket Page requires Product Level Tracking to be implemented on
merchant's website.

``` javascript
AWIN.Tracking.Adschoom = AWIN.Tracking.Adschoom || {};
AWIN.Tracking.Adschoom.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Adschoom.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

Product Page requires Product Level Tracking to be implemented on
merchant's website.

``` javascript
AWIN.Tracking.Adschoom = AWIN.Tracking.Adschoom || {};
AWIN.Tracking.Adschoom.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Adschoom.pagetype = "PAGE_TYPE";
AWIN.Tracking.Adschoom.identifier = "IDENTIFIER";
```



## Category Page Configuration

``` javascript
AWIN.Tracking.Adschoom = AWIN.Tracking.Adschoom || {};
AWIN.Tracking.Adschoom.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Adschoom.pagetype = "PAGE_TYPE";
AWIN.Tracking.Adschoom.category = "CATEGORY";
```



## Registration Page Configuration

``` javascript
AWIN.Tracking.Adschoom = AWIN.Tracking.Adschoom || {};
AWIN.Tracking.Adschoom.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Adschoom.pagetype = "PAGE_TYPE";
```



## Checkout Page Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website.

``` javascript
AWIN.Tracking.Adschoom = AWIN.Tracking.Adschoom || {};
AWIN.Tracking.Adschoom.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Adschoom.pagetype = "PAGE_TYPE";
```



# Relevant Tickets

[PROD-3255](https://jira.awin.com/browse/PROD-3255)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/adschoom.js)