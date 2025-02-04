
# Supported Pages

- Product Page
- Basket Page
- Checkout Page
- Category Page

# Configuration

Plugin supports Zanox parameters. Refer to the source code for more
details.

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Product Page Configuration


``` javascript
AWIN.Tracking.Oliro = AWIN.Tracking.Oliro || {};
AWIN.Tracking.Oliro.containerId = "CONTAINER_ID";
AWIN.Tracking.Oliro.pagetype = "product";
```




## Basket Page Configuration


``` javascript
AWIN.Tracking.Oliro = AWIN.Tracking.Oliro || {};
AWIN.Tracking.Oliro.containerId = "CONTAINER_ID";
AWIN.Tracking.Oliro.pagetype = "basket";
```




## Checkout Page Configuration


``` javascript
AWIN.Tracking.Oliro = AWIN.Tracking.Oliro || {};
AWIN.Tracking.Oliro.containerId = "CONTAINER_ID";
AWIN.Tracking.Oliro.pagetype = "checkout";
```




## Category Page Configuration


``` javascript
AWIN.Tracking.Oliro = AWIN.Tracking.Oliro || {};
AWIN.Tracking.Oliro.containerId = "CONTAINER_ID";
AWIN.Tracking.Oliro.pagetype = "category";
AWIN.Tracking.Oliro.category = "CATEGORY_ID";
```




## Related JIRA Ticket

[PROD-3208](https://jira.awin.com/browse/PROD-3208)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/oliro.js)