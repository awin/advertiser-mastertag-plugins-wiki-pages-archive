
# Supported Pages

- Home Page
- Product Page
- Checkout Page
- Basket Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## Basket & Checkout & Home Page Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.ShopBack = AWIN.Tracking.ShopBack || {};
AWIN.Tracking.ShopBack.adspaceId = "ADSPACE_ID";
AWIN.Tracking.ShopBack.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.ShopBack = AWIN.Tracking.ShopBack || {};
AWIN.Tracking.ShopBack.adspaceId = "ADSPACE_ID";
AWIN.Tracking.ShopBack.identifier = "IDENTIFIER";
AWIN.Tracking.ShopBack.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/shopBack.js)