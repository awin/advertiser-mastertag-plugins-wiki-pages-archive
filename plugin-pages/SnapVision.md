# Requirements

- Mastertag must be displayed across all product pages in the shop.



# Configuration

Plugin supports following PAGETYPE: product

## Configuration Example

The pagetype should be hard-coded to "product". The corresponding
properties for product ID and product category need to be populated
dynamically with data from the product page.


``` javascript

AWIN.Tracking.SnapVision = AWIN.Tracking.SnapVision || {};

if(dataLayer.filter(x => x.pagePostType2 == "single-product").length > 0){
    AWIN.Tracking.SnapVision.pagetype = "product";
    AWIN.Tracking.SnapVision.identifier = dataLayer.filter(x => x.pagePostType2 == "single-product")[0].ecommerce.detail.products[0].id;
    AWIN.Tracking.SnapVision.category = dataLayer.filter(x => x.pagePostType2 == "single-product")[0].ecommerce.detail.products[0].category;
}
```




# Relevant Tickets

[PROD-10122](https://jira.awin.com/browse/PROD-10122)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/snapVision/plugin.js)

# Example Implementation

Note that plugin could be deactivated, in which case needs to be
activated on test advertiser account. [Test
Shop](https://ts-awin.com/woocommerce/product/test-product-1/)