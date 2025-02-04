
# Page types

The plugin will fire on all pages.

# Requirements

The MasterTag should fire on all pages unconditionally.

# Plugin Configuration Code

**NOTE:** The plugin can be turned on without adding **any** code in the
UI. The reason for this is that if no code is added in the UI config the
plugin will automatically take the Awin merchant ID (which it is using
as an identifier) from the MasterTag. However, if you do add code to the
UI config, then you **must** populate
`AWIN.Tracking.Contester.merchantId` with the Awin merchant ID manually.

In short, you can turn on the plugin without adding the below code.

The code below goes into the UI config: *Awin UI \> Toolbox \>
Advertiser MasterTag \> My Plug-ins \> Set-up* (please select plugin
name *Contester*).


``` javascript
AWIN.Tracking.Contester = AWIN.Tracking.Contester || {};
AWIN.Tracking.Contester.merchantId = "[AWIN MERCHANT ID]";
```


# Relevant Tickets

[PROD-10974](https://awin.atlassian.net/browse/PROD-10974)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/contester/plugin.js)