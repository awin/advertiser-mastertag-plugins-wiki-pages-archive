# Supported Pages

- Home Page
- Product Page
- Checkout Page
- Basket Page
- Category Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## Home Page Configuration

``` javascript
AWIN.Tracking.SmartBMC = AWIN.Tracking.SmartBMC || {};
AWIN.Tracking.SmartBMC.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.SmartBMC.pagetype = "PAGE_TYPE";
```



## Basket & Checkout

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.SmartBMC = AWIN.Tracking.SmartBMC || {};
AWIN.Tracking.SmartBMC.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.SmartBMC.pagetype = "PAGE_TYPE";
zx_products = ["PRODUCT_DATA"]; //id and quantity
```



## Category Page Configuration

``` javascript
AWIN.Tracking.SmartBMC = AWIN.Tracking.SmartBMC || {};
AWIN.Tracking.SmartBMC.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.SmartBMC.category = "CATEGORY";
AWIN.Tracking.SmartBMC.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.SmartBMC = AWIN.Tracking.SmartBMC || {};
AWIN.Tracking.SmartBMC.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.SmartBMC.identifier = "IDENTIFIER";
AWIN.Tracking.SmartBMC.pagetype = "PAGE_TYPE";
```



# Example Config


``` javascript
AWIN.Tracking.SmartBMC = AWIN.Tracking.SmartBMC || {};
AWIN.Tracking.SmartBMC.advertiserId = "lctb";
AWIN.Tracking.SmartBMC.pagetype = "home";

if (document.getElementsByClassName("page search-show").length > 0) {
   AWIN.Tracking.SmartBMC.pagetype = "category";
   AWIN.Tracking.SmartBMC.category = location.pathname.split("/").slice(-1)[0];
} else if (document.getElementsByClassName("page product-show").length > 0) {
   AWIN.Tracking.SmartBMC.pagetype = "product";
   AWIN.Tracking.SmartBMC.identifier = document.getElementsByClassName("page product-show")[0].dataset.querystring.split("=")[1];
} else if (document.getElementsByClassName("page cart-show").length > 0) {
   AWIN.Tracking.SmartBMC.pagetype = "basket";
   var zx_products = [];
   for (var i = 0; i < dataLayer.filter(function (x) { return x.event == "view_cart" })[0].ecommerce.items.length; i++) {
      var o = {};
      o.identifier = dataLayer.filter(function (x) { return x.event == "view_cart" })[0].ecommerce.items[i].id;
      o.quantity = dataLayer.filter(function (x) { return x.event == "view_cart" })[0].ecommerce.items[i].quantity;
      zx_products.push(o);
   }

} else if (AWIN.Tracking.Sale) {
  AWIN.Tracking.SmartBMC.pagetype = "checkout";
   var zx_products = [];
   for (var i = 0; i < dataLayer.filter(function (x) { return x.event == "checkout" })[0].ecommerce.items.length; i++) {
      var o = {};
      o.identifier = dataLayer.filter(function (x) { return x.event == "checkout" })[0].ecommerce.items[i].id;
      o.quantity = dataLayer.filter(function (x) { return x.event == "checkout" })[0].ecommerce.items[i].quantity;
      zx_products.push(o);
   }
}
```




# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/smartBmc/plugin.js)