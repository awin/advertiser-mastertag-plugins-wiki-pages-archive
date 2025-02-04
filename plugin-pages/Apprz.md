
# Supported Pages

- Product Page
- Checkout Page
- Cart/Basket page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to plugin source code for more
details.

Product and basket page require Product Level Tracking to be enabled.

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website.

## Page Configuration

``` javascript
AWIN.Tracking.Apprz = AWIN.Tracking.Apprz || {};
AWIN.Tracking.Apprz.merchantId = "MERCHANT_ID";
```



# Relevant Tickets

[PROD-4549](https://jira.awin.com/browse/PROD-4549)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/apprz.js)