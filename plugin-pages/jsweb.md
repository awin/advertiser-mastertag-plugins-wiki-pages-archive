# Supported Pages

- Product Page
- Category Page
- Search Page
- Basket Page
- Checkout Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Product Page Configuration

``` javascript
AWIN.Tracking.jsweb = AWIN.Tracking.jsweb || {};
AWIN.Tracking.jsweb.pagetype = "product";
AWIN.Tracking.jsweb.token = "TOKEN";
AWIN.Tracking.jsweb.name = "NAME";
AWIN.Tracking.jsweb.identifier = "PRODUCT_IDENTIFIER";
```



## Category Page Configuration

``` javascript
AWIN.Tracking.jsweb = AWIN.Tracking.jsweb || {};
AWIN.Tracking.jsweb.pagetype = "category";
AWIN.Tracking.jsweb.token = "TOKEN";
AWIN.Tracking.jsweb.category = "CATEGORY";
```



## Search Page Configuration

``` javascript
AWIN.Tracking.jsweb = AWIN.Tracking.jsweb || {};
AWIN.Tracking.jsweb.pagetype = "search";
AWIN.Tracking.jsweb.token = "TOKEN";
AWIN.Tracking.jsweb.identifier = "IDENTIFIER";
```



## Basket Page Configuration

``` javascript
AWIN.Tracking.jsweb = AWIN.Tracking.jsweb || {};
AWIN.Tracking.jsweb.pagetype = "addtocart";
AWIN.Tracking.jsweb.token = "TOKEN";
```



## Checkout Page Configuration

``` javascript
AWIN.Tracking.jsweb = AWIN.Tracking.jsweb || {};
AWIN.Tracking.jsweb.pagetype = "conversion";
AWIN.Tracking.jsweb.token = "TOKEN";
AWIN.Tracking.jsweb.lead_id = "LEAD_ID" || "";
AWIN.Tracking.jsweb.email = "EMAIL" || "";
```



# Relevant Tickets

[PROD-6049](https://jira.awin.com/browse/PROD-6049)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/jsweb/plugin.js)