
# Supported Pages

- Home Page
- Product Page
- Checkout Page
- Category Page
- Basket Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## Home & Checkout & Basket Page Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.RTBTracker = AWIN.Tracking.RTBTracker || {};
AWIN.Tracking.RTBTracker.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.RTBTracker.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.RTBTracker = AWIN.Tracking.RTBTracker || {};
AWIN.Tracking.RTBTracker.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.RTBTracker.identifier = "IDENTIFIER";
AWIN.Tracking.RTBTracker.pagetype = "PAGE_TYPE";
```



## Category Page Configuration

``` javascript
AWIN.Tracking.RTBTracker = AWIN.Tracking.RTBTracker || {};
AWIN.Tracking.RTBTracker.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.RTBTracker.category = "CATEGORY";
AWIN.Tracking.RTBTracker.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/rtbTracker.js)