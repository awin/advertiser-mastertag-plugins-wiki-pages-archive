
# Supported Pages

- Checkout Page
- Generic Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## All Pages Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.UIMUnsecure = AWIN.Tracking.UIMUnsecure || {};
AWIN.Tracking.UIMUnsecure.token = "TOKEN";
AWIN.Tracking.UIMUnsecure.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/uimUnsecure.js)