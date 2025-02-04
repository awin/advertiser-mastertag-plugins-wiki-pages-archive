
# Requirements

The plugin should fire on a specific page type, which the advertiser has
tagged with the following dataLayer variable:
`{tyvisoRewardsPage : true}`. The advertiser must make the
afore-mentioned variable available in the dataLayer, it is a condition
they agreed with during the onboarding phase.

# Plugin setup code

Property `partnerId` should be provided by the partner.

The code below goes into *Awin UI \> Toolbox \> Advertiser MasterTag \>
My Plug-ins \> Set-up* (please select plugin name *United Interent
Media*).


``` javascript
AWIN.Tracking.TyvisoRewards = AWIN.Tracking.TyvisoRewards || {};
AWIN.Tracking.TyvisoRewards.partnerId = "PARTNER_ID";
```


### Example


``` javascript
AWIN.Tracking.TyvisoRewards = AWIN.Tracking.TyvisoRewards || {};
AWIN.Tracking.TyvisoRewards.partnerId = "631b001c5d1231232f663520b";
```


## Additional config

The plugin will search for `tyvisoRewardsPage` in the dataLayer. If this
variable is present in the dataLayer but the plugin fails to pick it up
automatically you can configure it manually to do so by using the
`pageType` property.

### Example


``` javascript
AWIN.Tracking.TyvisoRewards = AWIN.Tracking.TyvisoRewards || {};
AWIN.Tracking.TyvisoRewards.partnerId = "631b001c5d1231232f663520b";

if (dataLayer.filter(x=>x.tyvisoRewardsPage).length > 0) {
    AWIN.Tracking.TyvisoRewards.pageType = true;
}
```


# Relevant Tickets

[SOLUTION-44152](https://jira.awin.com/browse/SOLUTION-44152)
[PROD-10552](https://jira.awin.com/browse/PROD-10552)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/tyvisoRewards/plugin.js)