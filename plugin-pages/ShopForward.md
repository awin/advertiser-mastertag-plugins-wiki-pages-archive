
# Requirements

Advertiser MasterTag must to be displayed on all page unconditionally.

The advertiser must make available on their website (dataLayer, HTML, or
URL) the following:

- page type identifier (i.e. category, product, basket, etc)
- product data (i.e. id, price, etc)

**NOTE:** On the `checkout` page the plugin will automatically get the
product data if the advertiser has PLT implemented, otherwise it will
look for it in the `zx_products` array. If the advertiser has PLT
implemented, then you should NOT add a configuration for the `checkout`
page.

# Plugin setup code

Property `TOKEN_ID` should be provided by the partner.

The ShopForward plugin supports the following `PAGETYPE`:
begin_checkout, checkout, basket, product, category, search, generic.

The code below goes into *Awin UI \> Toolbox \> Advertiser MasterTag \>
My Plug-ins \> Set-up* (please select plugin name *ShopForward*).

## Generic Page


``` javascript
AWIN.Tracking.ShopForward = AWIN.Tracking.ShopForward || {};
AWIN.Tracking.ShopForward.token = "TOKEN_ID";
AWIN.Tracking.ShopForward.pagetype = "generic";
```


## Category Page


``` javascript
AWIN.Tracking.ShopForward = AWIN.Tracking.ShopForward || {};
AWIN.Tracking.ShopForward.token = "TOKEN_ID";
AWIN.Tracking.ShopForward.pagetype = "category";
```


## Search Results Page


``` javascript
AWIN.Tracking.ShopForward = AWIN.Tracking.ShopForward || {};
AWIN.Tracking.ShopForward.token = "TOKEN_ID";
AWIN.Tracking.ShopForward.pagetype = "search";
```


## Product Page


``` javascript
AWIN.Tracking.ShopForward = AWIN.Tracking.ShopForward || {};
AWIN.Tracking.ShopForward.token = "TOKEN_ID";
AWIN.Tracking.ShopForward.pagetype = "product";
AWIN.Tracking.ShopForward.currency = "CURRENCY_CODE";
AWIN.Tracking.ShopForward.amount = "PRICE";
AWIN.Tracking.ShopForward.identifier = "PRODUCT_ID";
```


## Basket Page


``` javascript
AWIN.Tracking.ShopForward = AWIN.Tracking.ShopForward || {};
AWIN.Tracking.ShopForward.token = "TOKEN_ID";
AWIN.Tracking.ShopForward.pagetype = "basket";
AWIN.Tracking.ShopForward.currency = "CURRENCY_CODE";
var zx_products = [];
for (var i = 0; i < dataLayer[0].cartContent.items.length; i++) {
    zx_products.push(
        {
            'identifier' : dataLayer[0].cartContent.items[i].id,
            'quantity' : dataLayer[0].cartContent.items[i].quantity,
            'price' : dataLayer[0].cartContent.items[i].price
        });
}
```


## Checkout Page

**NOTE:** On this page the plugin will automatically get the product
data if the advertiser has PLT implemented, otherwise it will look for
it in the `zx_products` array. If the advertiser has PLT implemented,
then you should NOT add the configuration for this page.


``` javascript
//only configure if PLT is not implemented
AWIN.Tracking.ShopForward = AWIN.Tracking.ShopForward || {};
AWIN.Tracking.ShopForward.token = "TOKEN_ID";
AWIN.Tracking.ShopForward.pagetype = "checkout";
AWIN.Tracking.Sale.orderRef = "ORDER_REF";
AWIN.Tracking.Sale.currency = "CURRENCY";
var zx_products = [];
for (var i = 0; i < dataLayer[0].cartContent.items.length; i++) {
    zx_products.push(
        {
            'identifier' : dataLayer[0].cartContent.items[i].id,
            'quantity' : dataLayer[0].cartContent.items[i].quantity,
            'price' : dataLayer[0].cartContent.items[i].price
        });
}
```


## Begin Checkout Page


``` javascript
AWIN.Tracking.ShopForward = AWIN.Tracking.ShopForward || {};
AWIN.Tracking.ShopForward.token = "TOKEN_ID";
AWIN.Tracking.ShopForward.pagetype = "begin_checkout";
AWIN.Tracking.Sale.currency = "CURRENCY";
var zx_products = [];
for (var i = 0; i < dataLayer[0].cartContent.items.length; i++) {
    zx_products.push(
        {
            'identifier' : dataLayer[0].cartContent.items[i].id,
            'quantity' : dataLayer[0].cartContent.items[i].quantity,
            'price' : dataLayer[0].cartContent.items[i].price
        });
}
```


# Example of Full Configuration


``` javascript
AWIN.Tracking.ShopForward = AWIN.Tracking.ShopForward || {};
AWIN.Tracking.ShopForward.token = "AW-10822997408";
AWIN.Tracking.ShopForward.pagetype = "generic";

if (dataLayer[0].pagePostType == 'product' && dataLayer[0].pagePostType2 == undefined) {
    AWIN.Tracking.ShopForward.pagetype = 'category';
    AWIN.Tracking.ShopForward.category = 'shop';
} else if (dataLayer[0].pagePostType2 == 'single-product') {
    AWIN.Tracking.ShopForward.pagetype = 'product';
    AWIN.Tracking.ShopForward.identifier = dataLayer[0].ecommerce.detail.products[0].id;
    AWIN.Tracking.ShopForward.amount = dataLayer[0].ecommerce.detail.products[0].price;
    AWIN.Tracking.ShopForward.currency = 'EUR';
} else if (location.href.includes('/cart/')) {
    AWIN.Tracking.ShopForward.pagetype = 'basket';
    AWIN.Tracking.ShopForward.currency = 'EUR';
    var zx_products = [];
    for (var i = 0; i < dataLayer[0].cartContent.items.length; i++) {
        zx_products.push(
            {
                'identifier' : dataLayer[0].cartContent.items[i].id,
                'quantity' : dataLayer[0].cartContent.items[i].quantity,
                'price' : dataLayer[0].cartContent.items[i].price
            }

            );
    }
} else if (location.pathname.includes("/checkout/") && !location.pathname.includes("/order-received/")) {
    AWIN.Tracking.ShopForward.pagetype = 'begin_checkout';
    var zx_products = [];
    for (var i = 0; i < dataLayer.filter(x => x.event == 'begin_checkout')[0].ecommerce.items.length; i++) {
        zx_products.push(
            {
                'identifier' : dataLayer.filter(x => x.event == 'begin_checkout')[0].ecommerce.items[i].id,
                'quantity' : dataLayer.filter(x => x.event == 'begin_checkout')[0].ecommerce.items[i].quantity,
                'price' : dataLayer.filter(x => x.event == 'begin_checkout')[0].ecommerce.items[i].price
            }

            );
    }
//only configure if PLT is not implemented
} else if (AWIN.Tracking.Sale) {
    AWIN.Tracking.ShopForward.pagetype = 'checkout';
    AWIN.Tracking.ShopForward.currency = 'EUR';
    var zx_products = [];
    for (var i = 0; i < dataLayer.filter(x => x.event == 'purchase')[0].ecommerce.items.length; i++) {
        zx_products.push(
            {
                'identifier' : dataLayer.filter(x => x.event == 'purchase')[0].ecommerce.items[i].id,
                'quantity' : dataLayer.filter(x => x.event == 'purchase')[0].ecommerce.items[i].quantity,
                'price' : dataLayer.filter(x => x.event == 'purchase')[0].ecommerce.items[i].price
            }

            );
    }
}
//only use these statements for testing purposes
console.log("ShopForward Object: ", AWIN.Tracking.ShopForward);
if (typeof zx_products !== "undefined") {
    console.log("zx_products: ", zx_products);
}
```


# Relevant Tickets

[PROD-10468](https://jira.awin.com/browse/PROD-10468)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/shopForward/plugin.js)