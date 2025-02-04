
# Integration requirements

The Dwin1 tag needs to be displayed on each supported page and
unconditionally including the confirmation page as part of the Awin
conversion tracking. Plugin requires Product Level Tracking on the
confirmation page OR the basket data (identifier) / items must be
available within any custom data layer to configure the plugin.

# Supported Pages

- START
- PRODUCT
- CATALOG
- SEARCH
- CART
- CHECKOUT

Pagetype variable must be populated with one of the above values.

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters for fetching basket data on the
CHECKOUT page. Refer to the source code for more details.

## Generic Configuration Required For All Pages

``` javascript
AWIN.Tracking.Fatmedia = AWIN.Tracking.Fatmedia || {};
AWIN.Tracking.Fatmedia.program = "PROGRAM ID";
AWIN.Tracking.Fatmedia.pagetype = "PAGE_TYPE";
```



## Home Page

``` javascript
AWIN.Tracking.Fatmedia = AWIN.Tracking.Fatmedia || {};
AWIN.Tracking.Fatmedia.program = "PROGRAM ID";
AWIN.Tracking.Fatmedia.pagetype = "START";
```



## Product Page

``` javascript
AWIN.Tracking.Fatmedia = AWIN.Tracking.Fatmedia || {};
AWIN.Tracking.Fatmedia.program = "PROGRAM ID";
AWIN.Tracking.Fatmedia.pagetype = "PRODUCT";
AWIN.Tracking.Fatmedia.product = "PRODUCT_NUMBER";
```



## Category Page

``` javascript
AWIN.Tracking.Fatmedia = AWIN.Tracking.Fatmedia || {};
AWIN.Tracking.Fatmedia.program = "PROGRAM ID";
AWIN.Tracking.Fatmedia.pagetype = "CATALOG";
```



## Search Results Page

``` javascript
AWIN.Tracking.Fatmedia = AWIN.Tracking.Fatmedia || {};
AWIN.Tracking.Fatmedia.program = "PROGRAM ID";
AWIN.Tracking.Fatmedia.pagetype = "SEARCH";
```



## Basket Page

``` javascript
AWIN.Tracking.Fatmedia = AWIN.Tracking.Fatmedia || {};
AWIN.Tracking.Fatmedia.program = "PROGRAM ID";
AWIN.Tracking.Fatmedia.pagetype = "CART";
```



## Confirmation Page

Requires AWIN.Tracking.Sale object to be preset on the page. Pagetype
CHECKOUT will be automatically detected.

In addition to the above configuration, the plugin requires PLT or
zx_products array to be present on the page.

PLT:

``` javascript
<form name="aw_basket_form">
     <textarea id="aw_basket">
         AW:P|1001|test1234|123456|Test Product 1|3.99|1|sku2116|DEFAULT|DVD
         AW:P|1001|test1234|23456|Test Product 2|5.99|2|sku232|DEFAULT|Electronics
     </textarea>
 </form>
```


zx_products:

``` javascript
zx_products = [
     { identifier: 123456, amount: "3.99", currency: "EUR", quantity: 1 },
     { identifier: 23456, amount: "5.99", currency: "EUR", quantity: 2 }
 ];
```



# Configuration Example

``` javascript
AWIN.Tracking.Fatmedia = AWIN.Tracking.Fatmedia || {};
AWIN.Tracking.Fatmedia.program  = "15792";

if (dataLayer[0].page.PageType == "home") {
    AWIN.Tracking.Fatmedia.pagetype = "START";
} else if (dataLayer[0].page.PageType == "product.world")
{
    AWIN.Tracking.Fatmedia.pagetype = "CATALOG";

}
 else if (dataLayer[0].page.PageType == "product.detail") {
    AWIN.Tracking.Fatmedia.pagetype = "PRODUCT";
    AWIN.Tracking.Fatmedia.product = dataLayer.filter(x => x.ecDataAction == "productDetail")[0].ecommerce.detail.products[0].id;
}

 else if (/cart/.test(location.pathname))

 {
    AWIN.Tracking.Fatmedia.pagetype = "CART";
}
```



# Consent

Plugin supports consent flag parameter: AWIN.Tracking.Fatmedia.euconsent
= "1"; // default value If applicable, insert 1 or TCF consent string if
consent is given or 0 if no consent is given.

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/fatmedia/plugin.js)

# Relevant Tickets

[PROD-9226](https://jira.awin.com/browse/PROD-9226)