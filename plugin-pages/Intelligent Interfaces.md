## Description

The Inteligent Intefaces mastertag will append a

<Script>

tag to the document to include the relevant advertiser’s II bundle.

## Integration requirements

Integrated advertiser will have a bespoke Javascript bundle hosted on
Inteligent Intefaces CDN.

## Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace { advertiser Id } with its real value.

### Template


``` javascript

AWIN.Tracking.IntelligentInterfaces = AWIN.Tracking.IntelligentInterfaces || {};
AWIN.Tracking.IntelligentInterfaces.advertiserId = { advertiser Id };
```


