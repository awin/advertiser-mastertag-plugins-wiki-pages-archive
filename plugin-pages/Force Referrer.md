Force Referrer plugin allows for passing static referring URL

# Supported Pages

- Checkout Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Checkout Page Configuration

Requires AWIN.Tracking.Sale object to be implemented on merchant's
checkout site.

``` javascript
AWIN.Tracking.ForceReferrer = {};
AWIN.Tracking.ForceReferrer.link = 'https://www.hoppa.com';
```



# Relevant Tickets

[PROD-8984](https://jira.awin.com/browse/PROD-8984)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/forceReferrer/plugin.js)