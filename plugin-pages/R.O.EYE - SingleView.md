# Integration requirements

The Dwin1 tag needs to be displayed on every page, including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

The SingleView plugin will be added to all pages where master tag is
included and it will automatically detect checkout page where
AWIN.Tracking.Sale is included. More details can be found in the ‘Plugin
Configuration’ section of this document.

# Special program configuration

Please be aware that SingleView requires the following parameters to be
appended to the landing page (and should be added to the existing click
append).


``` javascript
sv1=affiliate&sv_campaign_id=!!!id!!!
```


Note: Please make sure the parameters are also added on membership level
IF there is already an existing append in place for that membership.
Please follow correct GET Parameter syntax

If there is a membership with Skimlinks publisher (ID: 78888, 181013)
please ensure following append is also added/set on membersip level:


``` javascript
&sv_campaign_id=!!!id!!!&sv_tax1=affiliate&sv_tax2=!!!publishertagid!!!&sv_tax3=!!!companyname!!!
&sv_tax4=!!!clickref!!!&sv_affiliate_id=!!!aid!!!
```


# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | R.O.EYE           |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

# Plugin Configuration

## Generic: All Pages

The code below goes into the plugin set-up field.


``` javascript
AWIN.Tracking.RoEye = AWIN.Tracking.RoEye || {};
```



**Example for linked merchant accounts (referrer credited):**

Replace `ADVERTISER_ID` with its real value.


``` javascript
AWIN.Tracking.RoEye = AWIN.Tracking.RoEye || {};
if (location.href.match(/de/i)) {
    AWIN.Tracking.RoEye.advertiserId = "ADVERTISER_ID_DE";
    AWIN.Tracking.RoEye.actionTrackerId = "ADVERTISER_ID_DE";
} else if (location.href.match(/nl/i)) {
    AWIN.Tracking.RoEye.advertiserId = "ADVERTISER_ID_NL";
    AWIN.Tracking.RoEye.actionTrackerId = "ADVERTISER_ID_NL";
}
```




# Plugin Code


``` javascript
AWIN.Tracking.RoEye = AWIN.Tracking.RoEye || {};
AWIN.Tracking.RoEye.advertiserId = AWIN.Tracking.RoEye.advertiserId || AWIN.Tracking.iMerchantId;
AWIN.Tracking.RoEye.actionTrackerId = AWIN.Tracking.RoEye.actionTrackerId || AWIN.Tracking.iMerchantId;
AWIN.Tracking.RoEye.url = AWIN.Tracking.RoEye.url || AWIN.sProtocol + "lantern.roeyecdn.com/";

(function ($r) {
    function findAwinScriptTagBySrcAttribute(srcAttribute) {
        return document
            .querySelector(
                "script[src='" + srcAttribute + "'][id^='_aw_script_']"
            );
    }

    if($r.advertiserId === 'undefined') {
        return;
    }

    var lanternGlobalJs = 'lantern_global_' + $r.advertiserId + '.min.js';
    var allPagesScript = AWIN.Tracking.RoEye.url + lanternGlobalJs;

    if (typeof AWIN.Tracking.Sale !== 'undefined') {
        var script = 'var lantern = {' +
            'order_id: "' + AWIN.Tracking.Sale.orderRef + '",' +
            'order_value: "' + AWIN.Tracking.Sale.amount + '",' +
            'order_currency: "' + AWIN.Tracking.Sale.currency + '"' +
        '};';

        if (typeof AWIN.Tracking.RoEye.actionTrackerId !== 'undefined') {
            script += 'lantern.action_tracker_id = "' + encodeURIComponent(AWIN.Tracking.RoEye.actionTrackerId) + '";';
        }

        AWIN.Tracking.scriptAppend(false, script);
    }

    if (
        typeof AWIN.Tracking.Sale !== 'undefined' ||
        findAwinScriptTagBySrcAttribute(allPagesScript) === null
    ) {
        AWIN.Tracking.scriptAppend(allPagesScript);
    }
})(AWIN.Tracking.RoEye);
```

