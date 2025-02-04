
# Page types

The plugin will fire on all pages. The plugin automatically detects the
confirmation/checkout page. In addition to this, the plugin supports a
"lead" page type where the user signs up for potential subscriptions,
newsletters, etc..

# Requirements

The MasterTag should fire on all page unconditionally.

# Plugin Configuration Code

The code below goes into *Awin UI \> Toolbox \> Advertiser MasterTag \>
My Plug-ins \> Set-up* (please select plugin name *TvScientific*).

Please replace "**TVSCI_ID**" placeholder with the identifiers provided
by the partner.

`AWIN.Tracking.TvScientific.pagetype` must be set to "generic" to enable
the plugin to work.


``` javascript
AWIN.Tracking.TvScientific = AWIN.Tracking.TvScientific || {};
AWIN.Tracking.TvScientific.tvsciID = 'TVSCI_ID';
AWIN.Tracking.TvScientific.pagetype = 'generic'; //must be defined as generic here
```


# Example Implementation (including lead page type)

**Please Note**: The below example includes the scenario where the
advertiser offers some sort of user subscription that the partner might
want to track, in many cases this will not be the case, therefore, the
only the first 3 lines of code are necessary.

For lead cases please make sure that 'LEAD_ORDER_REFERENCE' is replaced
with the subscription order reference.


``` javascript
AWIN.Tracking.TvScientific = AWIN.Tracking.TvScientific || {};
AWIN.Tracking.TvScientific.tvsciID = 'tvscientific-pix-o-ca6af412-5454-3412-12313-213212321232';
AWIN.Tracking.TvScientific.pagetype = 'generic'; //must be defined as generic here

//only for advertisers who offer subscriptions
if (location.pathname.includes("sign-up-page")) {
    AWIN.Tracking.TvScientific.pagetype = 'lead';
    AWIN.Tracking.TvScientific.eventId = 'LEAD_ORDER_REFERENCE';
}
```


# Relevant Tickets

[PROD-10689](https://awin.atlassian.net/browse/PROD-10689)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/tvScientific/plugin.js)