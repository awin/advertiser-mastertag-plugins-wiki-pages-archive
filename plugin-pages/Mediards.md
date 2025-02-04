
# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

The Mediards plugin has different tags depending on the type of page
visited.

Plugin supports following `PAGETYPE`: home, product, checkout, basket,
category, search, generic

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | Mediards          |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `SPECIFIC_Mediards_CAMPAIGN_ID` with its real value.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.


``` javascript
AWIN.Tracking.Mediards = AWIN.Tracking.Mediards || {};
AWIN.Tracking.Mediards.campaignId = "SPECIFIC_Mediards_CAMPAIGN_ID";
AWIN.Tracking.Mediards.pagetype = "PAGETYPE_IDENTIFIER";
```





``` javascript
AWIN.Tracking.Mediards = AWIN.Tracking.Mediards || {};
AWIN.Tracking.Mediards.campaignId = "9161";
AWIN.Tracking.Mediards.pagetype = "generic";
```



(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

## Product Page

The plugin does not use the product scraper itself but you could use it
to fetch the ID if you prefer and supply it to the identifier config
variable.


``` javascript
AWIN.Tracking.Mediards.identifier = "ID_OF_THE_PRODUCT";
AWIN.Tracking.Mediards.category = "NAME_OF_CATEGORY";
AWIN.Tracking.Mediards.amount = "PRODUCT_PRICE";
```



Example:


``` javascript
AWIN.Tracking.Mediards.identifier = google_tag_params.prodid[0];
AWIN.Tracking.Mediards.category = google_tag_params.prodCategory[0];
AWIN.Tracking.Mediards.amount = google_tag_params.prodPrice[0];
```




## Category Page


``` javascript
AWIN.Tracking.Mediards.category = "NAME_OF_CATEGORY";
```



Example:


``` javascript
AWIN.Tracking.Mediards.category = google_tag_params.category;
```




## Search Results Page


``` javascript
AWIN.Tracking.Mediards.search_term = "USER_SEARCH_TERMS";
```



Example:


``` javascript
AWIN.Tracking.Mediards.search_term = google_tag_params.searchQ;
```




## Basket Page

Plugin requires product data (productIds, productPrice, productQuantity)
on the basket page. Data can be supplied to the plugin with array of
products (zx_products) or with the PLT form.

Example:


``` javascript
if (dataLayer[2].viewCartItems) {
    var zx_products = [];
    for (var i = 0; i < dataLayer[2].viewCartItems.length; i++) {
        zx_products.push({
        'identifier':dataLayer[2].viewCartItems[i].sku,
        'quantity':dataLayer[2].viewCartItems[i].quantity,
        'amount':dataLayer[2].viewCartItems[i].price});
    }
}
```




## Checkout Page

Plugin requires product data (productIds, productPrice, productQuantity)
on the checkout page. If client has Product Level Tracking Implemented
on the checkout page, data will be retrieved automatically. If PLT is
not implemented, data can be supplied to the plugin with array of
products (zx_products).

Example:


``` javascript
if (dataLayer[2].viewCheckoutItems) {
    var zx_products = [];
    for (var i = 0; i < dataLayer[2].viewCheckoutItems.length; i++) {
        zx_products.push({
        'identifier':dataLayer[2].viewCheckoutItems[i].sku,
        'quantity':dataLayer[2].viewCheckoutItems[i].quantity,
        'amount':dataLayer[2].viewCheckoutItems[i].price});
    }
}
```




# Example Complete Setup

Example below is written on the basis that there is no PLT implemented
on the checkout page. Product data array is the same on the basket and
the checkout page.


``` javascript
AWIN.Tracking.Mediards = AWIN.Tracking.Mediards || {};
AWIN.Tracking.Mediards.campaignId = "9161";
AWIN.Tracking.Mediards.pagetype = "generic";

if (AWIN.Tracking.Sale) {
    AWIN.Tracking.Mediards.pagetype = "checkout";
} else if (google_tag_params.pagetype == "cart") {
    AWIN.Tracking.Mediards.pagetype = "basket";
} else if (google_tag_params.pagetype == "product") {
    AWIN.Tracking.Mediards.pagetype = "product";
    AWIN.Tracking.Mediards.identifier = google_tag_params.prodid[0];
    AWIN.Tracking.Mediards.category = google_tag_params.prodCategory[0];
    AWIN.Tracking.Mediards.amount = google_tag_params.prodPrice[0];
} else if (google_tag_params.pagetype == "category") {
    AWIN.Tracking.Mediards.pagetype = "category";
    AWIN.Tracking.Mediards.category = google_tag_params.category;
} else if (google_tag_params.pagetype == "home") {
    AWIN.Tracking.Mediards.pagetype = "home";
} else if (google_tag_params.pagetype == "searchPage") {
    AWIN.Tracking.Mediards.pagetype = "search";
    AWIN.Tracking.Mediards.search_tearm = google_tag_params.searchQ;
}

if (dataLayer[2].viewCartItems) {
    var zx_products = [];
    for (var i = 0; i < dataLayer[2].viewCartItems.length; i++) {
        zx_products.push({
        'identifier':dataLayer[2].viewCartItems[i].sku,
        'quantity':dataLayer[2].viewCartItems[i].quantity,
        'amount':dataLayer[2].viewCartItems[i].price});
    }
}
```


# Plugin Code


``` javascript
AWIN.Tracking.Mediards = AWIN.Tracking.Mediards || {};
AWIN.Tracking.Mediards.url = AWIN.Tracking.Mediards.url ||
AWIN.sProtocol + "tr.mediards.de/?";

(function ($a) {
    var pagetype = AWIN.Tracking.fetchZxParam("pagetype") || $a.pagetype;
    var url = "";
    window.extref = AWIN.Tracking.buildQueryString({extref: document.location.href});

    if (typeof pagetype === "undefined") {
        return;
    }

    $a.fetchBasketData = function () {
        var products = AWIN.Tracking.fetchZxParam("products") || AWIN.Tracking.getBasketData();
        if (typeof products === "string") {
            products = JSON.parse(products);
        }
        for (var i = 0; i < products.length; i++) {
            products[i].identifier = (typeof products[i].id !== "undefined") ? products[i].id : products[i].identifier;
            products[i].amount = (typeof products[i].price !== "undefined") ? products[i].price : products[i].amount;
            delete products[i].price;
            delete products[i].id;
        }

        return products;
    };

    $a.getTotalAmount = function (products) {
        var total_amount = 0;
        for (var i = 0; i < products.length; i++) {
            total_amount = total_amount + (parseFloat(products[i].amount) * parseInt(products[i].quantity));
        }

        return total_amount;
    };

    $a.getProductIds = function (products) {
        var ids = "";
        for (var i = 0; i < products.length; i++) {
            ids += (ids === "") ? products[i].identifier : "," + products[i].identifier;
        }

        return ids;
    };


    switch (pagetype.toLowerCase()) {
        case "home":
            url = AWIN.Tracking.buildQueryString({
                type: "0",
                cid: $a.campaignId,
                language: AWIN.Tracking.fetchZxParam("language") || $a.language,
                extref: document.location.href
            });
            break;
        case "product":
            url = AWIN.Tracking.buildQueryString({
                type: "1",
                cid: $a.campaignId,
                language: AWIN.Tracking.fetchZxParam("language") || $a.language,
                productid: AWIN.Tracking.fetchZxParam("identifyer") || $a.identifier,
                category: AWIN.Tracking.fetchZxParam("category") || $a.category,
                price: AWIN.Tracking.fetchZxParam("amount") || $a.amount,
                curr: AWIN.Tracking.fetchZxParam("currency") || $a.currency,
                extref: document.location.href
            });
            break;
        case "checkout":
            var products = $a.fetchBasketData();
            url = AWIN.Tracking.buildQueryString({
                type: "2",
                cid: $a.campaignId,
                language: AWIN.Tracking.fetchZxParam("language") || $a.language,
                productids: $a.getProductIds(products),
                salecode: AWIN.Tracking.fetchZxParam("code") || AWIN.Tracking.Sale.code,
                price: $a.getTotalAmount($a.fetchBasketData()),
                curr: AWIN.Tracking.fetchZxParam("currency") || AWIN.Tracking.Sale.currency,
                extref: document.location.href
            });
            break;
        case "basket":
            var products = $a.fetchBasketData();
            url = AWIN.Tracking.buildQueryString({
                type: "4",
                cid: $a.campaignId,
                language: AWIN.Tracking.fetchZxParam("language") || $a.language,
                basket: $a.getProductIds(products),
                price: $a.getTotalAmount($a.fetchBasketData()),
                curr: AWIN.Tracking.fetchZxParam("currency") || $a.currency,
                extref: document.location.href
            });
            break;
        case "category":
            var products = $a.products || $a.fetchBasketData("products");
            url = AWIN.Tracking.buildQueryString({
                type: "3",
                cid: $a.campaignId,
                language:AWIN.Tracking.fetchZxParam("language") || $a.language,
                results: $a.getProductIds(products),
                category: AWIN.Tracking.fetchZxParam("category") || $a.category,
                extref: document.location.href
            });
            break;
        case "search":
            var products = $a.products || $a.fetchBasketData("products");
            url = AWIN.Tracking.buildQueryString({
                type: "5",
                cid: $a.campaignId,
                language: AWIN.Tracking.fetchZxParam("language") || $a.language,
                query: AWIN.Tracking.fetchZxParam("search_query") || $a.search_term,
                results: $a.getProductIds(products),
                extref: document.location.href
            });
            break;
        case "generic":
            url = AWIN.Tracking.buildQueryString({
                type: "10",
                cid: $a.campaignId,
                language: AWIN.Tracking.fetchZxParam("language") || $a.language,
                extref: document.location.href
            });
            break;
    }

    AWIN.Tracking.scriptAppend(AWIN.Tracking.Mediards.url + url);
})(AWIN.Tracking.Mediards);
```

