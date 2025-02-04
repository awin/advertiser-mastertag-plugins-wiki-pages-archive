
# Description

Captify are the largest aggregator of search data in Europe and provide
retargeting based on results from search boxes, toolbars and search
engines.

Tech contact: andrew.ward@captify.co.uk

# How is the tag implemented?

The Captify tag is always the same on every page, the only thing that
needs to change is the Captify merchantId. This is a number Captify
allocate to each individual client website. For example, JD Williams has
a Captify merchantId = 406.

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | Captify           |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form. Replace THE_ADVERTISER_SPECIFIC_ID with its real value supplied by
**Captify** for the merchant.


``` javascript
AWIN.Tracking.Captify = AWIN.Tracking.Captify || {};
AWIN.Tracking.Captify.merchantId = "SPECIFIC_CAPTIFY_MERCHANT_ID";
```

