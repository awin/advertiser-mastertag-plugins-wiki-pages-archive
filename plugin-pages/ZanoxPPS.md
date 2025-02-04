
# Supported Pages

- Generic Page
- Checkout Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## Checkout Page Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.ZanoxPPS = AWIN.Tracking.ZanoxPPS || {};
AWIN.Tracking.ZanoxPPS.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.ZanoxPPS.cid = "CID";
AWIN.Tracking.ZanoxPPS.customerID = "CUSTOMER_ID";
AWIN.Tracking.ZanoxPPS.partnerID = "PARTNER_ID";
AWIN.Tracking.ZanoxPPS.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/zanoxPPS.js)