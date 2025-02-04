# Supported Pages

- home
- product
- cart
- orderStarted (page where the user started creating the order - i.e.
  the next page after the basket page)
- checkout
- category (activate tag manager on this page type)

# Requirements

- Plugin requires AWIN mastertag implemented on all pages in the shop
  and javascript based tracking code on the confirmation page.
- On the product page the product ID should be the same as in the
  product feed.
- On the basket and checkout page plugin requires product details
  (identifier, amount, quantity) and supports Product Level Tracking or
  zx_products array.

# Configuration

- Plugin requires individual tracker for each page type and additional
  tokens (service, sid, cid, pid) to activate tag manager of the
  provider.
- Tag manager should be activated on category page where the partner
  will collect the list of categories.
- Additionally tag manager will be activated on pages where the Add to
  cart / remove from cart functionality is available on the website.

``` javascript
AWIN.Tracking.Euvic360ecomDisplay.tagManager = true; // activation of tag manager
```


Replace `"VALUE_PLACEHOLDERS"` with real values.

``` javascript
AWIN.Tracking.Euvic360ecomDisplay = AWIN.Tracking.Euvic360ecomDisplay || {};
AWIN.Tracking.Euvic360ecomDisplay.service = "SERVICE"; // service token for tag manager
AWIN.Tracking.Euvic360ecomDisplay.sid = "SID"; // sid token for tag manager
AWIN.Tracking.Euvic360ecomDisplay.cid = "CID"; // cid token for tag manager
AWIN.Tracking.Euvic360ecomDisplay.pid = "PID"; // pid token for tag manager

if (condition) {
    AWIN.Tracking.Euvic360ecomDisplay.pagetype = "home";
    AWIN.Tracking.Euvic360ecomDisplay.tracker = "TRACKER FOR PAGETYPE HOME";
} else if (condition) {
    AWIN.Tracking.Euvic360ecomDisplay.pagetype = "category";
        AWIN.Tracking.Euvic360ecomDisplay.tracker = "TRACKER FOR PAGETYPE CATEGORY";
    AWIN.Tracking.Euvic360ecomDisplay.tagManager = true; // activate tag manager
} else if (condition) {
    AWIN.Tracking.Euvic360ecomDisplay.pagetype = "product";
    AWIN.Tracking.Euvic360ecomDisplay.tracker = "TRACKER FOR PAGETYPE PRODUCT";
    AWIN.Tracking.Euvic360ecomDisplay.productId = "PRODUCT_ID"; // product id same as in the feed
    AWIN.Tracking.Euvic360ecomDisplay.productPrice = "PRODUCT_PRICE";
        AWIN.Tracking.Euvic360ecomDisplay.tagManager = true; // activate, if 'Add to basket' available
} else if (condition)) {
    AWIN.Tracking.Euvic360ecomDisplay.pagetype = "basket";
    AWIN.Tracking.Euvic360ecomDisplay.tracker = "TRACKER FOR PAGETYPE BASKET";
    var zx_products = [{"identifier":"PRODUCT_ID","amount":"AMOUNT","quantity":"QUANTITY"}];
} else if (condition) {
    AWIN.Tracking.Euvic360ecomDisplay.pagetype = "orderStarted";
    AWIN.Tracking.Euvic360ecomDisplay.tracker = "TRACKER FOR PAGE TYPE ORDER STARTED";
} else if (AWIN.Tracking.Sale) {
    AWIN.Tracking.Euvic360ecomDisplay.pagetype = "checkout";
    AWIN.Tracking.Euvic360ecomDisplay.tracker = "TRACKER FOR PAGETYPE CHECKOUT";
        var zx_products = [{"identifier":"PRODUCT_ID","amount":"AMOUNT","quantity":"QUANTITY"}];
}
```


== Configuration example ==

``` javascript
AWIN.Tracking.Euvic360ecomDisplay = AWIN.Tracking.Euvic360ecomDisplay || {};
AWIN.Tracking.Euvic360ecomDisplay.service = "8063";
AWIN.Tracking.Euvic360ecomDisplay.sid = "8063";
AWIN.Tracking.Euvic360ecomDisplay.cid = "178";
AWIN.Tracking.Euvic360ecomDisplay.pid = "18683";
if (dataLayer.filter(x => x.pageType == "homepage").length > 0) {
    AWIN.Tracking.Euvic360ecomDisplay.pagetype = "home";
    AWIN.Tracking.Euvic360ecomDisplay.tracker = "5351";
} else if (dataLayer.filter(x => x.pageType == "categoryPage").length > 0) {
    AWIN.Tracking.Euvic360ecomDisplay.pagetype = "category";
    AWIN.Tracking.Euvic360ecomDisplay.tracker = "5355";
    AWIN.Tracking.Euvic360ecomDisplay.tagManager = true;
} else if (dataLayer.filter(x => x.pageType == "productPage").length > 0) {
    AWIN.Tracking.Euvic360ecomDisplay.pagetype = "product";
    AWIN.Tracking.Euvic360ecomDisplay.tracker = "5352";
    AWIN.Tracking.Euvic360ecomDisplay.productId = dataLayer.filter(x => x.pageType == "productPage")[0].product.id;
    AWIN.Tracking.Euvic360ecomDisplay.productPrice = dataLayer.filter(x => x.pageType == "productPage")[0].product.price;
    AWIN.Tracking.Euvic360ecomDisplay.tagManager = true; // if 'Add to basket' button available
} else if (dataLayer.filter(x => x.pageType == "shoppingCart").length > 0) {
    AWIN.Tracking.Euvic360ecomDisplay.pagetype = "basket";
    AWIN.Tracking.Euvic360ecomDisplay.tracker = "5356";
    var zx_products = [];
    for (var i = 0; i < dataLayer.filter(x => x.pageType == "shoppingCart")[0].products.length; i++) {
        var o = {};
        o.identifier = dataLayer.filter(x => x.pageType == "shoppingCart")[0].products[i].id;
        o.amount = dataLayer.filter(x => x.pageType == "shoppingCart")[0].products[i].price;
        o.quantity = dataLayer.filter(x => x.pageType == "shoppingCart")[0].products[i].quantity;
        zx_products.push(o);
    }
} else if (location.href.includes("/checkout/onepage/")) {
    AWIN.Tracking.Euvic360ecomDisplay.pagetype = "orderStarted";
    AWIN.Tracking.Euvic360ecomDisplay.tracker = "5869";
} else if (AWIN.Tracking.Sale) {
    AWIN.Tracking.Euvic360ecomDisplay.pagetype = "checkout";
    AWIN.Tracking.Euvic360ecomDisplay.tracker = "5357";
    var zx_products = [];
    for (var i = 0; i < dataLayer.filter(x => x.pageType == "orderConfirmation")[0].transactionProducts.length; i++) {
        var o = {};
        o.identifier = dataLayer.filter(x => x.pageType == "orderConfirmation")[0].transactionProducts[i].id;
        o.amount = dataLayer.filter(x => x.pageType == "orderConfirmation")[0].transactionProducts[i].price;
        o.quantity = dataLayer.filter(x => x.pageType == "orderConfirmation")[0].transactionProducts[i].quantity;
        zx_products.push(o);
    }
}
```


= Relevant Tickets =

[PROD-10293](https://jira.awin.com/browse/PROD-10293)

# Plugin Source Code

[on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/euvic360ecomDisplay/plugin.js)