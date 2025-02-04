
# Requirements

Advertiser MasterTag must to be displayed on all page unconditionally.

The advertiser must make available in the dataLayer the following:

- page type identifier (i.e. category, product, basket, etc)
- product data (i.e. id, price, etc)

**Note**: If the advertiser has PLT implemented, then the plugin will
take the product data from here automatically the "checkout" page, in
this case please do not configure anything for this page. Alternatively,
the usual configuration using `zx_products` should be implemented.

# Plugin setup code

Property `TOKEN` should be provided by the partner.

The placeholder strings in capital letters (e.g. `TOKEN`, `PRODUCT_ID`)
should be replaced by the genuine values.

The UIM plugin supports the following `PAGETYPE`: checkout, basket,
product, category.

The code below goes into *Awin UI \> Toolbox \> Advertiser MasterTag \>
My Plug-ins \> Set-up* (please select plugin name *United Interent
Media*).

## Category Page


``` javascript
AWIN.Tracking.uim = AWIN.Tracking.uim || {};
AWIN.Tracking.uim.token = "TOKEN";
AWIN.Tracking.uim.pagetype = "category";
AWIN.Tracking.uim.category = "CATEGORY_NAME";
```


## Product Page


``` javascript
AWIN.Tracking.uim = AWIN.Tracking.uim || {};
AWIN.Tracking.uim.token = "TOKEN";
AWIN.Tracking.uim.pagetype = "product";
AWIN.Tracking.uim.currency = "CURRENCY_CODE";
AWIN.Tracking.uim.identifier = "PRODUCT_ID";
```


## Basket Page


``` javascript
AWIN.Tracking.uim = AWIN.Tracking.uim || {};
AWIN.Tracking.uim.token = "TOKEN";
AWIN.Tracking.uim.pagetype = "basket";
AWIN.Tracking.uim.currency = "CURRENCY_CODE";
var zx_products = [];
for (dataLayer.basket.length) {
    zx_products.push(
        {
            'identifier' : "PRODUCT_ID",
            'price' : "PRODUCT_PRICE"
        });
}
```


## Checkout Page


``` javascript
AWIN.Tracking.uim = AWIN.Tracking.uim || {};
AWIN.Tracking.uim.token = "TOKEN";
AWIN.Tracking.uim.pagetype = "checkout";
AWIN.Tracking.Sale.currency = "CURRENCY";
var zx_products = [];
for (dataLayer.purchase.length) {
    zx_products.push(
        {
            'identifier' : "PRODUCT_ID",
            'price' : "PRODUCT_PRICE"
        });
}
```


# Example of Full Working Configuration


``` javascript
AWIN.Tracking.uim = AWIN.Tracking.uim || {};
AWIN.Tracking.uim.token = '18311';

if (dataLayer[0].pagePostType == 'product' && dataLayer[0].pagePostType2 == undefined) {
    AWIN.Tracking.uim.pagetype = 'category';
    AWIN.Tracking.uim.category = 'shop';
} else if (dataLayer[0].pagePostType2 == 'single-product') {
    AWIN.Tracking.uim.pagetype = 'product';
    AWIN.Tracking.uim.identifier = dataLayer[0].ecommerce.detail.products[0].id;
    AWIN.Tracking.uim.currency = 'EUR';
} else if (location.href.includes('/cart/')) {
    AWIN.Tracking.uim.pagetype = 'basket';
    AWIN.Tracking.uim.currency = 'EUR';
    var zx_products = [];
    for (var i = 0; i < dataLayer[0].cartContent.items.length; i++) {
        zx_products.push(
            {
                "identifier": dataLayer[0].cartContent.items[i].id,
                "price": dataLayer[0].cartContent.items[i].price
            });
    }
} else if (AWIN.Tracking.Sale) {
    AWIN.Tracking.uim.pagetype = 'checkout';
    var zx_products = [];
    for (var i = 0; i < dataLayer.filter(x => x.event == 'purchase')[0].ecommerce.items.length; i++) {
        zx_products.push(
            {
                "identifier": dataLayer.filter(x => x.event == 'purchase')[0].ecommerce.items[i].id,
                "price": dataLayer.filter(x => x.event == 'purchase')[0].ecommerce.items[i].price
            })
    }
}
```


# Relevant Tickets

[PROD-10570](https://jira.awin.com/browse/PROD-10570)
[PROD-10570](https://jira.awin.com/browse/SOLUTION-43983)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/unitedInternetMedia/plugin.js)