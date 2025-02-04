
# Supported Pages

- Generic Page
- Home Page
- Basket Page
- Category Page
- Search Page
- Product Page
- Checkout Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Supports Zanox parameters. For details, please view the source code
linked below.

## Generic Page Configuration

``` javascript
AWIN.Tracking.Adexda = AWIN.Tracking.Adexda || {};
AWIN.Tracking.Adexda.pagetype = "PAGETYPE";
AWIN.Tracking.Adexda.placementId = "PLACEMENT_ID";
AWIN.Tracking.Adexda.trackerId = "TRACKER_ID";
```



## Home Page Configuration

``` javascript
AWIN.Tracking.Adexda = AWIN.Tracking.Adexda || {};
AWIN.Tracking.Adexda.pagetype = "PAGETYPE";
AWIN.Tracking.Adexda.placementId = "PLACEMENT_ID";
AWIN.Tracking.Adexda.trackerId = "TRACKER_ID";
```



## Basket Page Configuration

``` javascript
AWIN.Tracking.Adexda = AWIN.Tracking.Adexda || {};
AWIN.Tracking.Adexda.pagetype = "PAGETYPE";
AWIN.Tracking.Adexda.placementId = "PLACEMENT_ID";
AWIN.Tracking.Adexda.trackerId = "TRACKER_ID";
```



## Category Page Configuration

``` javascript
AWIN.Tracking.Adexda = AWIN.Tracking.Adexda || {};
AWIN.Tracking.Adexda.pagetype = "PAGETYPE";
AWIN.Tracking.Adexda.placementId = "PLACEMENT_ID";
AWIN.Tracking.Adexda.trackerId = "TRACKER_ID";
AWIN.Tracking.Adexda.category = "CATEGORY";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.Adexda = AWIN.Tracking.Adexda || {};
AWIN.Tracking.Adexda.pagetype = "PAGETYPE";
AWIN.Tracking.Adexda.placementId = "PLACEMENT_ID";
AWIN.Tracking.Adexda.trackerId = "TRACKER_ID";
AWIN.Tracking.Adexda.category = "CATEGORY";
AWIN.Tracking.Adexda.identifier = "IDENTIFIER";
```



## Search Page Configuration

``` javascript
AWIN.Tracking.Adexda = AWIN.Tracking.Adexda || {};
AWIN.Tracking.Adexda.pagetype = "PAGETYPE";
AWIN.Tracking.Adexda.placementId = "PLACEMENT_ID";
AWIN.Tracking.Adexda.trackerId = "TRACKER_ID";
AWIN.Tracking.Adexda.searchQuery = "SEARCH_QUERY";
```



## Checkout Page Configuration

Requires AWIN.Tracking.Sale to be implemented on merchant's website.

``` javascript
AWIN.Tracking.Adexda = AWIN.Tracking.Adexda || {};
AWIN.Tracking.Adexda.pagetype = "PAGETYPE";
AWIN.Tracking.Adexda.placementId = "PLACEMENT_ID";
AWIN.Tracking.Adexda.trackerId = "TRACKER_ID";
```



# Relevant Tickets

[PROD-3225](https://jira.awin.com/browse/PROD-3225)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/adexda.js)