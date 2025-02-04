
# Description

Ad6Profiling .

# Integration requirements

- At a minimum Dwin tag to be shown unconditionally on capture pages
- The Dwin1 tag needs to be displayed on the confirmation page as part
  of the Awin conversion tracking.
- Merchant must be Unconditionally Tracking

# How is the tag implemented?

The Ad6Profiling plugin fires one tag that reads a variable r6id in the
global scope which is filled with AWIN.Tracking.Ad6id. This tag will in
turn fire another tag based on the value of r6id. The tag will fire on
every page.

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | Ad6Profiling      |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `SPECIFIC_AD6_ADVERTISER` with its real value supplied by
**Ad6** for the Advertiser.


``` javascript
AWIN.Tracking.Ad6 = AWIN.Tracking.Ad6 || {};
AWIN.Tracking.Ad6.id = 'SPECIFIC_AD6_ADVERTISER';
```



Example:


``` javascript
AWIN.Tracking.Ad6 = AWIN.Tracking.Ad6 || {};
AWIN.Tracking.Ad6.id = "example1234";
```

