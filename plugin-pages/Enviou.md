
# Supported Pages

- Generic Page set up only (for all pages)

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Generic Page Configuration

``` javascript
AWIN.Tracking.Enviou = AWIN.Tracking.Enviou || {};
AWIN.Tracking.Enviou.clientToken = "SPECIFIC_CLIENT_TOKEN";
```


The plugin will not work if client token is not defined.

# Relevant Tickets

[PROD-9192](https://jira.awin.com/browse/PROD-9192)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/enviou/plugin.js)