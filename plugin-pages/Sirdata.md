
# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

The Sirdata plugin has different tags depending on the type of page
visited.

Plugin supports following `PAGETYPE`: category, product, basket, search,
checkout, generic

# Tag example

<https://js.sddan.com/cart.d?command_amount=8.40&pa=22143&si=1&su=1&u=https%3A%2F%2Fwww.tenvinilo.com%2Fcompra%2Fpedido%2F&r=https%3A%2F%2Fwww.tenvinilo.com%2Fvinilos-decorativos%2Fvinilo-nubes-de-lindas-texturas-7418>

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | Sirdata           |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `SPECIFIC_Sirdata_PROGRAM_ID` with its real value.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.


``` javascript
AWIN.Tracking.SirData = AWIN.Tracking.SirData || {};
AWIN.Tracking.SirData.advertiserId = "SPECIFIC_SirData_PROGRAM_ID";
AWIN.Tracking.SirData.pagetype = "PAGETYPE_IDENTIFIER";
```





``` javascript
AWIN.Tracking.SirData = AWIN.Tracking.SirData || {};
AWIN.Tracking.SirData.advertiserId = "22143";
AWIN.Tracking.SirData.pagetype = "generic";
```



(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

## Product Page

The plugin does not use the product scraper itself but you could use it
to fetch the ID if you prefer and supply it to the identifier config
variable.


``` javascript
AWIN.Tracking.SirData.identifier = "ID_OF_THE_PRODUCT";
AWIN.Tracking.SirData.category = "NAME_OF_CATEGORY";
```



Example:


``` javascript
AWIN.Tracking.SirData.identifier = document.getElementById('stickerRefCode').innerHTML;
```




## Category Page


``` javascript
AWIN.Tracking.SirData.category = "NAME_OF_CATEGORY";
```



Example:


``` javascript
AWIN.Tracking.SirData.category = google_tag_params.category;
```




## Search Results Page


``` javascript
AWIN.Tracking.SirData.searchQuery = "USER_SEARCH_TERMS";
```



Example:


``` javascript
AWIN.Tracking.SirData.searchQuery = google_tag_params.searchQ;
```




## Basket Page

Plugin requires basket value.

Example:


``` javascript
AWIN.Tracking.SirData.totalAmount = google_tag_params.basket.value;
```




## Checkout Page

Plugin automatically assigns the pagetype and retrieves the data if
<b>AWIN.Tracking.Sale</b> is present therefore it is not necessary to
add this part in configuration.

# Example Complete Setup


``` javascript

AWIN.Tracking.SirData = AWIN.Tracking.SirData || {};
AWIN.Tracking.SirData.advertiserId = "22143";
AWIN.Tracking.SirData.pagetype = "generic";

if (google_tag_params.pagetype == "product") {
    AWIN.Tracking.SirData.pagetype = "product";
    AWIN.Tracking.SirData.identifier = document.getElementById('stickerRefCode').innerHTML;
} else if (google_tag_params.pagetype == "cart") {
    AWIN.Tracking.SirData.pagetype = "basket";
    AWIN.Tracking.SirData.totalAmount = google_tag_params.basket.value;
} else if (google_tag_params.pagetype == "category") {
    AWIN.Tracking.SirData.pagetype = "category";
    AWIN.Tracking.SirData.category = google_tag_params.category;
} else if (google_tag_params.pagetype == "searchPage") {
    AWIN.Tracking.SirData.pagetype = "search";
    AWIN.Tracking.SirData.searchQuery =
    AWIN.Tracking.getQueryVarValue('searchInput', document.location.search.substring(1));
}
```


# Plugin code


``` javascript
AWIN.Tracking.SirData = AWIN.Tracking.SirData || {};
AWIN.Tracking.SirData.url = AWIN.Tracking.SirData.url || AWIN.sProtocol + "js.sddan.com";

(function ($s) {
    if ("undefined" === typeof $s.advertiserId) {
        return;
    }

    var pagetype = $s.pagetype || AWIN.Tracking.fetchZxParam('pagetype');

    if ("undefined" === typeof pagetype) {
        return;
    }

    if (AWIN.Tracking.Sale) {
        pagetype = "checkout";
    } else if ("checkout" === pagetype.toLowerCase()) {
        AWIN.Tracking.Sale = {};
    }

    var url = $s.url;
    var query = false;

    switch (pagetype.toLowerCase()) {
        case "product":
            url += "/product.d?" + AWIN.Tracking.buildQueryString({
                product_id: $s.identifier || AWIN.Tracking.fetchZxParam('identifier'),
                product_name: $s.productName || AWIN.Tracking.fetchZxParam('product_name'),
                product_price: $s.price || AWIN.Tracking.fetchZxParam('product_price')
            });
            query = true;
            break;
        case "search":
            url += "/LAL.d?" + AWIN.Tracking.buildQueryString({
                s: $s.searchQuery || AWIN.Tracking.fetchZxParam('search_query')
            });
            query = true;
            break;
        case "category":
            url += "/LAL.d?" + AWIN.Tracking.buildQueryString({
                cat_name: $s.category || AWIN.Tracking.fetchZxParam('category')
            });
            query = true;
            break;
        case "basket":
            url += "/cart.d?" + AWIN.Tracking.buildQueryString({
                command_amount: $s.totalAmount || AWIN.Tracking.fetchZxParam('total_amount')
            });
            query = true;
            break;
        case "checkout":
            url += "/order.d?" + AWIN.Tracking.buildQueryString({
                command_amount: AWIN.Tracking.fetchZxParam('total_amount') || AWIN.Tracking.Sale.amount,
                command_id: AWIN.Tracking.fetchZxParam('transaction') || AWIN.Tracking.Sale.orderRef,
                ht_paid: 1
            });
            query = true;
            break;
        default:
            url += "/LAL.d";
            break;
    }

    url += (query ? "&" : "?") + AWIN.Tracking.buildQueryString({
        pa: $s.advertiserId,
        si: 1,
        su: 1,
        u: document.location.href,
        r: document.referrer
    });

    AWIN.Tracking.scriptAppend(url);
})(AWIN.Tracking.SirData);
```

