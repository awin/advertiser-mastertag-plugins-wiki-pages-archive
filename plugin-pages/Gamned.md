
# Supported Pages

- Home Page
- Product Page
- Checkout Page
- Category Page
- Search Page
- Basket Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## Home & Basket Page Configuration

``` javascript
AWIN.Tracking.Gamned = AWIN.Tracking.Gamned || {};
AWIN.Tracking.Gamned.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Gamned.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.Gamned = AWIN.Tracking.Gamned || {};
AWIN.Tracking.Gamned.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Gamned.identifier = "IDENTIFIER";
AWIN.Tracking.Gamned.category = "CATEGORY";
AWIN.Tracking.Gamned.pagetype = "PAGE_TYPE";
```



## Checkout Page Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.Gamned = AWIN.Tracking.Gamned || {};
AWIN.Tracking.Gamned.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Gamned.pagetype = "PAGE_TYPE";
```



## Category Page Configuration

``` javascript
AWIN.Tracking.Gamned = AWIN.Tracking.Gamned || {};
AWIN.Tracking.Gamned.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Gamned.category = "CATEGORY";
AWIN.Tracking.Gamned.pagetype = "PAGE_TYPE";
```



## Search Page Configuration

``` javascript
AWIN.Tracking.Gamned = AWIN.Tracking.Gamned || {};
AWIN.Tracking.Gamned.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Gamned.searchQuery = "SEARCH_QUERY";
AWIN.Tracking.Gamned.pagetype = "PAGE_TYPE";
AWIN.Tracking.Gamned.products = [
  { identifier: 123456, amount: "3.99", currency: "EUR", quantity: 1 },
  { identifier: 23456, amount: "5.99", currency: "EUR", quantity: 2 }
];
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/gamned.js)