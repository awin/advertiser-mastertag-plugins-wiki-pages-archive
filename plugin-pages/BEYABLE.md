
# Requirements

- MasterTag must be displayed across all pages in the shop
- javascript based tracking code (Conversion Tag) must be loaded
  unconditionally on the order confirmation page.
- Plugin requires Product Level Tracking implemented on the checkout
  success page OR any alternative dataLayer.



# Configuration

Plugin supports following `pageType`: home, category, product,
shippinginfo, basket, checkout

The code below goes into *Awin UI \> Toolbox \> Advertiser MasterTag \>
My Plug-ins \> Set-up* (please select plugin name *Beyable*).



## Config code

Replace `"CLIENT_KEY"` with the identifier provided by the publisher.

Necessary properties to be set: clientKey


``` javascript

AWIN.Tracking.Beyable = AWIN.Tracking.Beyable || {};
AWIN.Tracking.Beyable.clientKey = 'CLIENT_KEY';
```


## Home page

Necessary properties to be set: pageType


``` javascript

AWIN.Tracking.Beyable.pageType = 'home';
```


## Category page

Necessary properties to be set: pageType, category name

Replace placeholder surrounded by angular brackets (`<>`) with it's real
value scraped from advertiser's website.


``` javascript

AWIN.Tracking.Beyable.pageType = 'category';
AWIN.Tracking.Beyable.category= '<PRODUCT_CATEGORY>';
```


## Product page

Necessary properties to be set: pageType, product id, product category,
product name, product price

Replace placeholder surrounded by angular brackets (`<>`) with it's real
value scraped from advertiser's website.


``` javascript

AWIN.Tracking.Beyable.pageType = 'product';
AWIN.Tracking.Beyable.identifier = '<PRODUCT_ID>';
AWIN.Tracking.Beyable.category = '<CATEGORY_NAME>';
AWIN.Tracking.Beyable.productName = '<PRODUCT_NAME>';
AWIN.Tracking.Beyable.productPrice = '<PROUCT_PRICE>';
```


## Shipping Details page

Necessary properties to be set: pageType

Replace placeholder surrounded by angular brackets (`<>`) with it's real
value scraped from advertiser's website.


``` javascript

AWIN.Tracking.Beyable.pageType = 'shippinginfo';
```


## Basket page

Necessary properties to be set: pageType

The plugin will look for product data in the "zx_products" array.

Replace placeholder surrounded by angular brackets (`<>`) with it's real
value scraped from advertiser's website.


``` javascript

AWIN.Tracking.Beyable.pageType = 'basket';
    var zx_products = [];
    for (var i = 0; i < dataLayer[0].cartContent.items.length; i++) {
        var o = {};
        o.identifier = '<PRODUCT_ID>';
        o.quantity = '<PRODUCT_QUANTITY>';
        o.price = '<PROUCT_PRICE>';
        o.name = '<PRODUCT_NAME>';
        zx_products.push(o);
    }
```


## Checkout page

Necessary properties to be set: pageType

IF PLT is implemented the plugin will look for the product ids in the
PLT object, else the plugin will look for product ids in the
"zx_products" array.

Replace placeholder surrounded by angular brackets (`<>`) with it's real
value scraped from advertiser's website.


``` javascript

AWIN.Tracking.Beyable.pageType = 'checkout';
    var zx_products = [];
    for (var i = 0; i < dataLayer[0].cartContent.items.length; i++) {
        var o = {};
        o.identifier = '<PRODUCT_ID>';
        o.quantity = '<PRODUCT_QUANTITY>';
        o.price = '<PROUCT_PRICE>';
        o.name = '<PRODUCT_NAME>';
        zx_products.push(o);
    }
```


# Configuration Example


``` javascript

AWIN.Tracking.Beyable = AWIN.Tracking.Beyable || {};
AWIN.Tracking.Beyable.clientKey = 'a8a2a1234afda3f8dd1e1b45e15321d0411161c374017e';


if (dataLayer[0].pagePostType == 'frontpage') {
    AWIN.Tracking.Beyable.pageType = 'home';
} else if (dataLayer[0].pagePostType == 'product' && dataLayer[0].pagePostType2 == undefined) {
    AWIN.Tracking.Beyable.pageType = 'category';
    AWIN.Tracking.Beyable.category = 'shop';
} else if (dataLayer[0].pagePostType2 == 'single-product') {
    AWIN.Tracking.Beyable.pageType = 'product';
    AWIN.Tracking.Beyable.identifier = dataLayer[0].ecommerce.detail.products[0].id;
    AWIN.Tracking.Beyable.category = 'shop';
    AWIN.Tracking.Beyable.name = dataLayer[0].ecommerce.detail.products[0].name;
    AWIN.Tracking.Beyable.price = dataLayer[0].ecommerce.detail.products[0].price;
} else if (dataLayer[0].pagePostType2 == 'shiping-details') {
    AWIN.Tracking.Beyable.pageType = 'shippinginfo';
} else if (location.href.includes('/cart/')) {
    AWIN.Tracking.Beyable.pageType = 'basket';
    var zx_products = [];
    for (var i = 0; i < dataLayer[0].cartContent.items.length; i++) {
        var o = {};
        o.identifier = dataLayer[0].cartContent.items[i].id;
        o.quantity = dataLayer[0].cartContent.items[i].quantity;
        o.price = dataLayer[0].cartContent.items[i].price;
        o.name = dataLayer[0].cartContent.items[i].name;
        zx_products.push(o);
    }

} else if (AWIN.Tracking.Sale) {
    AWIN.Tracking.Beyable.pageType = 'checkout';
    var zx_products = [];
    for (var i = 0; i < dataLayer[2].ecommerce.items.length; i++) {
        var o = {};
        o.identifier = dataLayer[2].ecommerce.items[i].id;
        o.quantity = dataLayer[2].ecommerce.items[i].quantity;
        o.price = dataLayer[2].ecommerce.items[i].price;
        o.name = dataLayer[2].ecommerce.items[i].name;
        zx_products.push(o);
    }
}
```


# Relevant Tickets

[PROD-10969](https://awin.atlassian.net/browse/PROD-10969)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/beyable/plugin.js)