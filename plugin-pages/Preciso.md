# Requirements

- MasterTag must be displayed across all pages in the shop
- javascript based tracking code (Conversion Tag) must be loaded
  unconditionally on the order confirmation page.
- Plugin requires Product Level Tracking implemented on the checkout
  success page OR any alternative dataLayer.



# Configuration

Plugin supports following PAGETYPE: home, category, product, basket,
checkout

## Config code

Replace `"TOKEN"` with the token provided by the publisher.

Necessary properties to be set: tokenId


``` javascript

AWIN.Tracking.Preciso = AWIN.Tracking.Preciso || {};
AWIN.Tracking.Preciso.tokenId = 'TOKEN';
```


## Home page

Necessary properties to be set: pagetype


``` javascript

AWIN.Tracking.Preciso.pagetype = 'home';
```


## Category page

Necessary properties to be set: pagetype, category name

Replace placeholder surrounded by angular brackets (`<>`) with it's real
value scraped from advertiser's website.


``` javascript

AWIN.Tracking.Preciso.pagetype = 'category';
AWIN.Tracking.Preciso.category= '<PRODUCT_CATEGORY>';
```


## Product page

Necessary properties to be set: pagetype, product id, product category,
product name, product price, currency (hard-coded)

Replace placeholder surrounded by angular brackets (`<>`) with it's real
value scraped from advertiser's website.


``` javascript

AWIN.Tracking.Preciso.pagetype = 'product';
AWIN.Tracking.Preciso.identifier = '<PRODUCT_ID>';
AWIN.Tracking.Preciso.category = '<CATEGORY_NAME>';
AWIN.Tracking.Preciso.productName = '<PRODUCT_NAME>';
AWIN.Tracking.Preciso.productPrice = '<PROUCT_PRICE>';
AWIN.Tracking.Preciso.currency = 'EUR';
```


## Basket page

Necessary properties to be set: pagetype

The plugin will look for product ids in the "zx_products" array.

Replace placeholder surrounded by angular brackets (`<>`) with it's real
value scraped from advertiser's website.


``` javascript

AWIN.Tracking.Preciso.pagetype = 'basket';
    var zx_products = [];
    for (var i = 0; i < dataLayer[0].cartContent.items.length; i++) {
        zx_products.push('<PRODUCT_ID>');
    }
```


## Checkout page

Necessary properties to be set: pagetype

IF PLT is implemented the plugin will look for the product ids in the
PLT object, else the plugin will look for product ids in the
"zx_products" array.

Replace placeholder surrounded by angular brackets (`<>`) with it's real
value scraped from advertiser's website.


``` javascript

AWIN.Tracking.Preciso.pagetype = 'checkout';
    var zx_products = [];
    for (var i = 0; i < dataLayer.filter(x => x.event == 'purchase')[0].ecommerce.items.length; i++) {
        zx_products.push('<PRODUCT_ID>')
    }
```


# Configuration Example

Replace `"TOKEN"` with the token provided by the publisher.


``` javascript

AWIN.Tracking.Preciso = AWIN.Tracking.Preciso || {};
AWIN.Tracking.Preciso.tokenId = 'TOKEN';

if (dataLayer[0].pagePostType == 'frontpage') {
    AWIN.Tracking.Preciso.pagetype = 'home';
} else if (dataLayer[0].pagePostType == 'product' && dataLayer[0].pagePostType2 == undefined) {
    AWIN.Tracking.Preciso.pagetype = 'category';
    AWIN.Tracking.Preciso.category = 'shop';
} else if (dataLayer[0].pagePostType2 == 'single-product') {
    AWIN.Tracking.Preciso.pagetype = 'product';
    AWIN.Tracking.Preciso.identifier = dataLayer[0].ecommerce.detail.products[0].id;
    AWIN.Tracking.Preciso.category = 'shop';
    AWIN.Tracking.Preciso.productName = dataLayer[0].ecommerce.detail.products[0].name;
    AWIN.Tracking.Preciso.productPrice = dataLayer[0].ecommerce.detail.products[0].price;
    AWIN.Tracking.Preciso.currency = 'EUR';
} else if (location.href.includes('/cart/')) {
    AWIN.Tracking.Preciso.pagetype = 'basket';
    var zx_products = [];
    for (var i = 0; i < dataLayer[0].cartContent.items.length; i++) {
        zx_products.push(dataLayer[0].cartContent.items[i].id);
    }
} else if (AWIN.Tracking.Sale) {
    AWIN.Tracking.Preciso.pagetype = 'checkout';
    var zx_products = [];
    for (var i = 0; i < dataLayer.filter(x => x.event == 'purchase')[0].ecommerce.items.length; i++) {
        zx_products.push(dataLayer.filter(x => x.event == 'purchase')[0].ecommerce.items[i].id)
    }
}
```


# Relevant Tickets

[PROD-10190](https://awin.atlassian.net/browse/PROD-10190)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/tree/master/src/plugins/thirdParty/preciso)