
The plugin will be loaded for all pages.

## Plugin setup

Replace `"VALUE_PLACEHOLDERS"` with real values.


``` javascript
AWIN.Tracking.Envolvetech = AWIN.Tracking.Envolvetech || {};
AWIN.Tracking.Envolvetech.dataIdentifier = "DATA_IDENTIFIER";
```



===Mandatory values===

- DATA_IDENTIFIER - identifier of the campaign from the publisher

### Example


``` javascript
AWIN.Tracking.Envolvetech = AWIN.Tracking.Envolvetech || {};
AWIN.Tracking.Envolvetech.dataIdentifier = "ahFnfmVudm9sdmV0ZWNoLTAwMXIdCxIQQ2hhdFdpZGdldENvbmZpZxiAgIC898y2CQw";
```




## Plugin Code (THIS PART SHOULD NOT BE INCLUDED IN THE CONFIG - it is only an FYI)


``` javascript
AWIN.Tracking.Envolvetech = AWIN.Tracking.Envolvetech || {};
AWIN.Tracking.Envolvetech.url = AWIN.Tracking.Envolvetech.url || AWIN.sProtocol + "widget.envolvetech.com/static/js/app.js";
AWIN.Tracking.Envolvetech.dataBackend = AWIN.Tracking.Envolvetech.dataBackend || AWIN.sProtocol + "bot-dot-envolvetech-001.appspot.com";

(function ($e) {
    if (typeof $e.dataIdentifier === "undefined"){
        return;
    }

    AWIN.Tracking.scriptAppend(
        $e.url,
        false,
        false,
        {"data-identifier": $e.dataIdentifier, "data-backend": $e.dataBackend}
    );
})(AWIN.Tracking.Envolvetech);
```


