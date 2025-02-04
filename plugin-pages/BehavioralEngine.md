
# Supported Pages

- Product
- Checkout
- Basket
- Category

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

Accepted pagetype values are product, checkout, basket, category.

Basket page requires Product Level Tracking (Awin basket) to be
implemented on merchant's website.

## Page Configuration

``` javascript
AWIN.Tracking.BehavioralEngine = AWIN.Tracking.BehavioralEngine || {};
AWIN.Tracking.BehavioralEngine.token = "TOKEN_ID";
AWIN.Tracking.BehavioralEngine.pagetype = "PAGE_TYPE";
AWIN.Tracking.BehavioralEngine.href = "URL";
```



# Relevant Tickets

[PROD-3277](https://jira.awin.com/browse/PROD-3277)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/behavioralEngine.js)