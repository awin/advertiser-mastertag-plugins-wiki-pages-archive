# Supported Pages

- Checkout Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Checkout Page Configuration

Requires AWIN.Tracking.Sale object to be implemented on merchant's site.
Requires Required Product Level Tracking to be implemented on checkout
page.

``` javascript
AWIN.Tracking.CommerceConnect = AWIN.Tracking.CommerceConnect || {};
AWIN.Tracking.CommerceConnect.shopIdent = "ID";
```



# Relevant Tickets

[PROD-8551](https://jira.awin.com/browse/PROD-8551)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/commerceConnect/plugin.js)