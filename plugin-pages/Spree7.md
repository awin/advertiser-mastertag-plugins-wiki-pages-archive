
# Supported Pages

- Category Page
- Checkout Page
- Basket Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## All Pages Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.Spree7 = AWIN.Tracking.Spree7 || {};
AWIN.Tracking.Spree7.pixelIDs = "PIXEL_IDS";
AWIN.Tracking.Spree7.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/spree7.js)