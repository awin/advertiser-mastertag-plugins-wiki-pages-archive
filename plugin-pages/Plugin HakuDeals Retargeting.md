
# Page types

The plugin will fire on all pages.

# Requirements

The MasterTag should fire on all pages unconditionally.

# Plugin Configuration Code

The code below goes into *Awin UI \> Toolbox \> Plugin Store \> My
Plugins \> Set-up* (please select plugin name *HakuDeals Retargeting*).

Please replace "**CAMPAIGN_ID**" and "**CAMPAIGN_NAME**" placeholders
with the identifiers provided by the partner.

The "**CAMPAIGN_NAME**" placeholder can be left **blank** if not
provided by the partner.


``` javascript
AWIN.Tracking.HakuDealsRetargeting = AWIN.Tracking.HakuDealsRetargeting || {};
AWIN.Tracking.HakuDealsRetargeting.campaignId = 'CAMPAIGN_ID';
AWIN.Tracking.HakuDealsRetargeting.campaignName = 'CAMPAIGN_NAME';
```


# Example


``` javascript
AWIN.Tracking.HakuDealsRetargeting = AWIN.Tracking.HakuDealsRetargeting || {};
AWIN.Tracking.HakuDealsRetargeting.campaignId = '12324-3eeb-123-872f-ef49c2aede73';
AWIN.Tracking.HakuDealsRetargeting.campaignName = 'Techsol';
```


# Relevant Tickets

[CORALSERV-360](https://awin.atlassian.net/browse/CORALSERV-360)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/hakuDealsRetargeting/plugin.js)