
# Supported Pages

- Landing Page
- Product Page
- Add to cart Page
- Category Page
- Search Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Add to cart Page Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.Squadata = AWIN.Tracking.Squadata || {};
AWIN.Tracking.Squadata.token = "TOKEN";
AWIN.Tracking.Squadata.identifier = "IDENTIFIER";
AWIN.Tracking.Squadata.transaction = "TRANSACTION";
AWIN.Tracking.Squadata.pagetype = "PAGE_TYPE";
```



## Category Page Configuration

``` javascript
AWIN.Tracking.Squadata = AWIN.Tracking.Squadata || {};
AWIN.Tracking.Squadata.token = "TOKEN";
AWIN.Tracking.Squadata.category = "CATEGORY";
AWIN.Tracking.Squadata.pagetype = "PAGE_TYPE";
```



## Landing Page Configuration

``` javascript
AWIN.Tracking.Squadata = AWIN.Tracking.Squadata || {};
AWIN.Tracking.Squadata.token = "TOKEN";
AWIN.Tracking.Squadata.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.Squadata = AWIN.Tracking.Squadata || {};
AWIN.Tracking.Squadata.token = "TOKEN";
AWIN.Tracking.Squadata.name = "NAME";
AWIN.Tracking.Squadata.identifier = "IDENTIFIER";
AWIN.Tracking.Squadata.pagetype = "PAGE_TYPE";
```



## Search Page Configuration

``` javascript
AWIN.Tracking.Squadata = AWIN.Tracking.Squadata || {};
AWIN.Tracking.Squadata.token = "TOKEN";
AWIN.Tracking.Squadata.identifier = "IDENTIFIER";
AWIN.Tracking.Squadata.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/squadata.js)