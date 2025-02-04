
# Supported Pages

- Home Page
- Product Page
- Category Page
- Basket Page
- Checkout Page
- Generic Page

# Configuration

Plugin supports Zanox parameters. Refer to the source code for more
details.

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Home Page Configuration


``` javascript
AWIN.Tracking.MyThingsTravel = AWIN.Tracking.MyThingsTravel || {};
AWIN.Tracking.MyThingsTravel.pagetype = "home";
```




## Basket Page Configuration


``` javascript
AWIN.Tracking.MyThingsTravel = AWIN.Tracking.MyThingsTravel || {};
AWIN.Tracking.MyThingsTravel.pagetype = "basket";
```




## Search Page Configuration


``` javascript
AWIN.Tracking.MyThingsTravel = AWIN.Tracking.MyThingsTravel || {};
AWIN.Tracking.MyThingsTravel.pagetype = "search";
AWIN.Tracking.MyThingsTravel.identifier = "IDENTIFIER";
AWIN.Tracking.MyThingsTravel.startDate = "START_DATE";
AWIN.Tracking.MyThingsTravel.startDestination = "START_DESTINATION";
AWIN.Tracking.MyThingsTravel.stopDate = "STOP_DATE";
AWIN.Tracking.MyThingsTravel.stopDestination = "STOP_DESTINATION";
```




## Checkout Page Configuration


``` javascript
AWIN.Tracking.MyThingsTravel = AWIN.Tracking.MyThingsTravel || {};
AWIN.Tracking.MyThingsTravel.pagetype = "checkout";
AWIN.Tracking.MyThingsTravel.orderRef = "ORDER_REF";
AWIN.Tracking.MyThingsTravel.amount = "AMOUNT";
AWIN.Tracking.MyThingsTravel.currency = "CURRENCY";
```




## Product Page Configuration


``` javascript
AWIN.Tracking.MyThingsTravel = AWIN.Tracking.MyThingsTravel || {};
AWIN.Tracking.MyThingsTravel.pagetype = "product";
AWIN.Tracking.MyThingsTravel.identifier = "IDENTIFIER";
AWIN.Tracking.MyThingsTravel.startDate = "START_DATE";
AWIN.Tracking.MyThingsTravel.startDestination = "START_DESTINATION";
AWIN.Tracking.MyThingsTravel.stopDate = "STOP_DATE";
AWIN.Tracking.MyThingsTravel.stopDestination = "STOP_DESTINATION";
```




## Generic Page Configuration


``` javascript
AWIN.Tracking.MyThingsTravel = AWIN.Tracking.MyThingsTravel || {};
AWIN.Tracking.MyThingsTravel.pagetype = "generic";
```




## Related JIRA Ticket

[PROD-3193](https://jira.awin.com/browse/PROD-3193)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/myThingsTravel.js)