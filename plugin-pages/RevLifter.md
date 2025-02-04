
# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

The RevLifter plugin has two different tags that need to be implemented
on every page.

# Tag Plugin

|               |                      |
|---------------|----------------------|
| PluginType:   | RevLifter            |
| Plugin Setup: | "See Code Below"     |
| Active:       | "Tick The Check Box" |


== Plugin setup code == The code below goes into the plugin setup field
in the tag management form.

Replace `URL` with real values supplied by RevLifter.

Replace `UUID` with real values supplied by RevLifter.


``` javascript
AWIN.Tracking.RevLifter = {};
AWIN.Tracking.RevLifter.url = "URL";
AWIN.Tracking.RevLifter.uuid = "UUID";
```



Example:


``` javascript
AWIN.Tracking.RevLifter = {};
AWIN.Tracking.RevLifter.url = "https://assets.revlifter.io/7829f288-55b9-471f-9e1f-6c95229241d3.js";
AWIN.Tracking.RevLifter.uuid = "7829f288-55b9-471f-9e1f-6c95229241d3";
```



(values in `UPPER_CASE` should be replaced with the appropriate values)