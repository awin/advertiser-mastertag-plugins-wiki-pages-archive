
# Supported Pages

- Category Page
- Checkout Page
- Basket Page
- Home Page
- Generic Page
- Product Page
- Registration Page
- Search Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## All Pages Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.Xelsion = AWIN.Tracking.Xelsion || {};
AWIN.Tracking.Xelsion.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/xelsion.js)