# Supported Pages

- all
- checkout

## Requirements

Mastertag must be implemented unconditionally across all pages in the
shop.

Checkout page requires AWIN.Tracking.Sale object to be implemented
unconditionally on the confirmation page.

# Configuration

Replace `"TOKEN"` with real values.



``` javascript
AWIN.Tracking.PerfMaker = AWIN.Tracking.PerfMaker || {};
AWIN.Tracking.PerfMaker.token = "TOKEN";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/perfmaker/plugin.js)

# Ticket

[View on JIRA](https://jira.awin.com/browse/PROD-9527)