
# Supported Pages

- Checkout Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## All Pages Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.TradeSpotting = AWIN.Tracking.TradeSpotting || {};
AWIN.Tracking.TradeSpotting.token = "TOKEN";
AWIN.Tracking.TradeSpotting.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/tradeSpotting.js)