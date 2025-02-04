# How is the tag implemented?

The CityAds plugin has different tags depending on the type of page
visited.

# Integration requirements

The AWIN MasterTag needs to be fired unconditionally on all supported
pagetypes. Product data needs to be available in the advetiser's
dataLayer.

# Supported Pages

Replace `PAGETYPE` with any of the supported pagetypes:

- checkout
- product
- basket
- Any other `PAGETYPE` will default to "generic".

# Plugin implementation example


``` javascript
AWIN.Tracking.cityads = AWIN.Tracking.cityads || {};

if (dataLayer[3].google_tag_params && dataLayer[3].google_tag_params.ecomm_pagetype == 'product') {
    AWIN.Tracking.cityads.pagetype = 'product';
} else if (dataLayer[3].google_tag_params && dataLayer[3].google_tag_params.ecomm_pagetype == 'cart') {
    AWIN.Tracking.cityads.pagetype = 'basket';
    for (var i = 0; i < dataLayer.filter(x => x.event == "checkout")[0].ecommerce.checkout.products.length; i++) {
        var zx_products = [];
        zx_products.push({
            identifier: dataLayer.filter(x => x.event == "checkout")[0].ecommerce.checkout.products[i].id,
            quantity: dataLayer.filter(x => x.event == "checkout")[0].ecommerce.checkout.products[i].quantity
        });
    }
} else if (AWIN.Tracking.Sale) {
    AWIN.Tracking.cityads.pagetype = 'checkout';
    for (var i = 0; i < dataLayer.filter(x => x.event == "checkout")[0].ecommerce.checkout.products.length; i++) {
        var zx_products = [];
        zx_products.push({
            identifier: dataLayer.filter(x => x.event == "checkout")[0].ecommerce.checkout.products[i].id,
            quantity: dataLayer.filter(x => x.event == "checkout")[0].ecommerce.checkout.products[i].quantity
        });
    }
}
```




# Plugin Code

<https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/cityads/plugin.js>

# JIRA Ticket

<https://jira.awin.com/browse/PROD-7161>