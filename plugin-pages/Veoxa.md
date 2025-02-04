
## Integration requirements

The Dwin1 tag needs to be displayed on each supported page and
unconditionally including the confirmation page as part of the Awin
conversion tracking.

- Plugin requires Product Level Tracking on the basket (price, quantity)
  and confirmation page (identifier, price, quantity) OR the basket data
  / items must be available within any custom data layer to configure
  the plugin.

# Plugin setup code

Replace `"VALUE_PLACEHOLDERS"` with real values.

### Home page


``` javascript
AWIN.Tracking.Veoxa = AWIN.Tracking.Veoxa || {};
AWIN.Tracking.Veoxa.aid="AID";
AWIN.Tracking.Veoxa.pid="PID";
AWIN.Tracking.Veoxa.pageType="home";
```




### Category page


``` javascript
AWIN.Tracking.Veoxa = AWIN.Tracking.Veoxa || {};
AWIN.Tracking.Veoxa.aid="AID";
AWIN.Tracking.Veoxa.pid="PID";
AWIN.Tracking.Veoxa.pageType="category";
AWIN.Tracking.Veoxa.category="CATEGORY_ID";
```




### Product page


``` javascript
AWIN.Tracking.Veoxa = AWIN.Tracking.Veoxa || {};
AWIN.Tracking.Veoxa.aid="AID";
AWIN.Tracking.Veoxa.pid="PID";
AWIN.Tracking.Veoxa.pageType="product";
AWIN.Tracking.Veoxa.identifier="PRODUCT_ID";
```





### Basket page


``` javascript
AWIN.Tracking.Veoxa = AWIN.Tracking.Veoxa || {};
AWIN.Tracking.Veoxa.aid="AID";
AWIN.Tracking.Veoxa.pid="PID";
AWIN.Tracking.Veoxa.pageType="basket";
AWIN.Tracking.Veoxa.currency="CURRENCY_ISO_ALPHA3";
```




### Checkout page


``` javascript
AWIN.Tracking.Veoxa.pageType="checkout";
AWIN.Tracking.Veoxa.key="KEY_ID";
];
```




# Example


``` javascript
AWIN.Tracking.Veoxa = AWIN.Tracking.Veoxa || {};
AWIN.Tracking.Veoxa.aid="1743";
AWIN.Tracking.Veoxa.pid="2530";
AWIN.Tracking.Veoxa.pageType = "generic";

if(window.location.pathname == "/"){
    AWIN.Tracking.Veoxa.pageType = "home";
}   else if (AWIN.Tracking.Sale) {
    AWIN.Tracking.Veoxa.key = "M_e75nmEV5m9XHh5Cn27A";
    AWIN.Tracking.Veoxa.pageType = "checkout";
}  else if (location.pathname.indexOf("/cart") != -1 ) {
    AWIN.Tracking.Veoxa.pageType = "basket";
    AWIN.Tracking.Veoxa.currency = document.getElementById("in-context-paypal-metadata").getAttribute("data-currency") || "EUR";
}   else if (location.pathname.indexOf("/products") != -1 ) {
    AWIN.Tracking.Veoxa.pageType = "product";
    AWIN.Tracking.Veoxa.identifier = location.pathname.split("/")[((location.pathname.split("/").length)-1)];
} else if (location.pathname.indexOf("/collections") != -1 ) {   // find dif identif
    AWIN.Tracking.Veoxa.pageType = "category";
    AWIN.Tracking.Veoxa.category = location.pathname.split("/")[2];
}
```



<https://jira.awin.com/browse/SOLUTION-33267>



# Source Code


``` javascript
AWIN.Tracking.Veoxa = AWIN.Tracking.Veoxa || {};
AWIN.Tracking.Veoxa.url = AWIN.Tracking.Veoxa.url || AWIN.sProtocol + 'profiling.veoxa.com';

(function($v) {
    var pagetype = $v.pageType || AWIN.Tracking.fetchZxParam('pagetype');
    if ("undefined" === typeof pagetype) {
        pagetype = "undefined";
    } else {
        pagetype = pagetype.toLowerCase();
    }

    if (pagetype === 'undefined' || typeof $v.aid === "undefined" || typeof $v.pid === "undefined") {
        return;
    }

    $v.fetchBasketData = function() {
        var basketData = [],
            products = AWIN.Tracking.fetchZxParam('products') || AWIN.Tracking.getBasketData();

        if (typeof products === "string") {
            products = JSON.parse(products);
        }

        for (var i = 0; i < products.length; i++) {
            basketData.push({
                "id": products[i].identifier || products[i].id,
                "quantity": products[i].quantity,
                "price": products[i].amount || products[i].price
            });
        }
        return basketData;
    };

    $v.getBasketString = function() {
        return $v.fetchBasketData()
            .map(function (p){return `${p.id}:${p.price}:${p.quantity}`;})
            .join(';');
    };

    $v.getBasketValue = function() {
        return $v.fetchBasketData()
            .reduce(
                function(a,p) {return a + (p.quantity * p.price);},
                0
            );
    };

    var path;
    var paramsArray = {
        "aid": $v.aid,
        "pid": $v.pid
    };

    switch (pagetype) {
        case "home":
            path = '/boot/request/';
            paramsArray.action = 'Index';
            break;
        case "category":
            path = '/boot/request/';
            paramsArray.action = 'Category';
            paramsArray.categoryId = $v.category || AWIN.Tracking.fetchZxParam('category');
            break;
        case "product":
            path = '/boot/request/';
            paramsArray.action = 'Product';
            paramsArray.productId = $v.identifier || AWIN.Tracking.fetchZxParam('identifier');;
            break;
        case "basket":
            path = '/boot/request/';
            paramsArray.action = 'Basket';
            paramsArray.products = $v.getBasketString();
            paramsArray.amount = $v.getBasketValue();
            var currency = $v.currency || AWIN.Tracking.fetchZxParam('currency');
            if (typeof currency !== "undefined") {
                paramsArray.currency = currency;
            }
            break;
        case "checkout":
            path = '/transaction/boot/';
            paramsArray.key = $v.key;
            paramsArray.ref = AWIN.Tracking.fetchZxParam('transaction') || AWIN.Tracking.Sale.orderRef;
            paramsArray.amount = AWIN.Tracking.fetchZxParam('total_amount') || AWIN.Tracking.Sale.amount;
            paramsArray.products = $v.getBasketString();
            paramsArray.currency = AWIN.Tracking.fetchZxParam('currency') || AWIN.Tracking.Sale.currency;
            break;
        default:
            return;
            break;
    }

    AWIN.Tracking.scriptAppend(
        $v.url + path + '?' + AWIN.Tracking.buildQueryString(paramsArray),
        null,
        null,
        {"charset":"UTF-8", "async":"async", "defer":"defer"}
    );
})(AWIN.Tracking.Veoxa);
```




## Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/veoxa/plugin.js)

# JIRA TICKET

[PROD-9152](https://jira.awin.com/browse/PROD-9152)