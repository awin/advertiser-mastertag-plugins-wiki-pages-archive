
# Supported Pages

- Home Page
- Checkout Page
- Basket Page
- Product Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## Basket Page Configuration

Basket page requires Awin basket to be implemented on merchant's
website.

``` javascript
AWIN.Tracking.Uptain = AWIN.Tracking.Uptain || {};
AWIN.Tracking.Uptain.token = "TOKEN";
AWIN.Tracking.Uptain.currency = "CURRENCY";
AWIN.Tracking.Uptain.pagetype = "PAGE_TYPE";
```



## Checkout & Home Page Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.Uptain = AWIN.Tracking.Uptain || {};
AWIN.Tracking.Uptain.token = "TOKEN";
AWIN.Tracking.Uptain.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.Uptain = AWIN.Tracking.Uptain || {};
AWIN.Tracking.Uptain.token = "TOKEN";
AWIN.Tracking.Uptain.amount = "AMOUNT";
AWIN.Tracking.Uptain.currency = "CURRENCY";
AWIN.Tracking.Uptain.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/uptain.js)