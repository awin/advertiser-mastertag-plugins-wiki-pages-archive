
# Supported Pages

- Product Page
- Checkout Page
- Basket Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## Checkout & Basket Page Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.ZanoxThirdParty = AWIN.Tracking.ZanoxThirdParty || {};
AWIN.Tracking.ZanoxThirdParty.token = "TOKEN";
AWIN.Tracking.ZanoxThirdParty.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.ZanoxThirdParty = AWIN.Tracking.ZanoxThirdParty || {};
AWIN.Tracking.ZanoxThirdParty.token = "TOKEN";
AWIN.Tracking.ZanoxThirdParty.identifier = "IDENTIFIER";
AWIN.Tracking.ZanoxThirdParty.productName = "PRODUCT_NAME";
AWIN.Tracking.ZanoxThirdParty.presso = "PRESSO";
AWIN.Tracking.ZanoxThirdParty.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/zanoxThirdParty.js)