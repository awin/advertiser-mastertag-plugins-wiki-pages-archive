
# Supported Pages

- Home Page
- Checkout Page
- Basket Page
- Generic Page
- Search Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## Home & Checkout & Generic Page Configuration

``` javascript
AWIN.Tracking.RTBHouseAustriaAirlines = AWIN.Tracking.RTBHouseAustriaAirlines || {};
AWIN.Tracking.RTBHouseAustriaAirlines.token = "TOKEN";
AWIN.Tracking.RTBHouseAustriaAirlines.pagetype = "PAGETYPE";
```



## Basket Page Configuration

``` javascript
AWIN.Tracking.RTBHouseAustriaAirlines = AWIN.Tracking.RTBHouseAustriaAirlines || {};
AWIN.Tracking.RTBHouseAustriaAirlines.token = "TOKEN";
AWIN.Tracking.RTBHouseAustriaAirlines.startOrder = "START_ORDER";
AWIN.Tracking.RTBHouseAustriaAirlines.pagetype = "PAGETYPE";
```



## Search Page Configuration

``` javascript
AWIN.Tracking.RTBHouseAustriaAirlines = AWIN.Tracking.RTBHouseAustriaAirlines || {};
AWIN.Tracking.RTBHouseAustriaAirlines.token = "TOKEN";
AWIN.Tracking.RTBHouseAustriaAirlines.departDate = "DEPART_DATE";
AWIN.Tracking.RTBHouseAustriaAirlines.returnDate = "RETURN_DATE";
AWIN.Tracking.RTBHouseAustriaAirlines.departure = "DEPARTURE";
AWIN.Tracking.RTBHouseAustriaAirlines.roundTrip = "ROUND_TRIP";
AWIN.Tracking.RTBHouseAustriaAirlines.persons = "PERSONS";
AWIN.Tracking.RTBHouseAustriaAirlines.destination = "DESTINATION";
AWIN.Tracking.RTBHouseAustriaAirlines.pagetype = "PAGETYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/rtbHouseAustriaAirlines.js)