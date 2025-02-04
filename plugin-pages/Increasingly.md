# Supported Pages

All pages.

# Configuration

Replace `"CLIENT_ID"` and `"REGION"` with real values. These values
should be provided by Increasingly.

The plugin supports one of the following 3 regions: `"UK"`, `"US"`,
`"AU"`.


== Plugin Configuration Code ==

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website.


``` javascript
AWIN.Tracking.Increasingly = AWIN.Tracking.Increasingly || {};
AWIN.Tracking.Increasingly.token = "CLIENT_ID";
AWIN.Tracking.Increasingly.region = "REGION";
AWIN.Tracking.Increasingly.pagetype = "generic"; //always set to generic
```


## Example Configuration


``` javascript
AWIN.Tracking.Increasingly = AWIN.Tracking.Increasingly || {};
AWIN.Tracking.Increasingly.token = "007";
AWIN.Tracking.Increasingly.region = "UK";
AWIN.Tracking.Increasingly.pagetype = "generic" //always set to generic
```


# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/increasingly/plugin.js)

# Relevant Tickets

[PROD-10919](https://awin.atlassian.net/browse/PROD-10919)