# Description

Share A Sale plugins work together to append click ID to Share A Sale's
tracking calls. Share A Sale Cookie setter stores click ID in a cookie,
whereas Share A Sale Click Provider appends click ID to the tracking
call and appends it to the DOM.

Share A Sale Click ID provider plugin reads data from a cookie,
therefore does not require additional configuration.

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Share A Sale Cookie Setter Plugin Configuration

Cookie setter requires urlParameter name to be provided. The plugin will
search for click ID in the url with the provided name.

``` javascript
AWIN.Tracking.ShareASaleCookieSetter = AWIN.Tracking.ShareASaleCookieSetter || {};
AWIN.Tracking.ShareASaleCookieSetter.paramName = "PARAMETER_NAME";
```



# Relevant Tickets

[PROD-8276](https://jira.awin.com/browse/PROD-8276)

# Plugin Source Code

[View on GitHub
(shareASaleClickProvider)](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/shareASaleClickProvider/plugin.js)
[View on GitHub
(shareASaleCookieSetter)](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/shareASaleCookieSetter/plugin.js)