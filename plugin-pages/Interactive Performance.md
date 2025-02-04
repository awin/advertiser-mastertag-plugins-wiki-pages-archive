# Supported Pages

- Generic (on all pages)
- Category
- Product
- Basket
- Transaction
- Thank you

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

`CAT_ID` and `TOKEN` should be provided by the partner. Note: do not
mistake CAT_ID for category id.

## Generic Configuration

``` javascript
AWIN.Tracking.InteractivePerformance = AWIN.Tracking.InteractivePerformance || {};
AWIN.Tracking.InteractivePerformance.token = "TOKEN";
AWIN.Tracking.InteractivePerformance.pageType = "generic";
```



## Category Page Configuration

``` javascript
AWIN.Tracking.InteractivePerformance = AWIN.Tracking.InteractivePerformance || {};
AWIN.Tracking.InteractivePerformance.pageType = "category";
AWIN.Tracking.InteractivePerformance.token = "TOKEN";
AWIN.Tracking.InteractivePerformance.categoryId = "CATEGORY ID";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.InteractivePerformance = AWIN.Tracking.InteractivePerformance || {};
AWIN.Tracking.InteractivePerformance.pageType = "product";
AWIN.Tracking.InteractivePerformance.token = "TOKEN";
AWIN.Tracking.InteractivePerformance.categoryId = "CATEGORY ID";
AWIN.Tracking.InteractivePerformance.catId = "CAT_ID";
AWIN.Tracking.InteractivePerformance.productId = "PRODUCT ID";
```



## Basket Page Configuration

``` javascript
AWIN.Tracking.InteractivePerformance = AWIN.Tracking.InteractivePerformance || {};
AWIN.Tracking.InteractivePerformance.pageType = "basket";
AWIN.Tracking.InteractivePerformance.token = "TOKEN";
AWIN.Tracking.InteractivePerformance.categoryId = "CATEGORY ID";
AWIN.Tracking.InteractivePerformance.catId = "CAT_ID";
```


The plugin will take the product data from the zx_products array.

``` javascript
for (var i = 0; i < dataLayer[0].cartContent.items.length; i++) {
    var o = {};
    o.identifier = dataLayer[0].cartContent.items[i].item_id;
    o.quantity = dataLayer[0].cartContent.items[i].quantity;
    zx_products.push(o);
}
```



## Transaction Page Configuration

This is the order confirmation page (the equivalent of the "checkout"
page for other plugins).

``` javascript
AWIN.Tracking.InteractivePerformance = AWIN.Tracking.InteractivePerformance || {};
AWIN.Tracking.InteractivePerformance.pageType = "transaction";
AWIN.Tracking.InteractivePerformance.token = "TOKEN";
AWIN.Tracking.InteractivePerformance.categoryId = "CATEGORY ID";
AWIN.Tracking.InteractivePerformance.catId = "CAT_ID";
```



The plugin will automatically take the product data from PLT if this is
implemented, otherwise it will use the zx_products array.

``` javascript
for (var i = 0; i < dataLayer[0].checkout.items.length; i++) {
    var o = {};
    o.identifier = dataLayer[0].checkout.items[i].item_id;
    o.quantity = dataLayer[0].checkout.items[i].quantity;
    zx_products.push(o);
}
```



## Thank You Page Configuration

This page is the first page after the confirmation page.

``` javascript
AWIN.Tracking.InteractivePerformance = AWIN.Tracking.InteractivePerformance || {};
AWIN.Tracking.InteractivePerformance.pageType = "thankYou";
AWIN.Tracking.InteractivePerformance.token = "TOKEN";
```



# Relevant Tickets

[PROD-8189](https://jira.awin.com/browse/PROD-8189)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/interactivePerformance/plugin.js)