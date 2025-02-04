
# Supported Pages

- Product Page
- Checkout Page
- Basket Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## Checkout & Basket Page Configuration

``` javascript
AWIN.Tracking.RetargetMedia = AWIN.Tracking.GDMDigital || {};
AWIN.Tracking.RetargetMedia.advertiserToken = "ADVERTISER_TOKEN";
AWIN.Tracking.RetargetMedia.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.RetargetMedia = AWIN.Tracking.GDMDigital || {};
AWIN.Tracking.RetargetMedia.advertiserToken = "ADVERTISER_TOKEN";
AWIN.Tracking.RetargetMedia.identifier = "IDENTIFIER";
AWIN.Tracking.RetargetMedia.category = "CATEGORY";
AWIN.Tracking.RetargetMedia.brand = "BRAND";
AWIN.Tracking.RetargetMedia.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/retargetMedia.js)