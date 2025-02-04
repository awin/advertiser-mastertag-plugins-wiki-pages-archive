
# Page types

The plugin will fire on all pages.

# Requirements

The MasterTag should fire on all pages unconditionally.

# Plugin Configuration Code

The code below goes into *Awin UI \> Toolbox \> Advertiser MasterTag \>
My Plug-ins \> Set-up* (please select plugin name *Converify*).

Please replace the "**TOKEN_ID**" placeholder with the identifiers
provided by the partner.


``` javascript
AWIN.Tracking.Converify = AWIN.Tracking.Converify || {};
AWIN.Tracking.Converify.tokenId = "TOKEN_ID";
```


# Example


``` javascript
AWIN.Tracking.Converify = AWIN.Tracking.Converify || {};
AWIN.Tracking.Converify.tokenId = "12345";
```


# Relevant Tickets

[PROD-10967](https://awin.atlassian.net/browse/PROD-10967)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/converify/plugin.js)