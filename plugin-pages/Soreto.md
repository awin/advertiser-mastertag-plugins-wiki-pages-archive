
# How is the tag implemented?

The plugin should be fired automatically on the checkout page (if
AWIN.Tracking.Sale is present there). AWIN Mastertag and
Awin.Tracking.Sale object should be displayed unconditionally on the
confirmation page.

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | Soreto            |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Please replace "**MERCHANT_ID**" with a Advertiser ID.

The code should be fired only on the confirmation page.


``` javascript
AWIN.Tracking.Soreto = AWIN.Tracking.Soreto || {};
AWIN.Tracking.Soreto.identifier = "MERCHANT_ID";
```


Example:


``` javascript
AWIN.Tracking.Soreto = AWIN.Tracking.Soreto || {};
AWIN.Tracking.Soreto.identifier = "1001";
```




## Plugin code:


``` javascript
AWIN.Tracking.Soreto = AWIN.Tracking.Soreto || {};

(function ($a) {

  if (typeof $a.identifier === "undefined" || !AWIN.Tracking.Sale) {
    return;
  }

  $a.appendImg = function() {
    if (document.getElementsByTagName("body")[0]) {
      var image = document.createElement("img");
      image.id = 'reverbPixel';
      document.getElementsByTagName("body")[0].appendChild(image);
      AWIN.Tracking.hideElement(image);
    }
  };

  window.reverbAsyncInit = function() {

    var products = AWIN.Tracking.getBasketData();

    ReverbLightbox.open({
      timeout: 1500,
      firstName: $a.firstName
    }, $a.email);

    var order = Reverb.initOrder();

    order.setOrderId(AWIN.Tracking.Sale.orderRef);
    order.setOrderTotal(AWIN.Tracking.Sale.amount);

    products.forEach(function (product) {
      order.addLineItem(
        product.name,
        product.cg,
        product.sku,
        product.quantity,
        product.price,
        product.category
      );
    });
    order.ready();
    Reverb.init($a.identifier);
  };

  $a.appendImg();

  AWIN.Tracking.scriptAppend('https://api.soreto.com/scripts/reverb-sdk-1.5.0.min.js');
})(AWIN.Tracking.Soreto);
```

