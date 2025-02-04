
# Supported Pages

- Generic Page
- Basket Page
- Checkout Page
- Product Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## All Pages Configuration

``` javascript
AWIN.Tracking.DataAudience = AWIN.Tracking.DataAudience || {};
AWIN.Tracking.DataAudience.trackingId = "TRACKING_ID";
```



## Checkout Page Configuration

Requires AWIN.Tracking.Sale object to be implemented on merchant's site.

## Basket and Product Pages Configuration

Requires Product Level Tracking to be implemented on merchant's site.

# Relevant Tickets

NOT FOUND

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/DataAudience.js)