
# Integration requirements

- The Dwin1 tag needs to be on all pages.

<!-- -->

- The Dwin1 tag needs to be displayed on the confirmation page as part
  of the Awin conversion tracking.

<!-- -->

- The Advertiser should be unconditionally tracking

# How is the tag implemented?

The Digital Group plugin appends the same script to every page, which
relies on a adTrackObject to provide correct configuration for specific
pages. The adTrackObject is automatically configured by the plugin as
long as the plugin has been correctly configured on the UI. Digital
Group plugin can be configured for basket and checkout pages in addition
to a default script which is added to every page.

This plugin requires a pmToken to be provided by Digital Group for
individual merchants.

|               |                      |
|---------------|----------------------|
| PluginType:   | DigitalGroup         |
| Plugin Setup: | "See Code Below"     |
| Active:       | "Tick The Check Box" |

## Plugin setup code

### Generic Pages

Default configuration for a script to be appended to every page. Replace
\`PM-TOKEN\` with token value provided by Digital Group for merchant
that this plugin is being configured for.


``` javascript
AWIN.Tracking.DigitalGroup = {};
AWIN.Tracking.DigitalGroup.pagetype = "home";
AWIN.Tracking.DigitalGroup.pmToken = "PM-TOKEN";
```


### Basket Page

Default configuration for basket page. Replace \`PM-TOKEN\` with token
value provided by Digital Group for merchant that this plugin is being
configured for.


``` javascript
AWIN.Tracking.DigitalGroup = {};
AWIN.Tracking.DigitalGroup.pagetype = "basket";
AWIN.Tracking.DigitalGroup.pmToken = "PM-TOKEN";
```


### Checkout Page

Default configuration for basket page. Replace \`PM-TOKEN\` with token
value provided by Digital Group for merchant that this plugin is being
configured for.

If the \`pagetype\` variable is not set, the plugin will default to
\`checkout\` page if AWIN.Tracking.Sale object is found.


``` javascript
AWIN.Tracking.DigitalGroup = {};
AWIN.Tracking.DigitalGroup.pagetype = "checkout";
AWIN.Tracking.DigitalGroup.pmToken = "PM-TOKEN";
```


# Plugin Source Code


``` javascript
AWIN.Tracking.DigitalGroup = AWIN.Tracking.DigitalGroup || {};
AWIN.Tracking.DigitalGroup.url =
    AWIN.Tracking.DigitalGroup.url || AWIN.sProtocol +
    "track.adform.net/serving/scripts/trackpoint/async/";

(function ($d) {
    let pageType = $d.pagetype;
    if (typeof pageType === "undefined" || typeof $d.pmToken === "undefined") {
        return;
    }

    if (AWIN.Tracking.Sale) {
        pageType = "checkout";
    } else if ("checkout" === pageType.toLowerCase()) {
        AWIN.Tracking.Sale = {};
    }

    let adTrackObj = {pm: $d.pmToken};
    switch (pageType.toLowerCase()) {
        case "basket":
            adTrackObj.divider = encodeURIComponent('|');
            adTrackObj.pagename = encodeURIComponent('simyo|Basket');
            break;
        case "checkout":
            let basketData = AWIN.Tracking.getBasketData();
            let itemsData = basketData.map(function (item) {
                return {
                    categoryname: item.category,
                    productsales: (item.price * item.quantity).toFixed(2)
                };
            });

            adTrackObj.divider = encodeURIComponent('|');
            adTrackObj.pagename = encodeURIComponent('simyo|Checkout');
            adTrackObj.order = {
                sales: AWIN.Tracking.Sale.amount,
                itms: itemsData
            };
            break;
    }

    window._adftrack =
        Array.isArray(window._adftrack) ?
    window._adftrack : (window._adftrack ? [window._adftrack] : []);
    window._adftrack.push(adTrackObj);

    AWIN.Tracking.scriptAppend($d.url, null, null, {"async":"true"});
})(AWIN.Tracking.DigitalGroup);
```

