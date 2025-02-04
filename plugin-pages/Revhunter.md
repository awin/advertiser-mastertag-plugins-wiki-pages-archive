
# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

The Revhunter plugin has different tags depending on the type of page
visited.

# Supported Pages

- Generic/Home Page
- Product Page
- Category Page
- Basket Page
- Checkout Page

# Configuration

Refer to the source code for more details.

Replace `"VALUE_PLACEHOLDERS"` with real values.

ID is a static value and, as written below, it should be
"c12c3786102a52387cae4913554fc52f".

## Home/Generic Page Configuration


``` javascript
AWIN.Tracking.Revhunter = AWIN.Tracking.Revhunter || {};
AWIN.Tracking.Revhunter.pagetype = "home";
AWIN.Tracking.Revhunter.id = "c12c3786102a52387cae4913554fc52f";
AWIN.Tracking.Revhunter.zoneId = "ZONE_ID";
```




## Category Page Configuration

The plugin does not use the data scraper itself but you could use it to
fetch the category if you prefer and supply it to the category config
variable.


``` javascript
AWIN.Tracking.Revhunter = AWIN.Tracking.Revhunter || {};
AWIN.Tracking.Revhunter.pagetype = "category";
AWIN.Tracking.Revhunter.id = "c12c3786102a52387cae4913554fc52f";
AWIN.Tracking.Revhunter.zoneId = "ZONE_ID";
AWIN.Tracking.Revhunter.category = "CATEGORY_ID";
```




## Product Page Configuration

The plugin does not use the product scraper itself but you could use it
to fetch the ID if you prefer and supply it to the identifier config
variable.


``` javascript
AWIN.Tracking.Revhunter = AWIN.Tracking.Revhunter || {};
AWIN.Tracking.Revhunter.pagetype = "product";
AWIN.Tracking.Revhunter.id = "c12c3786102a52387cae4913554fc52f";
AWIN.Tracking.Revhunter.zoneId = "ZONE_ID";
AWIN.Tracking.Revhunter.identifier = "PRODUCT_ID";
```




## Basket Page Configuration

The plugin requires product data (productIds, quantities and prices) on
the basket page. Data can be supplied to the plugin with the PLT form.

If the client doesn't have PLT implemented, please see below for an
example and "how-to" implement the PLT on our side.


``` javascript
AWIN.Tracking.Revhunter = AWIN.Tracking.Revhunter || {};
AWIN.Tracking.Revhunter.pagetype = "basket";
AWIN.Tracking.Revhunter.id = "c12c3786102a52387cae4913554fc52f";
AWIN.Tracking.Revhunter.zoneId = "ZONE_ID";
```




## Checkout Page Configuration

The plugin will automatically retrieve total amount from
AWIN.Tracking.Sale.amount and order reference from
AWIN.Tracking.Sale.orderRef.


``` javascript
AWIN.Tracking.Revhunter = AWIN.Tracking.Revhunter || {};
AWIN.Tracking.Revhunter.pagetype = "checkout";
AWIN.Tracking.Revhunter.id = "c12c3786102a52387cae4913554fc52f";
AWIN.Tracking.Revhunter.zoneId = "ZONE_ID";
```




## Example with PLT - made by Guilherme Terra


``` javascript
let revhunterPluginMap = {
    product: ["product", "1663"],
    category: ["category", "1664"],
    cart: ["basket", "1665"],
    checkout: ["checkout", "1666"],
    home: ["home", "1667"],
    other: ["generic", "1668"]
};

AWIN.Tracking.Revhunter = AWIN.Tracking.Revhunter || {};
AWIN.Tracking.Revhunter.id = "c12c3786102a52387cae4913554fc52f";


var pageType = "";
if (AWIN.Tracking.Sale == undefined) {
    pageType = google_tag_params.ecomm_pagetype;
} else {
    pageType = "checkout";
};

AWIN.Tracking.Revhunter.pagetype = revhunterPluginMap[pageType][0];
AWIN.Tracking.Revhunter.zoneId = revhunterPluginMap[pageType][1];

if (AWIN.Tracking.Revhunter.pagetype === "product") {
    AWIN.Tracking.Revhunter.identifier = google_tag_params.ecomm_prodid;
    console.log("product page");
} else if (AWIN.Tracking.Revhunter.pagetype === "category") {
    AWIN.Tracking.Revhunter.category = google_tag_params.ecomm_category;
    console.log("category page");
} else if (AWIN.Tracking.Revhunter.pagetype === "basket") {

    var plt = "";

    var productPrices = document.querySelectorAll("td.cart_total > span");
    var prices = [];
    for (var index = 0; index < productPrices.length; index++) {
        prices.push(productPrices[index].innerText.match(/\d+(,\d+)?/)[0].replace(',', '.'));
    }

    var productQuantities = document.querySelectorAll("td.cart_quantity.text-center > div > input.cart_quantity_input.form-control.text-center");
    var quantities = [];
    for (var index = 0; index < productQuantities.length; index++) {
        quantities.push(productQuantities[index].value);
    }

    var productIds = google_tag_params.ecomm_prodid;
    var ids = [];
    for (var index = 0; index < productIds.length; index++) {
        ids.push(productIds[index]);
        quantities.push(productIds[index]);
    }

    for (var i = 0; i < ids.length; i++) {

        plt += "AW:P|19605|undefined|" +
            ids[i] + "|" +
            "undefined" + "|" +
            prices[i]/quantities[i] + "|" +
            quantities[i] + "|" +
            ids[i] + "|" +
            "DEFAULT|" +
            "undefined" + "\n";
    }
    var basketForm = document.createElement('form');
    basketForm.setAttribute('style', 'display:none');
    basketForm.setAttribute('name', 'basket_form');

    var basketTextArea = document.createElement('textarea');
    basketTextArea.setAttribute('wrap', 'physical');
    basketTextArea.setAttribute('id', 'aw_basket');
    basketTextArea.value = plt;

    basketForm.appendChild(basketTextArea);
    document.getElementsByTagName('body')[0].appendChild(basketForm);
}
```




# Plugin Source Code


``` javascript
AWIN.Tracking.Revhunter = AWIN.Tracking.Revhunter || {};
AWIN.Tracking.Revhunter.url = AWIN.Tracking.Revhunter.url || AWIN.sProtocol + "rev.owltrack.com/d/owljs.php";

(function ($r) {
    if ("undefined" === typeof $r.id || "undefined" === typeof $r.zoneId) {
        return;
    }

    var pagetype = $r.pagetype;

    if ("undefined" === typeof pagetype) {
        pagetype = (AWIN.Tracking.Sale) ? "checkout" : "generic";
    } else {
        pagetype = pagetype.toLowerCase();
        if ("checkout" === pagetype) {
            AWIN.Tracking.Sale = AWIN.Tracking.Sale || {};
        }
    }

    var basketValue = function(basketData) {
        return basketData
            .map(function(v) {return parseFloat(v.quantity)*parseFloat(v.price);})
            .reduce(function (a,b) {return a+b;},0);
    };

    var insNode  = document.createElement('ins');
    insNode.setAttribute('data-revive-id', $r.id);
    insNode.setAttribute('data-revive-zoneid', $r.zoneId);

    switch (pagetype) {
        case 'category':
            insNode.setAttribute('data-revive-categoryid', $r.category);
            break;
        case 'product':
            insNode.setAttribute('data-revive-productid', $r.identifier);
            break;
        case 'basket':
            var basketData = AWIN.Tracking.getBasketData();
            var products = basketData.map(function(v) {return v.id}).join(',');
            var counts = basketData.map(function(v) {return v.quantity}).join(',');

            insNode.setAttribute('data-revive-basket', basketValue(basketData));
            insNode.setAttribute('data-revive-products', products);
            insNode.setAttribute('data-revive-counts', counts);
            break;
        case 'checkout':
            insNode.setAttribute('data-revive-basket', AWIN.Tracking.Sale.amount);
            insNode.setAttribute('data-revive-order', AWIN.Tracking.Sale.orderRef);
            break;
    }

    AWIN.Tracking.getScriptAppendNode().appendChild(insNode);
    AWIN.Tracking.scriptAppend($r.url, null, null, {async: "async"});
})(AWIN.Tracking.Revhunter);
```



== Related JIRA Ticket ==
[PROD-8881](https://jira.awin.com/browse/PROD-8881)