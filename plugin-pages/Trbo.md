
# Supported Pages

- Search Page
- Checkout Page
- Home Page
- Category Page
- Product Page
- Basket Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## Search & Home & Category Pages Configuration

``` javascript
AWIN.Tracking.Trbo = AWIN.Tracking.Trbo || {};
AWIN.Tracking.Trbo.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.Trbo = AWIN.Tracking.Trbo || {};
AWIN.Tracking.Trbo.identifier = "IDENTIFIER";
AWIN.Tracking.Trbo.productName = "PRODUCT_NAME";
AWIN.Tracking.Trbo.price = "PRICE";
AWIN.Tracking.Trbo.pagetype = "PAGE_TYPE";
```



## Checkout Page Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.Trbo = AWIN.Tracking.Trbo || {};
AWIN.Tracking.Trbo.voucher = "VOUCHER";
AWIN.Tracking.Trbo.pagetype = "PAGE_TYPE";
```



## Basket Page Configuration

``` javascript
AWIN.Tracking.Trbo = AWIN.Tracking.Trbo || {};
AWIN.Tracking.Trbo.currency = "CURRENCY";
AWIN.Tracking.Trbo.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/trbo.js)