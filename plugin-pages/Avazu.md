
# Supported Pages

- Home Page
- Product Page
- Category Page
- Checkout Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## Home Page Configuration

``` javascript
AWIN.Tracking.Avazu = AWIN.Tracking.Avazu || {};
AWIN.Tracking.Avazu.runId = "RUN_ID";
AWIN.Tracking.Avazu.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Avazu.checkoutCode = "CHECKOUT_CODE";
AWIN.Tracking.Avazu.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.Avazu = AWIN.Tracking.Avazu || {};
AWIN.Tracking.Avazu.runId = "RUN_ID";
AWIN.Tracking.Avazu.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Avazu.checkoutCode = "CHECKOUT_CODE";
AWIN.Tracking.Avazu.pagetype = "PAGE_TYPE";
AWIN.Tracking.Avazu.detailUrl = "DETAIL_URL";
AWIN.Tracking.Avazu.category = "CATEGORY";
AWIN.Tracking.Avazu.categoryImage = "CATEGORY_IMAGE";
AWIN.Tracking.Avazu.identifier = "IDENTIFIER";
AWIN.Tracking.Avazu.productName = "PRODUCT_NAME";
AWIN.Tracking.Avazu.price = "PRICE";
AWIN.Tracking.Avazu.currency = "CURRENCY";
AWIN.Tracking.Avazu.imageUrl = "IMAGE_URL";
AWIN.Tracking.Avazu.description = "DESCRIPTION";
```



## Category Page Configuration

``` javascript
AWIN.Tracking.Avazu = AWIN.Tracking.Avazu || {};
AWIN.Tracking.Avazu.runId = "RUN_ID";
AWIN.Tracking.Avazu.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Avazu.checkoutCode = "CHECKOUT_CODE";
AWIN.Tracking.Avazu.pagetype = "PAGE_TYPE";
AWIN.Tracking.Avazu.categoryImage = "CATEGORY_IMAGE";
AWIN.Tracking.Avazu.category = "CATEGORY";
```



## Checkout Page Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.Avazu = AWIN.Tracking.Avazu || {};
AWIN.Tracking.Avazu.runId = "RUN_ID";
AWIN.Tracking.Avazu.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.Avazu.checkoutCode = "CHECKOUT_CODE";
AWIN.Tracking.Avazu.pagetype = "PAGE_TYPE";
```



# Relevant Tickets

[PROD-3163](https://jira.awin.com/browse/PROD-3163)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/avazu.js)