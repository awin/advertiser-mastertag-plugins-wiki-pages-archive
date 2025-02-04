
# Supported Pages

- Home Page
- Product Page
- Checkout Page
- Basket Page
- Category Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## Home Page Configuration && Basket Page Configuration

``` javascript
AWIN.Tracking.Facebook = AWIN.Tracking.Facebook || {};
AWIN.Tracking.Facebook.facebookId = "ID";
AWIN.Tracking.Facebook.advertiserName = "ADVERTISER_NAME";
AWIN.Tracking.Facebook.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.Facebook = AWIN.Tracking.Facebook || {};
AWIN.Tracking.Facebook.facebookId = "ID";
AWIN.Tracking.Facebook.advertiserName = "ADVERTISER_NAME";
AWIN.Tracking.Facebook.identifier = "IDENTIFIER";
AWIN.Tracking.Facebook.category = "CATEGORY";
AWIN.Tracking.Facebook.price = "PRICE";
AWIN.Tracking.Facebook.currency = "CURRENCY";
AWIN.Tracking.Facebook.pagetype = "PAGE_TYPE";
```



## Checkout Page Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.Facebook = AWIN.Tracking.Facebook || {};
AWIN.Tracking.Facebook.facebookId = "ID";
AWIN.Tracking.Facebook.advertiserName = "ADVERTISER_NAME";
AWIN.Tracking.Facebook.pagetype = "PAGE_TYPE";
```



## Category Page Configuration

``` javascript
AWIN.Tracking.Facebook = AWIN.Tracking.Facebook || {};
AWIN.Tracking.Facebook.facebookId = "ID";
AWIN.Tracking.Facebook.advertiserName = "ADVERTISER_NAME";
AWIN.Tracking.Facebook.category = "CATEGORY";
AWIN.Tracking.Facebook.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/facebook.js)