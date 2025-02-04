
# Supported Pages

- Home
- Product
- Search
- Generic
- Basket
- Checkout
- Category

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Page type accepts the following values: home, product, search, generic,
basket, checkout, category.

## Generic Page Configuration

``` javascript
AWIN.Tracking.BigBangDatav2 = AWIN.Tracking.BigBangDatav2 || {};
AWIN.Tracking.BigBangDatav2.token = "TOKEN_ID";
AWIN.Tracking.BigBangDatav2.pagetype = "PAGE_TYPE_VALUE";
```



# Relevant Tickets

[PROD-5183](https://jira.awin.com/browse/PROD-5183)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/bigBangDataV2.js)