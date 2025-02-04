
Deprecated zanox plugin

# Supported Pages

- Home Page
- Product Page
- Checkout Page
- Category Page
- Basket Page
- Registration Page
- Search Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## All Pages Configuration

``` javascript
AWIN.Tracking.GDMDigital = AWIN.Tracking.GDMDigital || {};
AWIN.Tracking.GDMDigital.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.GDMDigital.retargetingOn = true;
AWIN.Tracking.GDMDigital.pixelType = "PIXEL_TYPE";
AWIN.Tracking.GDMDigital.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/gdmDigitalZanox/plugin.js)