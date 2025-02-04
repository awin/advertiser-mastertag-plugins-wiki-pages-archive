
# Supported Pages

- Home Page
- Generic Page
- Basket Page
- Category Page
- Product Page
- Checkout Page
- Search Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

This plugin supports Zanox parameters. View the source code for more
details.

Accepted page type values are: home, category, product, basket,
checkout, search, generic.

## Home and Generic Pages Configuration

``` javascript
AWIN.Tracking.Alte = AWIN.Alte.ad4mat || {};
AWIN.Tracking.Alte.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Alte.pagetype = "PAGE_TYPE";
```



## Basket Pages Configuration

Basket Page requires Product Level Tracking to be implemented on
merchant's website.

``` javascript
AWIN.Tracking.Alte = AWIN.Alte.ad4mat || {};
AWIN.Tracking.Alte.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Alte.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

Product Page requires Product Level Tracking to be implemented on
merchant's website.

``` javascript
AWIN.Tracking.Alte = AWIN.Alte.ad4mat || {};
AWIN.Tracking.Alte.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Alte.pagetype = "PAGE_TYPE";
AWIN.Tracking.Alte.identifier = "IDENTIFIER";
```



## Category Page Configuration

``` javascript
AWIN.Tracking.Alte = AWIN.Alte.ad4mat || {};
AWIN.Tracking.Alte.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Alte.pagetype = "PAGE_TYPE";
AWIN.Tracking.Alte.category = "CATEGORY";
```



## Checkout Page Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website.

``` javascript
AWIN.Tracking.Alte = AWIN.Alte.ad4mat || {};
AWIN.Tracking.Alte.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Alte.pagetype = "PAGE_TYPE";
```



## Search Page Configuration

``` javascript
AWIN.Tracking.Alte = AWIN.Alte.ad4mat || {};
AWIN.Tracking.Alte.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Alte.pagetype = "PAGE_TYPE";
AWIN.Tracking.Alte.searchQuery = "SEARCH_QUERY";
```



# Relevant Tickets

[PROD-3203](https://jira.awin.com/browse/PROD-3203)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/alte.js)