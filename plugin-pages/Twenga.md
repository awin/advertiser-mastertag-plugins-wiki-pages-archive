
# Integration requirements

- The Dwin1 tag needs to be displayed on each supported page and
  unconditionally including the confirmation page as part of the Awin
  conversion tracking.
- Plugin requires Product Level Tracking on the confirmation page
  (alternatively the basket data / items must be available within any
  custom data layer to configure the plugin)
- Product identifier passed on the product- and confirmation page must
  match the product ID from awin feed

# Supported Pages

- Product Page
- Checkout Page

# Configuration

Refer to the source code for more details.

Replace `"VALUE_PLACEHOLDERS"` with real values.

## General Configuration


``` javascript
AWIN.Tracking.Twenga = AWIN.Tracking.Twenga || {};
AWIN.Tracking.Twenga.host = "HOST";
AWIN.Tracking.Twenga.master_site_id = "MASTER_SITE_ID";
```

HOST value supplied by Twenga
MASTER_SITE_ID value supplied by Twenga e.g.
twenga.my-ecommerce-site.com




## Product Page Configuration


``` javascript
AWIN.Tracking.Twenga = AWIN.Tracking.Twenga || {};
AWIN.Tracking.Twenga.pageType = "product";
AWIN.Tracking.Twenga.host = "HOST";
AWIN.Tracking.Twenga.master_site_id = "MASTER_SITE_ID";
AWIN.Tracking.Twenga.item_feed_reference_id = "FEED_REFERENCE_ID";
AWIN.Tracking.Twenga.item_feed_variant_id = "FEED_VARIANT_ID";
AWIN.Tracking.Twenga.item_currency = "CURRENCY";
AWIN.Tracking.Twenga.item_price = "PRICE";
```

FEED_REFERENCE_ID product identifier (same as in the Awin feed)
FEED_VARIANT_ID Product variant identifier as it appears in the feed.
Optional value if it is not used in the feed
CURRENCY ISO 4217 -\> EUR, USD
PRICE item price. "." must be used as separator of the decimal part. Ex:
60.00




## Checkout Page Configuration

Plugin will automatically detect the checkout page (if
AWIN.Tracking.Sale is available) and use product details from
zx_products array or Product Level Tracking.


``` javascript
AWIN.Tracking.Twenga = AWIN.Tracking.Twenga || {};
AWIN.Tracking.Twenga.pageType = "checkout";
AWIN.Tracking.Twenga.host = "HOST";
AWIN.Tracking.Twenga.master_site_id = "MASTER_SITE_ID";
```




## Configuration Example


``` javascript
AWIN.Tracking.Twenga = AWIN.Tracking.Twenga || {};
AWIN.Tracking.Twenga.host = "conforamaes.twgdns.com";
AWIN.Tracking.Twenga.master_site_id = "10313487";

if(dataLayer[0].pageType === "Pproduct"){
    AWIN.Tracking.Twenga.pageType = "product";
    AWIN.Tracking.Twenga.item_feed_reference_id = document.querySelector('meta[property="product:retailer_item_id"]').getAttribute('content');
    AWIN.Tracking.Twenga.item_currency = "EUR";
    AWIN.Tracking.Twenga.item_price = dataLayer[0].ecommerce.detail.products[0].price;
}
```



== Related JIRA Ticket ==
[PROD-8936](https://jira.awin.com/browse/PROD-8936)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/twenga/plugin.js)