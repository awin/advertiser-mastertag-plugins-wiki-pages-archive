Custom Sale URL plugin allows for hardcoding "L" parameter value in
tracking sale URL.

# Supported Pages

- Checkout Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Checkout Page Configuration

Requires AWIN.Tracking.Sale object to be implemented on merchant's
checkout site.

``` javascript
AWIN.Tracking.CustomSaleUrl = AWIN.Tracking.CustomSaleUrl || {};
AWIN.Tracking.CustomSaleUrl.customLParameter = "L_PARAMETER_VALUE";
```



# Relevant Tickets

[PROD-8825](https://jira.awin.com/browse/PROD-8825)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/customSaleUrl/plugin.js)