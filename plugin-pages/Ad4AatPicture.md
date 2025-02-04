
# Supported Pages

- Generic Page set up only (for all pages)

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Generic Page Configuration

``` javascript
AWIN.Tracking.Ad4matPicture = AWIN.Tracking.ad4mat || {};
AWIN.Tracking.Ad4matPicture.jQueryUrl = "SPECIFIC_AD4MAT_ADVERTISER_ID";
AWIN.Tracking.Ad4matPicture.adspaceId = "SPECIFIC_AD4MAT_COUNTRY_URL"; //Required
AWIN.Tracking.Ad4matPicture.connectIdPublisher = "PUBLISHER_ID";
AWIN.Tracking.Ad4matPicture.connectIdDeveloper = "DEVELOPER_ID";
AWIN.Tracking.Ad4matPicture.imageSelector = "IMAGE_SELECTOR";
```



# Relevant Tickets

[PROD-3240](https://jira.awin.com/browse/PROD-3240)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/ad4matPicture.js)