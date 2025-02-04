
# Description

RTB APP for internal use (Mediamath pixel firing)

# Integration requirements

- At a minimum Dwin tag to be shown unconditionally on capture pages
- The Dwin1 tag needs to be displayed on the confirmation page as part
  of the Awin conversion tracking.
- Merchant must be Unconditionally Tracking

# How is the tag implemented?

The MediamathProductRetargeting plugin fires one tag with advertiser id
and product id as parameters The tag will fire on the product page only.

# Tag Plugin

|              |                             |
|--------------|-----------------------------|
| PluginType:  | MediamathProductRetargeting |
| PluginSetup: | See Code Below              |
| Active       | Tick The Checkbox           |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form. Replace PAGETYPE with the actual page (oly necessary for the
product page). Replace SPECIFIC_MM_ADVERTISER with its real value
supplied by **MediaMath** for the Advertiser. Replace PRODUCT_ID with
the actual product identifier.


``` javascript
AWIN.Tracking.Mediamath = AWIN.Tracking.Mediamath || {};
AWIN.Tracking.Mediamath.pageType = 'PAGETYPE';
AWIN.Tracking.Mediamath.zxMMAdvertiserID = 'SPECIFIC_MM_ADVERTISER';
AWIN.Tracking.Mediamath.productZxIdentifier = 'PRODUCT_ID';
```


