# Requirements

AWIN mastertag must be implemented unconditionally across all pages in
the shop.

# Supported Pages

- all
- product

# Configuration

This plugins supports two types of campaigns and thus configurations.


**Static:**
No configuration is required.

**KI - Integration** (dynamic):
For this type of configuration, following is required.

- page type must ALWAYS be set as "product" (regardless of the actual
  pagetype).
- product identifier for product pages (sometimes campaign pages)
- landing page URL supplied by Bounce Experts / advertiser



``` javascript
AWIN.Tracking.BounceExperts = AWIN.Tracking.BounceExperts|| {};
AWIN.Tracking.BounceExperts.pagetype = "product";    //always set regardless of page type
AWIN.Tracking.BounceExperts.landingPageUrl = "LANDING PAGE URL"; //landing page URL incl. protocol
if (document.location.href.match(/product/)) {
    AWIN.Tracking.BounceExperts.productId = "PRODUCT_ID";    //only set on product pages
}
```

# Configuration Example

``` javascript
AWIN.Tracking.BounceExperts = AWIN.Tracking.BounceExperts|| {};
AWIN.Tracking.BounceExperts.pagetype = "product";    //always set regardless of page type
AWIN.Tracking.BounceExperts.landingPageUrl = "https://beispiel.lp.bounce-page.de/"; //always set - landing page URL incl. protocol
if (document.location.href.match(/product/)) {
    AWIN.Tracking.BounceExperts.productId = "PRODUCT_ID";    //only set on product pages
}
```




**Good to know:**


In rare cases - e.g. provider offering white label solutions to
advertisers - the script path must be changed.
Currently default value is
<https://api.bounce-management.de/bounce.min.js>
In order to overwrite the script path, following configuration is
required.

``` javascript
AWIN.Tracking.BounceExperts = AWIN.Tracking.BounceExperts|| {};
AWIN.Tracking.BounceExperts.url = "NEW_SCRIPT_PATH"; // e.g. "https://api.bounce-management.com/custom.js"
```


= Plugin Source Code = [View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/bounceExperts/plugin.js)

# Tickets

[PROD-9649](https://jira.awin.com/browse/PROD-9649)
[PROD-9925](https://jira.awin.com/browse/PROD-9925)
[PROD-9932](https://jira.awin.com/browse/PROD-9932)