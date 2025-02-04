
# Supported Pages

- Home Page
- Category Page
- Product Page
- Basket Page
- Checkout Page
- Search Page
- Generic Page

# Configuration

Plugin supports Zanox parameters. Refer to the source code for more
details.

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Home Page Configuration


``` javascript
AWIN.Tracking.Nano = AWIN.Tracking.Nano || {};
AWIN.Tracking.Nano.securityToken = "SECURITY_TOKEN";
AWIN.Tracking.Nano.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Nano.pagetype = "home";
```




## Category Page Configuration


``` javascript
AWIN.Tracking.Nano = AWIN.Tracking.Nano || {};
AWIN.Tracking.Nano.securityToken = "SECURITY_TOKEN";
AWIN.Tracking.Nano.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Nano.pagetype = "home";
AWIN.Tracking.Nano.category = "CATEGORY";
```




## Product Page Configuration


``` javascript
AWIN.Tracking.Nano = AWIN.Tracking.Nano || {};
AWIN.Tracking.Nano.securityToken = "SECURITY_TOKEN";
AWIN.Tracking.Nano.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Nano.pagetype = "product";
AWIN.Tracking.Nano.identifier = "IDENTIFIER";
```




## Basket Page Configuration


``` javascript
AWIN.Tracking.Nano = AWIN.Tracking.Nano || {};
AWIN.Tracking.Nano.securityToken = "SECURITY_TOKEN";
AWIN.Tracking.Nano.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Nano.pagetype = "basket";
AWIN.Tracking.Nano.products = <PRODUCTS>;
```




## Checkout Page Configuration


``` javascript
AWIN.Tracking.Nano = AWIN.Tracking.Nano || {};
AWIN.Tracking.Nano.securityToken = "SECURITY_TOKEN";
AWIN.Tracking.Nano.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Nano.pagetype = "checkout";
AWIN.Tracking.Nano.pixelId = "PIXEL_ID";
```




## Search Page Configuration


``` javascript
AWIN.Tracking.Nano = AWIN.Tracking.Nano || {};
AWIN.Tracking.Nano.securityToken = "SECURITY_TOKEN";
AWIN.Tracking.Nano.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Nano.pagetype = "search";
AWIN.Tracking.Nano.searchQuery = "SEARCH_QUERY";
```




## Generic Page Configuration


``` javascript
AWIN.Tracking.Nano = AWIN.Tracking.Nano || {};
AWIN.Tracking.Nano.securityToken = "SECURITY_TOKEN";
AWIN.Tracking.Nano.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Nano.pagetype = "generic";
```




## Related JIRA Ticket

[PROD-3249](https://jira.awin.com/browse/PROD-3249)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/nano.js)