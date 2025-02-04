
## Setup Supported Pages

Replace `"VALUE_PLACEHOLDERS"` with real values.


=== Home Page ===


``` javascript
AWIN.Tracking.RemailMe = AWIN.Tracking.RemailMe || {};
AWIN.Tracking.RemailMe.networkId = "NETWORK_ID";
AWIN.Tracking.RemailMe.userEmail = "USER_EMAIL";
AWIN.Tracking.RemailMe.pagetype = "home";
```



=== Category Page ===


``` javascript
AWIN.Tracking.RemailMe = AWIN.Tracking.RemailMe || {};
AWIN.Tracking.RemailMe.networkId = "NETWORK_ID";
AWIN.Tracking.RemailMe.userEmail = "USER_EMAIL";
AWIN.Tracking.RemailMe.pagetype = "category";
AWIN.Tracking.RemailMe.category = "CATEGORY_ID";
AWIN.Tracking.RemailMe.subcategory = "SUB_CATEGORY_ID";
```



=== Search Page ===


``` javascript
AWIN.Tracking.RemailMe = AWIN.Tracking.RemailMe || {};
AWIN.Tracking.RemailMe.networkId = "NETWORK_ID";
AWIN.Tracking.RemailMe.userEmail = "USER_EMAIL";
AWIN.Tracking.RemailMe.pagetype = "search";
AWIN.Tracking.RemailMe.searchQuery = "SEARCH_QUERY";
```




### Product Page


``` javascript
AWIN.Tracking.RemailMe = AWIN.Tracking.RemailMe || {};
AWIN.Tracking.RemailMe.networkId = "NETWORK_ID";
AWIN.Tracking.RemailMe.userEmail = "USER_EMAIL";
AWIN.Tracking.RemailMe.pagetype = "product";
AWIN.Tracking.RemailMe.identifier = "PRODUCT_ID";
```




### Basket Page


``` javascript
AWIN.Tracking.RemailMe = AWIN.Tracking.RemailMe || {};
AWIN.Tracking.RemailMe.networkId = "NETWORK_ID";
AWIN.Tracking.RemailMe.userEmail = "USER_EMAIL";
AWIN.Tracking.RemailMe.pagetype = "basket";
```



=== Checkout Page ===


``` javascript
AWIN.Tracking.RemailMe = AWIN.Tracking.RemailMe || {};
AWIN.Tracking.RemailMe.networkId = "NETWORK_ID";
AWIN.Tracking.RemailMe.userEmail = "USER_EMAIL";
AWIN.Tracking.RemailMe.pagetype = "checkout";
AWIN.Tracking.Sale.orderRef = "ORDER_REF";
```



=== Wishlist Page ===


``` javascript
AWIN.Tracking.RemailMe = AWIN.Tracking.RemailMe || {};
AWIN.Tracking.RemailMe.networkId = "NETWORK_ID";
AWIN.Tracking.RemailMe.userEmail = "USER_EMAIL";
AWIN.Tracking.RemailMe.pagetype = "wishlist";
```



=== Pushback Page ===


``` javascript
AWIN.Tracking.RemailMe = AWIN.Tracking.RemailMe || {};
AWIN.Tracking.RemailMe.networkId = "NETWORK_ID";
AWIN.Tracking.RemailMe.userEmail = "USER_EMAIL";
AWIN.Tracking.RemailMe.pagetype = "pushback";
```






## Plugin Code


``` javascript
AWIN.Tracking.RemailMe = AWIN.Tracking.RemailMe || {};
AWIN.Tracking.RemailMe.url = AWIN.Tracking.RemailMe.url || AWIN.sProtocol + "tr.cloud-media.fr/t/{NETWORK_ID}";

AWIN.Tracking.CryptoJS = AWIN.Tracking.CryptoJS || {};
AWIN.Tracking.CryptoJS.Core = AWIN.Tracking.CryptoJS.Core || {};
AWIN.Tracking.CryptoJS.Sha256 = AWIN.Tracking.CryptoJS.Sha256 || {};
AWIN.Tracking.CryptoJS.Core.url = "https://cdnjs.cloudflare.com/ajax/libs/crypto-js/3.1.9-1/core.js";
AWIN.Tracking.CryptoJS.Sha256.url = "https://cdnjs.cloudflare.com/ajax/libs/crypto-js/3.1.9-1/sha256.min.js";

(function($r) {
    try {
        $r.fetchBasketData = function() {
            let basketData = [],
                products = AWIN.Tracking.getBasketData();
            for (var i = 0; i < products.length; i++) {
                basketData.push({
                    "id": products[i].id,
                    "quantity": products[i].quantity,
                    "price": products[i].price
                });
            }
            return basketData;
        };

        $r.remailMeCallback = function () {
            if (typeof $r.networkId === "undefined") {
                return;
            }

            if (typeof $r.pagetype === "undefined") {
                return;
            }

            let pagetype = $r.pagetype.toLowerCase();

            if (AWIN.Tracking.Sale) {
                pagetype = "checkout";
            } else if ("checkout" === pagetype) {
                AWIN.Tracking.Sale = {};
            }

            let pixelParameters = {
                    "h": CryptoJS.SHA256($r.userEmail || "").toString(CryptoJS.enc.Hex)
                },
                addProductData = function (d, addOnlyId) {
                    $r.fetchBasketData().forEach(function(v,k){
                        d["products[" + k + "][id]"] = v.id;
                        if (addOnlyId === true) return;
                        d["products[" + k + "][price]"] = v.price;
                        d["products[" + k + "][quantity]"] = v.quantity;
                    });
                };

            switch (pagetype) {
                case "home":
                    pixelParameters = {...pixelParameters, "action": "home", "w": window.location.hostname};
                    break;
                case "category":
                    pixelParameters = {...pixelParameters, "action": "catalog", "cat": $r.category, "sscat": $r.subcategory};
                    addProductData(pixelParameters, true);
                    break;
                case "search":
                    pixelParameters = {...pixelParameters, "action": "search", "query": $r.searchQuery};
                    addProductData(pixelParameters, true);
                    break;
                case "product":
                    pixelParameters = {...pixelParameters, "action": "product", "product": $r.identifier};
                    addProductData(pixelParameters, true);
                    break;
                case "basket":
                    pixelParameters = {...pixelParameters, "action": "cart"};
                    addProductData(pixelParameters);
                    break;
                case "checkout":
                    pixelParameters = {...pixelParameters, "action": "sale", "order_id": AWIN.Tracking.Sale.orderRef};
                    addProductData(pixelParameters);
                    break;
                case "wishlist":
                    pixelParameters = {...pixelParameters, "action": "wishlist"};
                    addProductData(pixelParameters, true);
                    break;
                case "pushback":
                    pixelParameters = {...pixelParameters, "action": "pushback"};
                    break;
                default:
                    return;
                    break;
            }

            const url = $r.url.replace("{NETWORK_ID}", $r.networkId);
            AWIN.Tracking.pixelAppend(url + "?" + AWIN.Tracking.buildQueryString(pixelParameters));
        };

        $r.sha256Callback = function () {
            AWIN.Tracking.scriptAppend(AWIN.Tracking.CryptoJS.Sha256.url, null, "AWIN.Tracking.RemailMe.remailMeCallback()", {async:"true"});
        };

        AWIN.Tracking.scriptAppend(AWIN.Tracking.CryptoJS.Core.url, null, "AWIN.Tracking.RemailMe.sha256Callback()", {async:"true"});
    } catch (e) {
        console.log(e);
    }
})(AWIN.Tracking.RemailMe);
```




## JIRA Ticket

<https://jira.awin.com/browse/PROD-8591>

## Source Code Repository

<https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/remailMe/plugin.js>