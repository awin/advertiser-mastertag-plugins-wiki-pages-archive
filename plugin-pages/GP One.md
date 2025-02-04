
# Supported Pages

- generic
- product
- home
- category
- basket
- registration

## Requirements

AWIN Mastertag must be implemented unconditionally across all pages in
the shop; checkout page requires AWIN.Tracking.Sale object.
Basket and checkout page requires PLT or an alternative data layer
containing product identifier. Plugin supports zx_products array.
Checkout page is automatically detected.

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with REF supplied by the partner.

## Plugin configuration example

**NOTE:** this plugin was previously called AddService Media. [When it
was
renamed](https://awin.atlassian.net/servicedesk/customer/portal/19/CORALSERV-274)to
GP One we put a fix in place so that the plugin works when configured
either `AWIN.Tracking.AddserviceMedia` or `AWIN.Tracking.GPOne`. This
note is just to inform you that the old configs are still using the
`AddServiceMedia` object, but the new ones should be configured with
`AWIN.Tracking.GPOne`, as shown below.

``` javascript
AWIN.Tracking.GPOne = AWIN.Tracking.GPOne || {};
AWIN.Tracking.GPOne.adserverId = "gp";
AWIN.Tracking.GPOne.websiteId = "brille24.de"; // value supplied by partner
AWIN.Tracking.GPOne.av = "addservicemedia";
AWIN.Tracking.GPOne.pagetype = "generic";

if (document.location.href.match(/home/)) {
    AWIN.Tracking.GPOne.pagetype = "home";
} else if (document.location.href.match(/category/)) {
    AWIN.Tracking.GPOne.pagetype = "category";
} else if (document.location.href.match(/product/i)) {
    AWIN.Tracking.GPOne.pagetype = "product";
    AWIN.Tracking.GPOne.identifier = google_tag_params.ecomm_prodid;;
} else if (/cart/.test(location.href)) {
    AWIN.Tracking.GPOne.pagetype = "basket";
    var zx_products = [];
    for (var i = 0; i < google_tag_manager["GTM-MFSNPS"].dataLayer.get("view_cart").items.length; i++) {
      var aw_prod = {};
      aw_prod.identifier = google_tag_manager["GTM-MFSNPS"].dataLayer.get("view_cart").items[i].item_id;
      zx_products.push(aw_prod);
  }
}
//only add if advertiser does not have PLT
if (AWIN.Tracking.Sale) {
  for (var i = 0; i < google_tag_manager["GTM-MFSNPS"].dataLayer.get("checkout").items.length; i++) {
    var aw_prod = {};
    aw_prod.identifier = google_tag_manager["GTM-MFSNPS"].dataLayer.get("checkout").items[i].item_id;
    zx_products.push(aw_prod);
  }
}
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/addserviceMedia/plugin.js)

# Tickets

[PROD-10065](https://jira.awin.com/browse/PROD-10065)