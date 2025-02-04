
# Page types

The plugin fires on all pages.

# Requirements

The MasterTag should fire on all pages unconditionally.

# Plugin Configuration Code

The plugin does not require any advertiser identifier. The plugin only
requires page an product identifiers for the product page and checkout
page. Note, if the advertiser has PLT implemented, then you should not
create a config for the checkout page.


``` javascript
AWIN.Tracking.NspireDigital = AWIN.Tracking.NspireDigital || {};

if (document.location.pathname.includes("/product/")) {
    AWIN.Tracking.NspireDigital.pageType = "product";
    AWIN.Tracking.NspireDigital.identifier = [PRODUCT_ID];
} else if (AWIN.Tracking.Sale) {  //only configure is PLT is not implemented
    AWIN.Tracking.NspireDigital.pageType = "checkout";
    var zx_products = [];
    for (var i = 0; i < dataLayer.purchase.items.length; i++) {
            zx_products.push({"identifier" : [PRODUCT_ID]});
    }
}
```


# Example


``` javascript
AWIN.Tracking.NspireDigital = AWIN.Tracking.NspireDigital || {};

if (document.location.pathname.includes("/product/")) {
    AWIN.Tracking.NspireDigital.pageType = "product";
    AWIN.Tracking.NspireDigital.identifier = dataLayer.filter(function(x){return x.ecommerce;})[0].ecommerce.items[0].id;
} else if (AWIN.Tracking.Sale) {
    AWIN.Tracking.NspireDigital.pageType = "checkout";
    var zx_products = [];
    for (var i = 0; i < dataLayer.filter(function(x){return x.ecommerce;})[0].ecommerce.items.length; i++) {
            zx_products.push({"identifier" : dataLayer.filter(function(x){return x.ecommerce;})[0].ecommerce.items[i].id});
    }
}
```


# Relevant Tickets

[CORALSERV-381](https://awin.atlassian.net/browse/CORALSERV-381)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/nspireDigital/plugin.js)