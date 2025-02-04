
# Supported Pages

- Home Page
- Basket Page
- Product Page
- Category Page
- Checkout Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

This plugin supports Zanox Parameters. Refer to the source code for more
details.

## Home Page Configuration

``` javascript
AWIN.Tracking.Adrule = AWIN.Tracking.Adrule || {};
AWIN.Tracking.Adrule.campaignId = "CAMPAIGN_ID";
AWIN.Tracking.Adrule.pagetype = "PAGETYPE";
```



## Basket Page Configuration

Basket page requires Product Level Tracking to be implemented on
merchant's website.

``` javascript
AWIN.Tracking.Adrule = AWIN.Tracking.Adrule || {};
AWIN.Tracking.Adrule.campaignId = "CAMPAIGN_ID";
AWIN.Tracking.Adrule.pagetype = "PAGETYPE";
```



## Product Page Configuration

Product page requires Product Level Tracking to be implemented on
merchant's website.

``` javascript
AWIN.Tracking.Adrule = AWIN.Tracking.Adrule || {};
AWIN.Tracking.Adrule.campaignId = "CAMPAIGN_ID";
AWIN.Tracking.Adrule.pagetype = "PAGETYPE";
AWIN.Tracking.Adrule.identifier = "IDENTIFIER";
```



## Category Page Configuration

Product page requires Product Level Tracking to be implemented on
merchant's website.

``` javascript
AWIN.Tracking.Adrule = AWIN.Tracking.Adrule || {};
AWIN.Tracking.Adrule.campaignId = "CAMPAIGN_ID";
AWIN.Tracking.Adrule.pagetype = "PAGETYPE";
AWIN.Tracking.Adrule.category = "CATEGORY";
```



## Checkout Page Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website.

``` javascript
AWIN.Tracking.Adrule = AWIN.Tracking.Adrule || {};
AWIN.Tracking.Adrule.campaignId = "CAMPAIGN_ID";
AWIN.Tracking.Adrule.pagetype = "PAGETYPE";
```



# Relevant Tickets

[PROD-3243](https://jira.awin.com/browse/PROD-3243)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/adrule.js)