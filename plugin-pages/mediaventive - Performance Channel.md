# Plugin setup code

Replace `CONTAINER_ID` with its real value. It is an Id of 10 hex
characters.

Replace `PAGETYPE` with any of the supported pagetypes:

- homepage
- search
- category
- product
- basket
- order (if AWIN.Tracking.Sale and PLT are implemented, then you do not
  need to do anything for this page type)
- Any other `PAGETYPE` will default to "generic".


``` javascript
AWIN.Tracking.MediaVentive = AWIN.Tracking.MediaVentive || {};
AWIN.Tracking.MediaVentive.containerId = 'CONTAINER_ID';
AWIN.Tracking.MediaVentive.pagetype = 'PAGETYPE';
```




# Plugin example code GTM


``` javascript
AWIN.Tracking.MediaVentive = AWIN.Tracking.MediaVentive || {};
AWIN.Tracking.MediaVentive.containerId = 'f993e04444';
AWIN.Tracking.MediaVentive.pagetype = "generic";

if (google_tag_manager["GTM-NFBSZKB"].dataLayer.get("google_tag_params.ecomm_pagetype") == "cart") {
    AWIN.Tracking.MediaVentive.pagetype = "basket";
    var zx_products = [];
    for (var i = 0; i < google_tag_manager["GTM-NFBSZKB"].dataLayer.get("ecommerce.checkout.products").length; i++) {
        var o = {};
        o.identifier = google_tag_manager["GTM-NFBSZKB"].dataLayer.get("ecommerce.checkout.products")[i].id;
        o.quantity = google_tag_manager["GTM-NFBSZKB"].dataLayer.get("ecommerce.checkout.products")[i].quantity;
        o.amount = google_tag_manager["GTM-NFBSZKB"].dataLayer.get("ecommerce.checkout.products")[i].amount;
        zx_products.push(o);
    }
}
else if (google_tag_manager["GTM-NFBSZKB"].dataLayer.get("google_tag_params.ecomm_pagetype") == "product") {
    AWIN.Tracking.MediaVentive.pagetype = "product";
    AWIN.Tracking.MediaVentive.productId = google_tag_manager["GTM-NFBSZKB"].dataLayer.get("google_tag_params.ecomm_prodid");
    AWIN.Tracking.MediaVentive.categoryId = google_tag_manager["GTM-NFBSZKB"].dataLayer.get("ecommerce.detail.actionField.list");
}
else if (google_tag_manager["GTM-NFBSZKB"].dataLayer.get("google_tag_params.ecomm_pagetype") == "category") {
    AWIN.Tracking.MediaVentive.pagetype = "category";
    AWIN.Tracking.MediaVentive.categoryId = google_tag_manager["GTM-NFBSZKB"].dataLayer.get("google_tag_params.ecomm_category");
}
else if (google_tag_manager["GTM-NFBSZKB"].dataLayer.get("google_tag_params.ecomm_pagetype") == "home") {
    AWIN.Tracking.MediaVentive.pagetype = "homepage";
}
```




# Plugin Code

<https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/mediaVentive/plugin.js>


``` javascript
AWIN.Tracking.MediaVentive = AWIN.Tracking.MediaVentive || {};
AWIN.Tracking.MediaVentive.url = AWIN.Tracking.MediaVentive.url || AWIN.sProtocol + "tm.ad-srv.net/tm/a/container/init/{containerId}.js";

(function ($m) {
    var pagetype = $m.pagetype || AWIN.Tracking.fetchZxParam('pagetype') || '';

    if (AWIN.Tracking.Sale) {
        pagetype = "order";
    } else if ("order" === pagetype.toLowerCase()) {
        AWIN.Tracking.Sale = {};
    }
    if ("undefined" === typeof $m.containerId) {
        return;
    }

    $m.fetchBasketData = function() {
        var products = AWIN.Tracking.fetchZxParam("products") || AWIN.Tracking.getBasketData();
        for (var i = 0; i < products.length; i++) {

            products[i].identifier = (typeof products[i].id !== "undefined") ? products[i].id : products[i].identifier;
            products[i].amount = (typeof products[i].price !== "undefined") ? products[i].price : products[i].amount;
            delete products[i].price;
            delete products[i].id;
        }
        return products;
    };
    $m.combineProducts = function(products) {
        if (typeof products === "string") {
            products = JSON.parse(products);
        }

        var combinedProducts = [];
        Array.from(products).forEach(function (p) {
            combinedProducts.push({
                id: p['identifier'],
                qty: parseInt(p['quantity']),
                price: parseFloat(parseFloat(p['amount']).toFixed(2))
            });
        });
        return combinedProducts;
    };

    $m.setNtmData = function($data) {
        var uniqueDataLayerName = "ntmData"+Math.floor(Math.random()*10e12);
        window[uniqueDataLayerName] = [
            $data,
            {
                'event':'ntmInit',
                't':new Date().getTime()
            }
        ];
        return uniqueDataLayerName;
    };

    var data = {};
    switch (pagetype) {
        case "homepage":
            data = {pageType: pagetype};
            break;
        case "search":
            data = {
                pageType: pagetype,
                searchTerm: $m.searchQuery || AWIN.Tracking.fetchZxParam('search_query')
            };
            break;
        case "category":
            data = {
                pageType: pagetype,
                categoryId: $m.category || AWIN.Tracking.fetchZxParam('category')
            };
            break;
        case "product":
            data = {
                pageType: pagetype,
                productId: $m.identifier || AWIN.Tracking.fetchZxParam('identifier'),
                productDetails: $m.productName || AWIN.Tracking.fetchZxParam('product_name'),
                categoryId: $m.category || AWIN.Tracking.fetchZxParam('category')
            };
            break;
        case "basket":
            data = {
                pageType: pagetype,
                products: $m.combineProducts($m.fetchBasketData())
            };
            break;
        case "order":
            var orderValue = AWIN.Tracking.fetchZxParam('total_amount') || AWIN.Tracking.Sale.amount;
            var transaction = AWIN.Tracking.fetchZxParam('transaction') || AWIN.Tracking.Sale.orderRef;
            var orderValueFloat = parseFloat(orderValue);

            data = {
                pageType: pagetype,
                checkoutStage:"",
                products: $m.combineProducts($m.fetchBasketData()),
                orderValue: isNaN(orderValueFloat) ? orderValue : orderValueFloat,
                transactionId: transaction
            };
            break;
        default:
            data = {
                pageType: "generic",
                pageName: $m.pageName || AWIN.Tracking.fetchZxParam('page_name')
            };
            break;
    }

    var url = $m.url.replace('{containerId}', $m.containerId)+'?'+
        AWIN.Tracking.buildQueryString({
            ntmData: $m.setNtmData(data),
            rnd: Math.floor(Math.random()*100000000)
        });
    AWIN.Tracking.scriptAppend(url, null, null, {"async":"true"})
})(AWIN.Tracking.MediaVentive);
```

