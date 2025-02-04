# Supported Pages

- Generic Page
- Product Page
- Basket Page
- Confirmation Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Generic Page Configuration

``` javascript
AWIN.Tracking.VerizonMedia = AWIN.Tracking.VerizonMedia || {};
AWIN.Tracking.VerizonMedia.projectId = "PROJECT_ID";
AWIN.Tracking.VerizonMedia.pixelId = "PIXEL_ID";
```



## Basket Page Configuration

``` javascript
AWIN.Tracking.VerizonMedia = AWIN.Tracking.VerizonMedia || {};
AWIN.Tracking.VerizonMedia.pageType = "basket";
AWIN.Tracking.VerizonMedia.projectId = "PROJECT_ID";
AWIN.Tracking.VerizonMedia.pixelId = "PIXEL_ID";
AWIN.Tracking.VerizonMedia.productId = "PRODUCT_ID";

```



## Product Page Configuration

``` javascript
AWIN.Tracking.VerizonMedia = AWIN.Tracking.VerizonMedia || {};
AWIN.Tracking.VerizonMedia.pageType = "product";
AWIN.Tracking.VerizonMedia.projectId = "PROJECT_ID";
AWIN.Tracking.VerizonMedia.pixelId = "PIXEL_ID";
AWIN.Tracking.VerizonMedia.productId = "PRODUCT_ID";

```



## Confirmation Page Configuration

Confirmation page requires AWIN.Tracking.Sale object to be implemented
on merchant's website. Confirmation page requires Awin basket to be
implemented on merchant's website.

This page also allows for providing a comma separated product IDs via
AWIN.Tracking.VerizonMedia.productIds = "IDs". If this variable is not
provided, plugin will fetch product IDs from PLT. If neither option is
provided, plugin will not work.

``` javascript
AWIN.Tracking.VerizonMedia = AWIN.Tracking.VerizonMedia || {};
AWIN.Tracking.VerizonMedia.pageType = "confirmation";
AWIN.Tracking.VerizonMedia.projectId = "PROJECT_ID";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/verizonMedia/plugin.js)

# Relevant Ticket

[PROD-8866](https://jira.awin.com/browse/PROD-8866)