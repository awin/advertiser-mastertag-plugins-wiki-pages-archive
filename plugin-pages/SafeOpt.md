
# Supported Pages

- Generic Page
- Checkout Page

# Configuration

Replace `"ADDSHOPPER_ACCOUNT_ID"` with value supplied by the partner.

## Generic Page Configuration

``` javascript
AWIN.Tracking.SafeOpt = AWIN.Tracking.SafeOpt || {};
AWIN.Tracking.SafeOpt.addShopperAccountId = "ADDSHOPPER_ACCOUNT_ID";
```



# Relevant Tickets

[PROD-9111](https://jira.awin.com/browse/PROD-9111)
[PROD-10489](https://jira.awin.com/browse/PROD-10489)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/safeOpt/plugin.js)