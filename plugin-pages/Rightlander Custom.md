
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

The code below goes into *Awin UI \> Toolbox \> Advertiser MasterTag \>
My Plug-ins \> Set-up* (please select plugin name *Rightlander*).

## Generic Page


``` javascript
AWIN.Tracking.Rightlander = AWIN.Tracking.Rightlander || {};
AWIN.Tracking.Rightlander.pagetype = "generic";
```


## HomePage


``` javascript
AWIN.Tracking.Rightlander = AWIN.Tracking.Rightlander || {};
AWIN.Tracking.Rightlander.pagetype = "home";
```


## Category Page


``` javascript
AWIN.Tracking.Rightlander = AWIN.Tracking.Rightlander || {};
AWIN.Tracking.Rightlander.pagetype = "category";
```


## Product Page


``` javascript
AWIN.Tracking.Rightlander = AWIN.Tracking.Rightlander || {};
AWIN.Tracking.Rightlander.pagetype = "product";
AWIN.Tracking.Rightlander.identifier = "PRODUCT_ID";
```


## Basket Page


``` javascript
AWIN.Tracking.Rightlander = AWIN.Tracking.Rightlander || {};
AWIN.Tracking.Rightlander.pagetype = "basket";
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
AWIN.Tracking.Rightlander = AWIN.Tracking.Rightlander || {};
AWIN.Tracking.Rightlander.pagetype = "checkout";
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
AWIN.Tracking.Rightlander = AWIN.Tracking.Rightlander || {};

if (location.pathname == "/") {
    AWIN.Tracking.Rightlander.pagetype = "home";
}else if (dataLayer[0].pagePostType == 'product' && dataLayer[0].pagePostType2 == undefined) {
    AWIN.Tracking.Rightlander.pagetype = 'category';
    AWIN.Tracking.Rightlander.category = 'shop';
} else if (dataLayer[0].pagePostType2 == 'single-product') {
    AWIN.Tracking.Rightlander.pagetype = 'product';
    AWIN.Tracking.Rightlander.identifier = dataLayer[0].ecommerce.detail.products[0].id;
} else if (location.href.includes('/cart/')) {
    AWIN.Tracking.Rightlander.pagetype = 'basket';
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
}
//only configure if PLT is not implemented
} else if (AWIN.Tracking.Sale) {
    AWIN.Tracking.Rightlander.pagetype = 'checkout';
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
console.log("Rightlander Object: ", AWIN.Tracking.Rightlander);
if (typeof zx_products !== "undefined") {
    console.log("zx_products: ", zx_products);
}
```


# Relevant Tickets

[CORALSERV-187](https://awin.atlassian.net/browse/CORALSERV-187)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/rightlander/plugin.js)