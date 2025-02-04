
# Supported Pages

- Product Page
- Checkout Page
- Basket Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## Product Page Configuration

``` javascript
AWIN.Tracking.GoPL = AWIN.Tracking.GoPL || {};
AWIN.Tracking.GoPL.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.GoPL.identifier = "IDENTIFIER";
AWIN.Tracking.GoPL.pagetype = "PAGE_TYPE";
```



## Checkout Page Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.GoPL = AWIN.Tracking.GoPL || {};
AWIN.Tracking.GoPL.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.GoPL.pagetype = "PAGE_TYPE";
```



## Basket Page Configuration

``` javascript
AWIN.Tracking.GoPL = AWIN.Tracking.GoPL || {};
AWIN.Tracking.GoPL.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.GoPL.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/goPl.js)