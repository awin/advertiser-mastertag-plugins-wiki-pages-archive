
# Supported Pages

- Product Page
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
AWIN.Tracking.ZanoxMediaBrazil = AWIN.Tracking.ZanoxMediaBrazil || {};
AWIN.Tracking.ZanoxMediaBrazil.mtid = "MTID";
AWIN.Tracking.ZanoxMediaBrazil.token = "TOKEN";
AWIN.Tracking.ZanoxMediaBrazil.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/zanoxMediaBrazil.js)