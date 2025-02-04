# \[\[Staff:Plugin_OneTag\|\[-\] OneTag\]\]

## **UNDER CONSTRUCTION, DO NOT USE**

## **UNDER CONSTRUCTION, DO NOT USE**

## **UNDER CONSTRUCTION, DO NOT USE**

# How is the tag implemented?

The OneTagplugin has different tags depending on the type of page
visited.

Plugin supports following `PAGETYPE`: home, product, cart, order

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `ADVERTISER_ID`, `CAMPAIGN_ID`, `SESSION_ID`, `PAGE_LANGUAGE`,
`SEARCH_QUERY` with its real value.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.


``` javascript
AWIN.Tracking.OneTag = AWIN.Tracking.OneTag || {};
AWIN.Tracking.OneTag.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.OneTag.campaignId = "CAMPAIGN_ID";
AWIN.Tracking.OneTag.pagetype = "PAGETYPE_IDENTIFIER";
AWIN.Tracking.OneTag.pageLanguage = "PAGE_LANGUAGE"; //can be hardcoded
AWIN.Tracking.OneTag.searchQuery = "SEARCH_QUERY";
AWIN.Tracking.OneTag.sessionId = "SESSION_ID";
```

