
# Description

Admedo are an RTB platform for display, mobile and retargeting. They
provide targeting and data insights to their advertisers

Tech contact: david.ayre@admedo.com

# Integration requirements

- The Dwin1 tag needs to be displayed on every page including the
  confirmation page as part of the Awin conversion tracking.

<!-- -->

- Ensure post view transactions are enabled for the account in the
  provider area and cookie duration is correct

<!-- -->

- If an adblocker solution is enabled - 'Click redirect to custom
  domain' **must** be enabled to ensure pv cookies are dropped on the
  alternate domain.

**De-duping clients**

Ensure there is a seperate channel set up within the clients channel
parameter rules. More information on setting these rules can be found
here: [Channel Parameter](#Channel_Parameter "wikilink")


# How is the tag implemented?

The Admedo plugin has two different tags depending on the page visited.

The retargeting pixel will be the same on every page, the only thing
that needs to be configured for this is the Admedo specified
\`retargetingPixelId\`.

The other is the conversion pixel which only appears on a sale page
which requires the Admedo specified \`conversionPixelId\` to be
configured .

These IDs are specified by Admedo which they allocate to each individual
client website.

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | Admedo            |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace SPECIFIC_ADMEDO_CONVERSION_PIXEL_ID &
SPECIFIC_ADMEDO_RETARGETING_PIXEL_ID with its real value supplied by
**Admedo** for the Advertiser.


``` javascript
AWIN.Tracking.Admedo = AWIN.Tracking.Admedo || {};
AWIN.Tracking.Admedo.conversionPixelId = "SPECIFIC_ADMEDO_CONVERSION_PIXEL_ID";
AWIN.Tracking.Admedo.retargetingPixelId = "SPECIFIC_ADMEDO_RETARGETING_PIXEL_ID";
```




# Ensure appropriate tracking links are used:

- Post View (Post Impression) Cookie Link :
  <http://awin1.com/appshow.php?a=AFFILIATE_ID&m=MERCHANT_ID>
- Post Click link to merchant site:
  <http://www.awin1.com/awclick.php?mid=MERCHANT_ID&id=AFFILIATE_ID>