
# Supported Pages

- Category Page
- Checkout Page
- Basket Page
- Product Page
- Home Page
- Search Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## Basket & Checkout & Home & Search Page Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Basket & Checkout page requires Awin basket to be
implemented on merchant's website.

``` javascript
AWIN.Tracking.Vivalu = AWIN.Tracking.Vivalu || {};
AWIN.Tracking.Vivalu.containerId = "CONTAINER_ID";
AWIN.Tracking.Vivalu.pagetype = "PAGE_TYPE";
```



## Category Page Configuration

``` javascript
AWIN.Tracking.Vivalu = AWIN.Tracking.Vivalu || {};
AWIN.Tracking.Vivalu.containerId = "CONTAINER_ID";
AWIN.Tracking.Vivalu.category = "CATEGORY";
AWIN.Tracking.Vivalu.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.Vivalu = AWIN.Tracking.Vivalu || {};
AWIN.Tracking.Vivalu.containerId = "CONTAINER_ID";
AWIN.Tracking.Vivalu.identifier = "IDENTIFIER";
AWIN.Tracking.Vivalu.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/vivalu.js)