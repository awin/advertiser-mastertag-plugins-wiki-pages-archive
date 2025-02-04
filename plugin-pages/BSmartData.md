
# Supported Pages

- Home Page
- Generic Page
- Basket Page
- Product Page
- Category Page
- Checkout Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

Page type accepted values: generic, home, product, checkout, basket,
category.

## Home/Generic Page Configuration

``` javascript
AWIN.Tracking.BSmartData = AWIN.Tracking.BSmartData || {};
AWIN.Tracking.BSmartData.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.BSmartData.pagetype = "PAGE_TYPE";
```



## Basket Page Configuration

Plugin requires Product Level Tracking (Awin basket) to be implemented
on merchant's website containing products basket.

``` javascript
AWIN.Tracking.BSmartData = AWIN.Tracking.BSmartData || {};
AWIN.Tracking.BSmartData.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.BSmartData.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.BSmartData = AWIN.Tracking.BSmartData || {};
AWIN.Tracking.BSmartData.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.BSmartData.pagetype = "PAGE_TYPE";
AWIN.Tracking.BSmartData.identifier = "IDENTIFIER";
```



## Category Page Configuration

``` javascript
AWIN.Tracking.BSmartData = AWIN.Tracking.BSmartData || {};
AWIN.Tracking.BSmartData.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.BSmartData.pagetype = "PAGE_TYPE";
AWIN.Tracking.BSmartData.category = "CATEGORY";
```



## Checkout Page Configuration

Plugin requires AWIN.Tracking.Sale object to be implemented on
merchant's checkout page.

``` javascript
AWIN.Tracking.BSmartData = AWIN.Tracking.BSmartData || {};
AWIN.Tracking.BSmartData.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.BSmartData.pagetype = "PAGE_TYPE";
```



# Relevant Tickets

[PROD-5405](https://jira.awin.com/browse/PROD-5405)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/bSmartData/plugin.js)