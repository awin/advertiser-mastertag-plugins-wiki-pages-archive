# Supported Pages

- Generic Page
- Product Page
- Checkout Page
- Category Page
- Basket Page
- Demarker Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Generic & Demarker Page Configuration

``` javascript
AWIN.Tracking.hofeMedia = AWIN.Tracking.hofeMedia || {};
AWIN.Tracking.hofeMedia.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.hofeMedia.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.hofeMedia = AWIN.Tracking.hofeMedia || {};
AWIN.Tracking.hofeMedia.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.hofeMedia.category = "CATEGORY";
AWIN.Tracking.hofeMedia.feedID = "FEED_ID";
AWIN.Tracking.hofeMedia.identifier = "IDENTIFIER";
AWIN.Tracking.hofeMedia.pagetype = "PAGE_TYPE";
```



## Checkout Page Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.hofeMedia = AWIN.Tracking.hofeMedia || {};
AWIN.Tracking.hofeMedia.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.hofeMedia.feedID = "FEED_ID";
AWIN.Tracking.hofeMedia.pagetype = "PAGE_TYPE";
```



## Category Page Configuration

``` javascript
AWIN.Tracking.hofeMedia = AWIN.Tracking.hofeMedia || {};
AWIN.Tracking.hofeMedia.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.hofeMedia.category = "CATEGORY";
AWIN.Tracking.hofeMedia.pagetype = "PAGE_TYPE";
```



## Basket Page Configuration

``` javascript
AWIN.Tracking.hofeMedia = AWIN.Tracking.hofeMedia || {};
AWIN.Tracking.hofeMedia.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.hofeMedia.category = "CATEGORY";
AWIN.Tracking.hofeMedia.feedID = "FEED_ID";
AWIN.Tracking.hofeMedia.pagetype = "PAGE_TYPE";
```



# Configuration Example

``` javascript
AWIN.Tracking.hofeMedia = AWIN.Tracking.hofeMedia || {};
 AWIN.Tracking.hofeMedia.advertiserId = "50562";
 AWIN.Tracking.hofeMedia.pagetype = "generic";
 AWIN.Tracking.hofeMedia.feedID = "16402";


 if(dataLayer[0].pageType == "catalog/category/view")
 {
 AWIN.Tracking.hofeMedia.category = dataLayer[0].categoryName;
 AWIN.Tracking.hofeMedia.pagetype = "category";
 }

 else if(dataLayer[0].pageType == "catalog/product/view")
 {
 AWIN.Tracking.hofeMedia.pagetype = "product";
 AWIN.Tracking.hofeMedia.category = dataLayer[0].categoryName;
 AWIN.Tracking.hofeMedia.identifier = dataLayer[0].productSku;
 }

 else if(dataLayer[0].pageType == "checkout/cart/index")
 {
 AWIN.Tracking.hofeMedia.pagetype = "basket";
     var zx_products = [];
     for (var i = 0; i < awin_sku_stamm.length; i++)
    {
         zx_products.push({
        'identifier':awin_sku_stamm[i],
        'quantity':JSON.parse(dataLayer[0].transactionProducts)[i].quantity})
     }
 }

 else if (AWIN.Tracking.Sale)
 {
    for (var i = 0; i < awin_sku_stamm.length; i++)
    {
        var o = {};
        o.identifier = awin_sku_stamm[i];
        o.quantity = dataLayer[0].transactionProducts[i].quantity;
        zx_products.push(o);
    }
}
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/hofeMedia/plugin.js)