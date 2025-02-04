
# Supported Pages

- Product Page
- Category Page
- Basket Page
- Checkout Page

# Configuration

Plugin supports Zanox parameters. Refer to the source code for more
details.

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Category Page Configuration


``` javascript
AWIN.Tracking.MIRetargeting = AWIN.Tracking.MIRetargeting || {};
AWIN.Tracking.MIRetargeting.pagetype = "category";
AWIN.Tracking.MIRetargeting.token = "TOKEN";
AWIN.Tracking.MIRetargeting.category = "CATEGORY";
AWIN.Tracking.MIRetargeting.startDate = "START_DATE";
AWIN.Tracking.MIRetargeting.endDate = "END_DATE";
AWIN.Tracking.MIRetargeting.destination1 = "DESTINATION_1";
AWIN.Tracking.MIRetargeting.destination2 = "DESTINATION_2";
AWIN.Tracking.MIRetargeting.event = "EVENT";
```




## Product Page Configuration


``` javascript
AWIN.Tracking.MIRetargeting = AWIN.Tracking.MIRetargeting || {};
AWIN.Tracking.MIRetargeting.pagetype = "product";
AWIN.Tracking.MIRetargeting.token = "TOKEN";
AWIN.Tracking.MIRetargeting.identifier = "PRODUCT_ID";
AWIN.Tracking.MIRetargeting.startDate = "START_DATE";
AWIN.Tracking.MIRetargeting.endDate = "END_DATE";
AWIN.Tracking.MIRetargeting.destination1 = "DESTINATION_1";
AWIN.Tracking.MIRetargeting.destination2 = "DESTINATION_2";
AWIN.Tracking.MIRetargeting.origin = "ORIGIN";
AWIN.Tracking.MIRetargeting.image = "IMAGE";
```




## Basket Page Configuration


``` javascript
AWIN.Tracking.MIRetargeting = AWIN.Tracking.MIRetargeting || {};
AWIN.Tracking.MIRetargeting.pagetype = "basket";
AWIN.Tracking.MIRetargeting.token = "TOKEN";
```




## Checkout Page Configuration


``` javascript
AWIN.Tracking.MIRetargeting = AWIN.Tracking.MIRetargeting || {};
AWIN.Tracking.MIRetargeting.pagetype = "checkout";
AWIN.Tracking.MIRetargeting.token = "TOKEN";
```




## Related JIRA Ticket

[PROD-4698](https://jira.awin.com/browse/PROD-4698)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/miRetargeting.js)