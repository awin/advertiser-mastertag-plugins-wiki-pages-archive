
# Supported Pages

- Generic Page
- Home Page
- Checkout Page
- Basket Page
- Product Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## All Pages Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.Zebestof = AWIN.Tracking.Zebestof || {};
AWIN.Tracking.Zebestof.referrer = "REFERRER";
AWIN.Tracking.Zebestof.siteId = "SITE_ID";
AWIN.Tracking.Zebestof.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.Zebestof = AWIN.Tracking.Zebestof || {};
AWIN.Tracking.Zebestof.referrer = "REFERRER";
AWIN.Tracking.Zebestof.siteId = "SITE_ID";
AWIN.Tracking.Zebestof.identifier = "IDENTIFIER";
AWIN.Tracking.Zebestof.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/zebestof.js)