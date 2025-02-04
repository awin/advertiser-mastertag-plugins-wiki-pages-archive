
# Page types

The plugin will fire on all pages.

# Requirements

The MasterTag should fire on all pages unconditionally.

# Plugin Configuration Code

The code below goes into *Awin UI \> Toolbox \> Advertiser MasterTag \>
My Plug-ins \> Set-up* (please select plugin name *Aluna*).

Please replace "**CAMPAIGN_ID**" and "**CAMPAIGN_NAME**" placeholders
with the identifiers provided by the partner.

The "**CAMPAIGN_NAME**" placeholder can be left **blank** if not
provided by the partner.


``` javascript
AWIN.Tracking.Aluna = AWIN.Tracking.Aluna || {};
AWIN.Tracking.Aluna.campaignId = "CAMPAIGN_ID";
AWIN.Tracking.Aluna.campaignName = "CAMPAIGN_NAME";
```


# Example


``` javascript
AWIN.Tracking.Aluna = AWIN.Tracking.Aluna || {};
AWIN.Tracking.Aluna.campaignId = "12345";
AWIN.Tracking.Aluna.campaignName = "";
```


# Relevant Tickets

[PROD-10201](https://jira.awin.com/browse/PROD-10520)
[PROD-10506](https://jira.awin.com/browse/PROD-10506)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/aluna/plugin.js)