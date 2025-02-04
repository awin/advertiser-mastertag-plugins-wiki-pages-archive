# Supported Pages

- Home Page
- Basket Page
- Product Page
- Category Page
- Checkout Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Home Page Configuration

``` javascript
AWIN.Tracking.JsWebProduction = AWIN.Tracking.JsWebProduction || {};
AWIN.Tracking.JsWebProduction.pagetype = "landing";
AWIN.Tracking.JsWebProduction.name = "BOUTIQUE_NAME";
```



## Basket Page Configuration

``` javascript
AWIN.Tracking.JsWebProduction = AWIN.Tracking.JsWebProduction || {};
AWIN.Tracking.JsWebProduction.pagetype = "addtocart";
AWIN.Tracking.JsWebProduction.name = "BOUTIQUE_NAME";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.JsWebProduction = AWIN.Tracking.JsWebProduction || {};
AWIN.Tracking.JsWebProduction.pagetype = "product";
AWIN.Tracking.JsWebProduction.name = "BOUTIQUE_NAME";
AWIN.Tracking.JsWebProduction.identifier = "PRODUCT_ID";
```



## Category Page Configuration

``` javascript
AWIN.Tracking.JsWebProduction = AWIN.Tracking.JsWebProduction || {};
AWIN.Tracking.JsWebProduction.pagetype = "product";
AWIN.Tracking.JsWebProduction.name = "BOUTIQUE_NAME";
AWIN.Tracking.JsWebProduction.category = "CATEGORY_ID";
```



## Checkout Page Configuration

``` javascript
AWIN.Tracking.JsWebProduction = AWIN.Tracking.JsWebProduction || {};
AWIN.Tracking.JsWebProduction.pagetype = "checkout";
AWIN.Tracking.JsWebProduction.name = "BOUTIQUE_NAME";
AWIN.Tracking.JsWebProduction.category = "CATEGORY_ID";
```



# Relevant Tickets

[PROD-6199](https://jira.awin.com/browse/PROD-6199)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/jsWebProduction/plugin.js)