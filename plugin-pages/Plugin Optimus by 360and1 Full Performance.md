# Requirements

- Mastertag must be displayed across all pages in the shop
- javascript based tracking code must be loaded unconditionally on the
  order confirmation page.
- Plugin requires Product Level Tracking implemented on the checkout
  success page or any alternative dataLayer.



# Configuration

Plugin supports following PAGETYPE: checkout, generic
Replace `"TOKEN"` with real values. Checkout success page will be
automatically detected, when AWIN.Tracking.Sale object is available.

## Configuration Example

Configurable tokens per PageType (supplied by Optimus):


``` javascript
AWIN.Tracking.OptimusBy360And1 = AWIN.Tracking.OptimusBy360And1 || {};
AWIN.Tracking.OptimusBy360And1.token = 'TOKEN';

var zx_products = [];
if(AWIN.Tracking.Sale){
  AWIN.Tracking.OptimusBy360And1.pagetype = 'checkout';
  for(var i = 0; i<dataLayer.filter(x =>x.ecommerce)[1].ecommerce.items.length; i++){
            var o = {};
            o.identifier =dataLayer.filter(x =>x.ecommerce)[1].ecommerce.items[i].item_name
            o.price = dataLayer.filter(x =>x.ecommerce)[1].ecommerce.items[i].price
            o.quantity =dataLayer.filter(x =>x.ecommerce)[1].ecommerce.items[i].quantity
            zx_products.push(o);
    }
}
```




# Relevant Tickets

[PROD-9969](https://jira.awin.com/browse/PROD-9968)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/optimusBy360And1/plugin.js)