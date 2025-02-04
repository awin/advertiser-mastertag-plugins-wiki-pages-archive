# Description

Please bear in mind the partner has another plugin meant for Display
activities and verify beforehand which one to use.
Before activating this plugin, please reach out to Technical Solutions
team, in order to verify together with partner if the plugin code is
loaded correctly in test shop. **Background:** shortly after plugin has
been created, partner decided to stop all Email activities, however is
open to start campaign in the future.
=Requirements= Plugin requires mastertag implemented on product pages
and javascript based tracking tag on the confirmation page. Plugin
requires Product Level Tracking on the checkout page and supports
zx_products array (containing identifier, amount, quantity)
=Supported Pages=

- product
- checkout

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.


== Configuration Example ==

``` javascript
AWIN.Tracking.Euvic360EcomEmail = AWIN.Tracking.Euvic360EcomEmail || {};
AWIN.Tracking.Euvic360EcomEmail.sid= "sid"; // campaign identifier supplied by the provider
if (condition) { // identify page type product
    AWIN.Tracking.Euvic360EcomEmail.pagetype = "product";
} else if (AWIN.Tracking.Sale) {
    var zx_products = [{"identifier":"PRODUCT_ID","amount":"AMOUNT","quantity":"QUANTITY"}];

}
```


= Relevant Tickets =

[PROD-10308](https://jira.awin.com/browse/PROD-10308)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/euvic360EcomEmail/plugin.js)