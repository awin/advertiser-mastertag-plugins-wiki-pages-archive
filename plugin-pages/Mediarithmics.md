# Mediarithmics plugin

## Description

To do

## Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace "ID" with its real value supplied by **Mediarithmics** for the
Advertiser.


``` javascript
AWIN.Tracking.Mediarithmics = AWIN.Tracking.Mediarithmics || {};
AWIN.Tracking.Mediarithmics.id = "ID";
```




### What to setup?

- product page :

set up this variable **AWIN.Tracking.Product.id** with productID given
on the page to identify that you are on the product page


``` javascript
AWIN.Tracking.Product = AWIN.Tracking.Product || {};
AWIN.Tracking.Product.id = "PRODUCT_ID";
```


- basket page :

if zx_products is defined, then call the function
**zx_generate_awin_basket()** to generate a awin basket else define the
zx_products first to identify that you are on the basket page

- checkout page :

set up this variable **AWIN.Tracking.Sale** with :

\+ AWIN.Tracking.Sale.orderRef to get orderID
+ AWIN.Tracking.Sale.currency to get currency

and call the function **zx_generate_awin_basket()** to generate a awin
basket from zx_products

### Generate Awin Basket from zx_products

This function will convert zx_products to Awin basket (for basket and
checkout pages)


``` javascript
// Function definition
function zx_generate_awin_basket() {
    if (!document.getElementById("aw_basket")) {
        var basket_textarea = document.createElement("textarea");
        basket_textarea.id = "aw_basket";
        basket_textarea.style = "display:none";
        basket_textarea.value = "";
        if (typeof zx_products != 'undefined') {
            for (var i = 0; i < zx_products.length; i++) {
                basket_textarea.value += "[x]|[y]|[z]|[" + zx_products[i].identifier + "]|[" + zx_products[i].identifier + "]|[" + zx_products[i].amount + "]|[" + zx_products[i].quantity + "]|[sku]|[cg]|[category]\n";
            }
        }
        document.getElementsByTagName('body')[0].appendChild(basket_textarea);
    }
}

// Call the function
zx_generate_awin_basket();
```


### Example for "Carte Zero" advertiser


``` javascript

AWIN.Tracking.Mediarithmics = AWIN.Tracking.Mediarithmics || {};
AWIN.Tracking.Mediarithmics.id = "CZR201601";

function zx_generate_awin_basket() {
    if (!document.getElementById("aw_basket")) {
        var basket_textarea = document.createElement("textarea");
        basket_textarea.id = "aw_basket";
        basket_textarea.style = "display:none";
        basket_textarea.value = "";
        if (typeof zx_products != 'undefined') {
            for (var i = 0; i < zx_products.length; i++) {
                basket_textarea.value += "[x]|[y]|[z]|[" + zx_products[i].identifier + "]|[" + zx_products[i].identifier + "]|[" + zx_products[i].amount + "]|[" + zx_products[i].quantity + "]|[sku]|[cg]|[category]\n";
            }
        }
        document.getElementsByTagName('body')[0].appendChild(basket_textarea);
    }
}

if (window.location.href.indexOf("product.htm") > -1) {
    AWIN.Tracking.Product.id = zx_identifier;
} else if (window.location.href.indexOf("basket.htm") > -1) {
    zx_generate_awin_basket();
} else if (window.location.href.indexOf("Checkout.htm") > -1) {
    zx_generate_awin_basket();
    AWIN.Tracking.Sale = {orderRef:zx_transaction, amount:zx_total_amount};
}zx_generate_awin_basket();
}
```


### EXAMPLE of requests in the browser

product page :


``` javascript
https://events.mediarithmics.com/v1/visits/pixel?%24items=jso-%5B%7B%22%24id%22%3A%2258936%22%7D%5D&%24ev=%24item_view&%24site_token=CZR201601&%24referrer=http%3A%2F%
= after decode :
https://events.mediarithmics.com/v1/visits/pixel?$items=jso-[{"$id":"58936"}]&$ev=$item_view&$site_token=CZR201601&$referrer=http:/..
product ID = 58936
token = CZR201601
```


basket page :


``` javascript
https://events.mediarithmics.com/v1/visits/pixel?%24items=jso-%5B%7B%22%24id%22%3A%2258936%22%2C%22%24price%22%3A%2288.50%22%2C%22%24qty%22%3A%221%22%7D%2C%7B%22%24id%22%3A%2257525%22%2C%22%24price%22%3A%2239.20%22%2C%22%24qty%22%3A%221%22%7D%5D&%24ev=%24basket_view&%24site_token=LMC201601&%24referrer=http%3A%2F%2Flemoncurve.com%2Flingerie-soutiens-gorge-corbeilles-balconnets%2F57525-soutien-gorge-balconnet-l-agent-by-agent-provocateur-mariona-red.html%3Fadded%3D1&%24url=http%3A%2F%2Fl..
= after decode :
https://events.mediarithmics.com/v1/visits/pixel?$items=jso-[{"$id":"58936","$price":"88.50","$qty":"1"},{"$id":"57525","$price":"39.20","$qty":"1"}]&$ev=$basket_view&$site_token=LMC201601&$referrer=http://..
```

