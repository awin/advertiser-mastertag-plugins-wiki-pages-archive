# Supported Pages

- all
- basket
- checkout success

## Requirements

AWIN Mastertag must be implemented unconditionally across all pages in
the shop; checkout page requires AWIN.Tracking.Sale object.
Basket page requires PLT or an alternative data layer containing product
identifier, sku, product price and quantity.
Checkout page is automatically detected.

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with AdCartID supplied by the partner.

## Plugin configuration example

``` javascript
AWIN.Tracking.AdCart = AWIN.Tracking.AdCart || {};
AWIN.Tracking.AdCart.AdCartId = "VALUE_PLACEHOLDERS";

if(/cart/.test(location.href)) {
    AWIN.Tracking.AdCart.pagetype = "basket";
    var zx_products = [];
    for (var i = 0; i < document.getElementsByClassName("product-item").length; i++) {
        zx_products.push({
            'identifier': document.getElementsByClassName("product-item")[i].getAttribute("data-sku")
        })
    };
}
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/adCart/plugin.js)