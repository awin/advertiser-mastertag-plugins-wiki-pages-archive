# READ ME

Plugin is not supported on AWIN platform anymore. Reference:
[SOLUTION-41465](https://jira.awin.com/browse/SOLUTION-41465)

# Supported Pages

- Home Page
- Category Page
- Product Page
- Search Page
- Basket Page
- Checkout Page
- Generic Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Active Page Configuration

``` javascript
AWIN.Tracking.AdroxPixel = AWIN.Tracking.AdroxPixel || {};
AWIN.Tracking.AdroxPixel.advertiserId = "SPECIFIC_ADVERTISER_ID";
AWIN.Tracking.AdroxPixel.pagetype = "SPECIFIC_PAGETYPE";
```


Pagetype accepted values are: home, category, product, search, basket,
checkout, generic.

## Basket and Product Pages

Requires Product Level Tracking to be implemented on advertiser's
website.

## Checkout

Requires AWIN.Tracking.Sale object to be implemented on merchant's
website.

# Relevant Tickets

[PROD-3246](https://jira.awin.com/browse/PROD-3246)
[PROD-5943](https://jira.awin.com/browse/PROD-5943)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/adroxPixel/plugin.js)