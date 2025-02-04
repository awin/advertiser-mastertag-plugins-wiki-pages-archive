
# How is the tag implemented?

**If the advertiser is using GTM, then the best thing to do is to set a
History Change trigger for the Awin Journey tag, and avoid using this
plugin. How to set a History Change trigger:**
<https://awin.atlassian.net/wiki/spaces/SOL/pages/246746742/Mastertag+integration+in+SPA+using+Google+Tag+Manager>

This plugin was developed to be used for advertisers who are using a
Single Page Application (SPA) website. The issue with SPAs is that the
MasterTag is not re-fired when the user navigates through the website,
and therefore any 3rd party partner plugins are not fired either.

The plugin will re-append the MasterTag to the HTML document whenever
the URL changes. If the URL does not change, then this plugin will NOT
work.

What is a SPA: <https://en.wikipedia.org/wiki/Single-page_application>

**NOTES:**

- This plugin uses the pushState function of the History interface. If
  the advertiser is already using this function somwhere on their SPA,
  then this plugin should **NOT** be used.
- You should inform the client of the following consequences of enabling
  this plugin. Enabling this plugin means that the MT will be appended
  on the website after each user click, this will result in multiple MTs
  appended for each user journey, which might result in decrease in
  performance, and some clients might not be happy about it.

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

**NOTE**: We've had issue with this plugin, therefore, the
***limitedRun=false*** parameter should be added as a temp fix to allow
the SPA plugin to reload the tag, until a permanent fix is implemented,
as per [PROD-10734](https://awin.atlassian.net/browse/PROD-10734)


``` javascript
AWIN.Tracking.SPAReload = AWIN.Tracking.SPAReload || {};
AWIN.Tracking.SPAReload.limitedRun = false; //always add
```


------------------------------------------------------------------------

# Additional Functionality

The plugin should work just with the setup specified above, however,
there are some cases where it might require additional configuration to
work correctly.

Therefore, if necessary, the plugin supports the following 2 additional
parameters:

- ***merchantId*** : for cases where the merchant id in the MasterTag
  being fired on the website is different than the accounts' merchant id
- ***timeout*** : this allows adding some additional delay in
  re-appending of the MasterTag. The unit is milliseconds, so if you
  want to add a 2 seconds delay, then use the value "2000". This
  parameter is useful for cases where the data is not loaded onto the
  dataLayer at the time when the MasterTag is loaded, and adding some
  delay to allow it to load is necessary.

### Example


``` javascript
AWIN.Tracking.SPAReload = AWIN.Tracking.SPAReload || {};
AWIN.Tracking.SPAReload.merchantId = 1001;
AWIN.Tracking.SPAReload.timeout = 2000;
AWIN.Tracking.SPAReload.limitedRun = false; //always add
```


- ***Plug in is currently worked on by the Production team for a
  permanent fix
  [PROD-10734](https://awin.atlassian.net/browse/PROD-10734)***