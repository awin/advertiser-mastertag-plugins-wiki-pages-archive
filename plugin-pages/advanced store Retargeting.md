# Integration requirements

The Dwin1 tag (Masterag) needs to be displayed on every page and
unconditionally including the confirmation page as part of the Awin
conversion tracking.

# Supported Pages

- Home page
- Category Page
- Product Page
- Basket page
- Search Page
- Checkout Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Home Page Configuration

``` javascript
AWIN.Tracking.ad4matNew = AWIN.Tracking.ad4matNew || {};
AWIN.Tracking.ad4matNew.token = "TOKEN";
AWIN.Tracking.ad4matNew.pageUrl = "URL_TOKEN";
AWIN.Tracking.ad4matNew.pagetype = "home";
```



## Category Page Configuration

``` javascript
AWIN.Tracking.ad4matNew = AWIN.Tracking.ad4matNew || {};
AWIN.Tracking.ad4matNew.token = "TOKEN";
AWIN.Tracking.ad4matNew.pageUrl = "URL_TOKEN";
AWIN.Tracking.ad4matNew.pagetype = "category";
AWIN.Tracking.ad4matNew.categoryId = "CATEGORY_ID";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.ad4matNew = AWIN.Tracking.ad4matNew || {};
AWIN.Tracking.ad4matNew.token = "TOKEN";
AWIN.Tracking.ad4matNew.pageUrl = "URL_TOKEN";
AWIN.Tracking.ad4matNew.pagetype = "product";
AWIN.Tracking.ad4matNew.categoryId = "CATEGORY_ID";
AWIN.Tracking.ad4matNew.productId = "PRODUCT_ID";
```



## Product and Search Page Configuration

``` javascript
AWIN.Tracking.ad4matNew = AWIN.Tracking.ad4matNew || {};
AWIN.Tracking.ad4matNew.token = "TOKEN";
AWIN.Tracking.ad4matNew.pageUrl = "URL_TOKEN";
AWIN.Tracking.ad4matNew.pagetype = "search";
AWIN.Tracking.ad4matNew.categoryId = "CATEGORY_ID";
AWIN.Tracking.ad4matNew.productId = "PRODUCT_ID";
```



## Basket Page Configuration

``` javascript
AWIN.Tracking.ad4matNew = AWIN.Tracking.ad4matNew || {};
AWIN.Tracking.ad4matNew.token = "TOKEN";
AWIN.Tracking.ad4matNew.pageUrl = "URL_TOKEN";
AWIN.Tracking.ad4matNew.pagetype = "basket";
AWIN.Tracking.ad4matNew.currency = "PRODUCT_SALE_CURRENCY";
```


Plugin will collect information about product category ID, product ID,
quantity and price via Product Level Tracking.

If the currency is not provided via the configuration, its value will be
set to empty string.

## Checkout Page Configuration

``` javascript
AWIN.Tracking.ad4matNew = AWIN.Tracking.ad4matNew || {};
AWIN.Tracking.ad4matNew.token = "TOKEN";
AWIN.Tracking.ad4matNew.pagetype = "checkout";
AWIN.Tracking.ad4matNew.pageUrl = "URL_TOKEN";
AWIN.Tracking.ad4matNew.rtOptout = "RT_OUTPUT";
```


Plugin will collect currency and revenue details from AWIN.Tracking.Sale
object. Category, product ID and quantity details will be taken from
product level tracking if it's implemented on merchant's site.

#### GDPR common parameters for all pagetypes:

- `AWIN.Tracking.ad4matNew.gdpr = "GDPR";`
- `AWIN.Tracking.ad4matNew.gdpr_consent = "GDPR_CONSENT";`
- `AWIN.Tracking.ad4matNew.gdpr_pd = "GDPR_PD";`




= Relevant Tickets =

[PROD-8058](https://jira.awin.com/browse/PROD-8058)
[PROD-9145](https://jira.awin.com/browse/PROD-9145)

Example code:


``` javascript
AWIN.Tracking.ad4matNew = AWIN.Tracking.ad4matNew || {};
AWIN.Tracking.ad4matNew.token = "2rukl8we";
AWIN.Tracking.ad4matNew.pageUrl = location.href;
if(location.href.match(/drestige\.com(((\/)|(\?(\S+)?)|(\/\?(\S+)?)))?$/i) ||
location.href.match(/destige\.com\/index\.aspx(((\/)|(\?(\S+)?)|(\/\?(\S+)?)))?$/i))
{
    AWIN.Tracking.ad4matNew.pagetype = "home";
}
else if(location.href.match(/collection/i))
{
    AWIN.Tracking.ad4matNew.pagetype = "category";
    AWIN.Tracking.ad4matNew.categoryId = location.href.split("=")[location.href.split("=").length-1];
}
else if(location.href.match(/product/i))
{
    AWIN.Tracking.ad4matNew.pagetype = "product";
    AWIN.Tracking.ad4matNew.categoryId = dataLayer[4][2].items[0].category;
    AWIN.Tracking.ad4matNew.productId  = dataLayer[4][2].items[0].id;
}
else if(location.href.match(/collection\?s/i))
{
    AWIN.Tracking.ad4matNew.pagetype = "search";
    AWIN.Tracking.ad4matNew.categoryId =
        AWIN.Tracking.getQueryVarValue('s', document.location.search.substring(1));
}
else if(location.href.match(/carrello/i))
{
    AWIN.Tracking.ad4matNew.pagetype = "basket";
    AWIN.Tracking.ad4matNew.currency = "EUR";
}
```


# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/ad4mat_new/plugin.js)