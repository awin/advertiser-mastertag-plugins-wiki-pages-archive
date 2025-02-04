Supported Pages

- Checkout Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## Basket Page Configuration

Plugin requires Product Level Tracking to be implemented.

``` javascript
AWIN.Tracking.BlueCart = AWIN.Tracking.BlueCart || {};
AWIN.Tracking.BlueCart.basketId = "BASKET_ID";
AWIN.Tracking.BlueCart.pagetype = "PAGE_TYPE";
```



# Relevant Tickets

[PROD-3278](https://jira.awin.com/browse/PROD-3278)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/blueCart/plugin.js)