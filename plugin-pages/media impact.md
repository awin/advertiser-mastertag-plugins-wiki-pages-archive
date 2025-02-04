# Supported Pages

- Home Page
- Product Page
- Category Page
- Basket Page
- Checkout Page

# Configuration

Plugin supports Zanox parameters. Refer to the source code for more
details. AWIN.Tracking.MediaImpact.token should be populated with the
token value provided by the advertiser.

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Home Page Configuration


``` javascript
AWIN.Tracking.MediaImpact = AWIN.Tracking.MediaImpact || {};
AWIN.Tracking.MediaImpact.token = "cAwGsdFLLAYarAAdTOa";
AWIN.Tracking.MediaImpact.pagetype = "home";
AWIN.Tracking.MediaImpact.category = "CATEGORY";
AWIN.Tracking.MediaImpact.startdate = "START_DATE";
AWIN.Tracking.MediaImpact.enddate = "END_DATE";
AWIN.Tracking.MediaImpact.destination1 = "DESTINATION_1";
AWIN.Tracking.MediaImpact.destination2 = "DESTINATION_2";
AWIN.Tracking.MediaImpact.event = "EVENT";
```




## Product Page Configuration


``` javascript
AWIN.Tracking.MediaImpact = AWIN.Tracking.MediaImpact || {};
AWIN.Tracking.MediaImpact.token = "cAwGsdFLLAYarAAdTOa";
AWIN.Tracking.MediaImpact.pagetype = "product";
AWIN.Tracking.MediaImpact.category = "CATEGORY";
AWIN.Tracking.MediaImpact.startdate = "START_DATE";
AWIN.Tracking.MediaImpact.enddate = "END_DATE";
AWIN.Tracking.MediaImpact.origin = "ORIGIN";
AWIN.Tracking.MediaImpact.photo = "PHOTO";
```




## Category Page Configuration


``` javascript
AWIN.Tracking.MediaImpact = AWIN.Tracking.MediaImpact || {};
AWIN.Tracking.MediaImpact.token = "cAwGsdFLLAYarAAdTOa";
AWIN.Tracking.MediaImpact.pagetype = "category";
AWIN.Tracking.MediaImpact.category = "CATEGORY";
AWIN.Tracking.MediaImpact.startdate = "START_DATE";
AWIN.Tracking.MediaImpact.enddate = "END_DATE";
AWIN.Tracking.MediaImpact.destination1 = "DESTINATION_1";
AWIN.Tracking.MediaImpact.destination2 = "DESTINATION_2";
AWIN.Tracking.MediaImpact.event = "EVENT";
```




## Basket Page Configuration


``` javascript
AWIN.Tracking.MediaImpact = AWIN.Tracking.MediaImpact || {};
AWIN.Tracking.MediaImpact.token = "cAwGsdFLLAYarAAdTOa";
AWIN.Tracking.MediaImpact.pagetype = "basket";
```




## Checkout Page Configuration


``` javascript
AWIN.Tracking.MediaImpact = AWIN.Tracking.MediaImpact || {};
AWIN.Tracking.MediaImpact.token = "cAwGsdFLLAYarAAdTOa";
AWIN.Tracking.MediaImpact.pagetype = "checkout";
```




## Related JIRA Ticket

[PROD-5920](https://jira.awin.com/browse/PROD-5920)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/mediaImpact/plugin.js)