
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
AWIN.Tracking.MintSquare = AWIN.Tracking.MintSquare || {};
AWIN.Tracking.MintSquare.pagetype = "product";
AWIN.Tracking.MintSquare.token = "TOKEN";
AWIN.Tracking.MintSquare.identifier = "IDENTIFIER";
```




## Category Page Configuration


``` javascript
AWIN.Tracking.MintSquare = AWIN.Tracking.MintSquare || {};
AWIN.Tracking.MintSquare.pagetype = "category";
AWIN.Tracking.MintSquare.token = "TOKEN";
AWIN.Tracking.MintSquare.category = "CATEGORY";
```




## Search Page Configuration


``` javascript
AWIN.Tracking.MintSquare = AWIN.Tracking.MintSquare || {};
AWIN.Tracking.MintSquare.pagetype = "search";
AWIN.Tracking.MintSquare.token = "TOKEN";
```




## Basket Page Configuration


``` javascript
AWIN.Tracking.MintSquare = AWIN.Tracking.MintSquare || {};
AWIN.Tracking.MintSquare.pagetype = "basket";
AWIN.Tracking.MintSquare.token = "TOKEN";
```




## Checkout Page Configuration


``` javascript
AWIN.Tracking.MintSquare = AWIN.Tracking.MintSquare || {};
AWIN.Tracking.MintSquare.pagetype = "checkout";
AWIN.Tracking.MintSquare.token = "TOKEN";
```




## Related JIRA Ticket

[PROD-4698](https://jira.awin.com/browse/PROD-4698)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/miRetargeting.js)