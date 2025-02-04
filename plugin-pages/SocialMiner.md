
**NOTE: This plugin failed to meet our minimum security requirements and
should not be used anymore.** Reference:
<https://jira.awin.com/browse/SOLUTION-26450>

# Supported Pages

- Home Page
- Product Page
- Checkout Page
- Basket Page
- Category Page
- Search Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## All Pages Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.SocialMiner = AWIN.Tracking.SocialMiner || {};
AWIN.Tracking.SocialMiner.customerId = "CUSTOMER_ID";
AWIN.Tracking.SocialMiner.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/socialMiner.js)