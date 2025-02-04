# Description

SmarterClick's on site technology intelligently displays targeted site
overlays to the high percentage of shoppers who leave your site every
day without buying. We simply help convert browsers in to buyers,
increasing your conversion rate and revenue.

Website: <https://www.smarterclick.co.uk/>

Contacts: Ennis Al-Saiegh ennis@smarterclick.co.uk

Joe Gilmore joe@smarterclick.co.uk

# Integration requirements

- The Dwin1 tag needs to be on all pages.

<!-- -->

- The Dwin1 tag needs to be displayed on the confirmation page as part
  of the Awin conversion tracking.

<!-- -->

- The Advertiser should be unconditionally tracking

# How is the tag implemented?

The SmarterClick tag is always the same on every page, the only thing
that needs to change is the 'domain' parameter.

This is a unique id SmarterClick allocate to each individual client
website.

|               |                      |
|---------------|----------------------|
| PluginType:   | SmarterClick         |
| Plugin Setup: | "See Code Below"     |
| Active:       | "Tick The Check Box" |

## Plugin setup code

The code below goes into the plugin setup field in the tag management
form. Replace \`DOMAIN-PARAMETER\` with its real value supplied by
**SmarterClick** for the merchant.


``` javascript
AWIN.Tracking.SmarterClick = {};
AWIN.Tracking.SmarterClick.domain = "DOMAIN-PARAMETER";
```


For some complex integrations, multiple 'domain' parameters are
provided. These are specified as an array:


``` javascript
AWIN.Tracking.SmarterClick = {};
AWIN.Tracking.SmarterClick.domain = ["DOMAIN-PARAMETER1", "DOMAIN-PARAMETER2"];
```


Example (domain = should be removed from supplied params):


``` javascript
AWIN.Tracking.SmarterClick = {};
AWIN.Tracking.SmarterClick.domain = ["JJIeweZ65ZmF", "IoPlye?9rBnVy"];
```

