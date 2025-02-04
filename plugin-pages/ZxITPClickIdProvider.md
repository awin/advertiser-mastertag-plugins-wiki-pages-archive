
# Description

Zanox ITP plugins work together to append partner ID to Zanox tracking
calls. Zanox Cookie setter stores partner ID in a cookie, whereas Zanox
Click Provider appends partner ID to the tracking call.

Click provider ID reads data from a cookie, therefore does not require
additional configuration.

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Zanox Cookie Setter COnfiguration

Cookie setter requires urlParameter name to be provided. The plugin will
search for partner ID in the url with the provided name.

``` javascript
AWIN.Tracking.zxITPCookieSetter = AWIN.Tracking.zxITPCookieSetter || {};
AWIN.Tracking.zxITPCookieSetter.urlParameterName = "PARAMETER_NAME";
```



# Relevant Tickets

[PROD-6547](https://jira.awin.com/browse/PROD-6547)
[PROD-6548](https://jira.awin.com/browse/PROD-6548)

# Plugin Source Code

[View on GitHub (Zanox ITP Click
Provider)](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/zxITPClickIdProvider.js)
[View on GitHub (Zanox ITP Cookie
Setter)](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/zxITPCookieSetter.js)