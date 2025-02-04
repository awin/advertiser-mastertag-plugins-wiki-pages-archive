# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

The Fanplayr2 plugin has different tags depending on the type of page
visited.

Plugin supports following `PAGETYPE`: home, product, checkout, basket,
category, generic

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | Fanplayr2         |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `SPECIFIC_FANPLAYR_CAMPAIGN_ID` with its real value.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.

If `CUSTOM_LOADER_SCRIPT` is provided by the publisher due to the lack
of data on the advertiser website, then a generic pagetype should apply
and complete configuration must be omitted.


``` javascript
AWIN.Tracking.Fanplayr2 = AWIN.Tracking.Fanplayr2 || {};
AWIN.Tracking.Fanplayr2.accountKey = "SPECIFIC_FANPLAYR_CAMPAIGN_ID";
AWIN.Tracking.Fanplayr2.loaderUrl = "CUSTOM_LOADER_SCRIPT";
AWIN.Tracking.Fanplayr2.pagetype = "PAGETYPE_IDENTIFIER";
```





``` javascript
AWIN.Tracking.Fanplayr2 = AWIN.Tracking.Fanplayr2 || {};
AWIN.Tracking.Fanplayr2.accountKey = "1adb3a0b6e1156244e15da30cdc0aa27";
AWIN.Tracking.Fanplayr2.loaderUrl = "https://cdn.fanplayr.com/customers/custom-loader/asda/loader.js";
AWIN.Tracking.Fanplayr2.pagetype = "generic";
```



(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

# Example Complete Setup

Example below is written on the basis that there is no PLT implemented
on the checkout page. Product data array is the same on the basket and
the checkout page.


``` javascript
AWIN.Tracking.Fanplayr2 = AWIN.Tracking.Fanplayr2 || {};
AWIN.Tracking.Fanplayr2.accountKey = "1adb3a0b6e1156244e15da30cdc0aa27";
AWIN.Tracking.Fanplayr2.pagetype = "generic";

if (dataLayer[0].pagePostType == 'frontpage') {
    AWIN.Tracking.Fanplayr2.pagetype = "home";
} else if (location.href.match(/product-category/i)) {
    AWIN.Tracking.Fanplayr2.pagetype = "category";
    AWIN.Tracking.Fanplayr2.categoryId = dataLayer[0].ecommerce.detail.categoryId;
    AWIN.Tracking.Fanplayr2.category = dataLayer[0].ecommerce.detail.category;
} else if (dataLayer[0].pagePostType == 'product') {
    AWIN.Tracking.Fanplayr2.pagetype = "product";
    AWIN.Tracking.Fanplayr2.categoryId = dataLayer[0].ecommerce.detail.categoryId;
    AWIN.Tracking.Fanplayr2.category = dataLayer[0].ecommerce.detail.products[0].category;
    AWIN.Tracking.Fanplayr2.identifier = dataLayer[0].ecommerce.detail.products[0].id;
    AWIN.Tracking.Fanplayr2.sku = dataLayer[0].ecommerce.detail.products[0].sku;
    AWIN.Tracking.Fanplayr2.price = dataLayer[0].ecommerce.detail.products[0].price;
    AWIN.Tracking.Fanplayr2.currency = "EUR";
    AWIN.Tracking.Fanplayr2.url = location.href;
    AWIN.Tracking.Fanplayr2.productName = dataLayer[0].ecommerce.detail.products[0].name;
    AWIN.Tracking.Fanplayr2.productImage = dataLayer[0].ecommerce.detail.products[0].imgUrl;
} else if (location.href.match(/cart/i)) {
    AWIN.Tracking.Fanplayr2.pagetype = "basket";
    AWIN.Tracking.Fanplayr2.currency = "EUR";

}

if (dataLayer[2].viewCartItems) {
    var zx_products = [];
    for (var i = 0; i < dataLayer[2].viewCartItems.length; i++) {
        zx_products.push({
        'id':dataLayer[2].viewCartItems[i].id,
        'sku':dataLayer[2].viewCartItems[i].sku,
        'quantity':dataLayer[2].viewCartItems[i].quantity,
        'price':dataLayer[2].viewCartItems[i].price,
        'name':dataLayer[2].viewCartItems[i].name}
        );
    }
}
```


# Plugin Code


``` javascript
AWIN.Tracking.Fanplayr2 = AWIN.Tracking.Fanplayr2 || {};
AWIN.Tracking.Fanplayr2.loaderUrl = AWIN.Tracking.Fanplayr2.loaderUrl || 'https://cdn.fanplayr.com/client/production/loader.js';
(function ($f) {
    var version = 3;
    var accountKey = $f.accountKey || AWIN.Tracking.fetchZxParam('accountKey');

    if (typeof accountKey === "undefined") {
        return;
    }

    var pagetype = $f.pagetype || AWIN.Tracking.fetchZxParam('pagetype') || 'generic';

    if (AWIN.Tracking.Sale) {
        pagetype = "checkout";
    } else {
        pagetype = pagetype.toLowerCase();
        if ("checkout" === pagetype) {
            AWIN.Tracking.Sale = {};
        }
    }

    $f.fetchBasketData = function() {
        var products = AWIN.Tracking.fetchZxParam('products') || AWIN.Tracking.getBasketData();

        if (typeof products === "string") {
            products = JSON.parse(products);
        }

        var mappedProducts = [];
        for (var i = 0; i < products.length; i++) {
            products[i].id = products[i].id || products[i].identifier;
            products[i].price = products[i].price || products[i].amount;
            mappedProducts.push({
                "id": products[i].id,
                "sku": products[i].sku,
                "price": products[i].price,
                "qty": products[i].quantity,
                "name": products[i].name
            });
        }
        return mappedProducts;
    };

    $f.getMappedPageType = function(page) {
        var mappedPageType = Object.entries({
            "basket":"cart",
            "category":"cat",
            "product":"prod",
            "home":"home",
            "generic":"page"
        })
        .filter(function(v){return (v[0]===page);});

        if (mappedPageType.length > 0){
            return mappedPageType[0][1];
        } else {
            return "";
        }
    };

    switch (pagetype) {
        case "checkout":
            if ( !window.fp_sales_orders ) {
                window.fp_sales_orders = {
                    version: version,
                    accountKey: accountKey,
                    storeDomain: document.domain,
                    data: {
                        orderId: AWIN.Tracking.fetchZxParam('transaction') || AWIN.Tracking.Sale.orderRef,
                        total: AWIN.Tracking.fetchZxParam('total_amount') || AWIN.Tracking.Sale.amount,
                        discount: $f.discount || AWIN.Tracking.fetchZxParam('discount') || "",
                        discountCode: AWIN.Tracking.fetchZxParam('voucher') || AWIN.Tracking.Sale.voucher || "",
                        currency: AWIN.Tracking.fetchZxParam('currency') || AWIN.Tracking.Sale.currency,
                        products : $f.fetchBasketData()
                    }
                };
                AWIN.Tracking.scriptAppend('https://cdn.fanplayr.com/client/production/fp_custom_orders.js', null, null, {"async": true});
            }
            break;
        case "basket":
        case "category":
        case "product":
        case "home":
        case "generic":
            var cartAction = "repeat";
            var mappedProducts = [];
            var lineItemCount = "";
            var numItems = "";
            var total = "";
            var discount = "";
            var discountCode = "";
            var currency = "";
            var gross = "";
            if (pagetype === "basket") {
                cartAction = "override";
                mappedProducts = $f.fetchBasketData();
                lineItemCount = mappedProducts.length;
                numItems = mappedProducts.reduce(
                    function(a,p){
                        var qty = parseInt(p.qty);
                        return a+(isNaN(qty)?0:qty);
                    },
                    0
                );
                total = mappedProducts.reduce(
                    function(a,p){
                        var qty=parseInt(p.qty),
                            price=parseFloat(p.price);
                        return a+((isNaN(qty) || isNaN(price))?0:qty*price);},
                    0
                );
                discount = $f.discount || AWIN.Tracking.fetchZxParam('discount');
                discountCode = $f.discountCode || AWIN.Tracking.fetchZxParam('discountCode');
                currency = $f.currency || AWIN.Tracking.fetchZxParam('currency');
                gross = $f.gross || AWIN.Tracking.fetchZxParam('gross') || total;
            }

            var categoryId = "";
            var categoryName = "";
            if (["category","product"].includes(pagetype)) {
                categoryId = $f.categoryId || AWIN.Tracking.fetchZxParam('categoryId');
                categoryName = $f.category || AWIN.Tracking.fetchZxParam('category');
            }

            var productIdentifier = "";
            var productPrice = "";
            var productUrl = "";
            var productSku = "";
            var productName = "";
            var productImage = "";
            if (pagetype === "product") {
                productIdentifier = $f.identifier || AWIN.Tracking.fetchZxParam('identifier');
                productPrice = $f.price || AWIN.Tracking.fetchZxParam('price');
                currency = $f.currency || AWIN.Tracking.fetchZxParam('currency');
                productUrl = $f.url || AWIN.Tracking.fetchZxParam('url');
                productSku = $f.sku || AWIN.Tracking.fetchZxParam('sku');
                productName = $f.productName || AWIN.Tracking.fetchZxParam('productName');
                productImage = $f.productImage || AWIN.Tracking.fetchZxParam('productImage');
            }

            var f = window.fanplayr = window.fanplayr || { _i:[] };
            f._i.push({
                version: version,
                accountKey: accountKey,
                applyToCartUrl: "",
                data: {
                    lineItemCount: lineItemCount,
                    numItems: numItems,
                    total: total,
                    gross: gross,
                    discount: discount,
                    discountCode: discountCode,
                    pageType: $f.getMappedPageType(pagetype),
                    categoryId: categoryId,
                    categoryName: categoryName,
                    productId: productIdentifier,
                    productName: productName,
                    productSku: productSku,
                    productPrice: productPrice,
                    productUrl: productUrl,
                    productImage: productImage,
                    currency: currency,
                    products : mappedProducts,
                    cartAction: cartAction
                }
            });

            AWIN.Tracking.scriptAppend(AWIN.Tracking.Fanplayr2.loaderUrl, null, null, {"async": true});
            break;
    }
})(AWIN.Tracking.Fanplayr2);
```

