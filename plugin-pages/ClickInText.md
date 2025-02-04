
# Supported Pages

- Home Page
- Basket Page
- Category Page
- Checkout Page
- Product Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Home Page Configuration

``` javascript
AWIN.Tracking.ClickInText = AWIN.Tracking.ClickInText || {};
AWIN.Tracking.ClickInText.token = "TOKEN";
AWIN.Tracking.ClickInText.pagetype = "PAGE_TYPE";
```



## Basket Page Configuration

Requires Product Level Tracking to be implemented on merchant's site.

``` javascript
AWIN.Tracking.ClickInText = AWIN.Tracking.ClickInText || {};
AWIN.Tracking.ClickInText.token = "TOKEN";
AWIN.Tracking.ClickInText.pagetype = "PAGE_TYPE";
```



## Category Page Configuration

``` javascript
AWIN.Tracking.ClickInText = AWIN.Tracking.ClickInText || {};
AWIN.Tracking.ClickInText.token = "TOKEN";
AWIN.Tracking.ClickInText.pagetype = "PAGE_TYPE";
AWIN.Tracking.ClickInText.category = "CATEGORY";
```



## Checkout Page Configuration

Requires AWIN.Tracking.Sale object to be implemented on merchant's site.

``` javascript
AWIN.Tracking.ClickInText = AWIN.Tracking.ClickInText || {};
AWIN.Tracking.ClickInText.token = "TOKEN";
AWIN.Tracking.ClickInText.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

Requires AWIN.Tracking.Sale object to be implemented on merchant's site.

``` javascript
AWIN.Tracking.ClickInText = AWIN.Tracking.ClickInText || {};
AWIN.Tracking.ClickInText.token = "TOKEN";
AWIN.Tracking.ClickInText.pagetype = "PAGE_TYPE";
AWIN.Tracking.ClickInText.identifier = "ID";
```



# Relevant Tickets

[PROD-3394](https://jira.awin.com/browse/PROD-3394)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/clickInText.js)