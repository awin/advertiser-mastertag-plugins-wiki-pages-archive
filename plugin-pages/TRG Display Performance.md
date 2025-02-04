# CURRENT STATUS

Provider confirmed this plugin is not required anymore. Reference:
<https://jira.awin.com/browse/PROD-10004>

# Integration requirements

The Dwin1 tag needs to be displayed on these pages:

- generic
- homepage
- category
- product
- basket
- order
- search

# Plugin setup code

(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

## Generic Page


``` javascript
AWIN.Tracking.TRGDisplayPerformance = AWIN.Tracking.TRGDisplayPerformance || {};
AWIN.Tracking.TRGDisplayPerformance.containerId = "CONTAINER_ID";
AWIN.Tracking.TRGDisplayPerformance.pagetype = "generic"; // "generic" or undefined
AWIN.Tracking.TRGDisplayPerformance.pageName = "PAGENAME_ID"; // OPTIONAL
```




## Home Page


``` javascript
AWIN.Tracking.TRGDisplayPerformance = AWIN.Tracking.TRGDisplayPerformance || {};
AWIN.Tracking.TRGDisplayPerformance.containerId = "CONTAINER_ID";
AWIN.Tracking.TRGDisplayPerformance.pagetype = "homepage";
```




## Category Page


``` javascript
AWIN.Tracking.TRGDisplayPerformance = AWIN.Tracking.TRGDisplayPerformance || {};
AWIN.Tracking.TRGDisplayPerformance.containerId = "CONTAINER_ID";
AWIN.Tracking.TRGDisplayPerformance.pagetype = "category";
AWIN.Tracking.TRGDisplayPerformance.category = "CATEGORY_ID";
```




## Product Page


``` javascript
AWIN.Tracking.TRGDisplayPerformance = AWIN.Tracking.TRGDisplayPerformance || {};
AWIN.Tracking.TRGDisplayPerformance.containerId = "CONTAINER_ID";
AWIN.Tracking.TRGDisplayPerformance.pagetype = "product";
AWIN.Tracking.TRGDisplayPerformance.identifier = "PRODUCT_ID";
AWIN.Tracking.TRGDisplayPerformance.productName = "PRODUCT_NAME"; //OPTIONAL
AWIN.Tracking.TRGDisplayPerformance.category = "PRODUCT_CATEGORY"; //OPTIONAL
```




## Basket Page


``` javascript
AWIN.Tracking.TRGDisplayPerformance = AWIN.Tracking.TRGDisplayPerformance || {};
AWIN.Tracking.TRGDisplayPerformance.containerId = "CONTAINER_ID";
AWIN.Tracking.TRGDisplayPerformance.pagetype = "basket";
```




## Order Page


``` javascript
AWIN.Tracking.TRGDisplayPerformance = AWIN.Tracking.TRGDisplayPerformance || {};
AWIN.Tracking.TRGDisplayPerformance.containerId = "CONTAINER_ID";
AWIN.Tracking.TRGDisplayPerformance.pagetype = "order";
```




## Search Page


``` javascript
AWIN.Tracking.TRGDisplayPerformance = AWIN.Tracking.TRGDisplayPerformance || {};
AWIN.Tracking.TRGDisplayPerformance.containerId = "CONTAINER_ID";
AWIN.Tracking.TRGDisplayPerformance.pagetype = "search";
AWIN.Tracking.TRGDisplayPerformance.searchQuery = "SEARCH_QUERY";
```




# Plugin Code


``` javascript
AWIN.Tracking.TRGDisplayPerformance = AWIN.Tracking.TRGDisplayPerformance || {};
AWIN.Tracking.TRGDisplayPerformance.url = AWIN.Tracking.TRGDisplayPerformance.url || AWIN.sProtocol + "tm.ad-srv.net/tm/a/container/init/{containerId}.js";

(function ($t) {
    try {
        if (typeof $t.containerId === "undefined") {
            return;
        }

        $t.url = $t.url.replace("{containerId}", $t.containerId);

        if (typeof $t.pagetype === "undefined") {
            $t.pagetype = "generic";
        }

        let pagetype = $t.pagetype.toLowerCase();

        if (AWIN.Tracking.Sale) {
            pagetype = "order";
        } else if ("order" === pagetype) {
            AWIN.Tracking.Sale = {};
        }

        $t.fetchBasketData = function() {
            let basketData = [],
                products = AWIN.Tracking.getBasketData();
            for (var i = 0; i < products.length; i++) {
                basketData.push({
                    "id": products[i].id,
                    "qty": products[i].quantity,
                    "price": products[i].price
                });
            }
            return basketData;
        };

        let pageData = [],
            r = "ntmData"+Math.floor(Math.random()*10e12);
        window[r] = [];
        switch (pagetype) {
            case "homepage":
                pageData = {
                    pageType: pagetype,
                };
                break;
            case "category":
                pageData = {
                    pageType: pagetype,
                    categoryId: $t.category
                };
                break;
            case "product":
                pageData = {
                    pageType: pagetype,
                    productId: $t.identifier
                };
                if (typeof $t.productName !== "undefined") pageData.productDetails = $t.productName;
                if (typeof $t.category !== "undefined") pageData.categoryId = $t.category;
                break;
            case "basket":
                pageData = {
                    pageType: pagetype,
                    products: $t.fetchBasketData()
                };
                break;
            case "order":
                pageData = {
                    pageType: pagetype,
                    products: $t.fetchBasketData(),
                    orderValue: AWIN.Tracking.Sale.amount,
                    transactionId: AWIN.Tracking.Sale.orderRef
                };
                break;
            case "search":
                pageData = {
                    pageType: pagetype,
                    searchTerm: $t.searchQuery
                };
                break;
            case "generic":
            default:
                pageData = {
                    pageType: pagetype,
                    pageName: $t.pageName || ''
                };
                break;
        }
        window[r].push(pageData);
        window[r].push({"event":"ntmInit","t":new Date().getTime()});

        let queryObject = {};
        if (r != "ntmData") {
            queryObject.ntmData = r;
        }
        queryObject.rnd = Math.floor(Math.random()*100000000);

        AWIN.Tracking.scriptAppend(
            $t.url + "?" + AWIN.Tracking.buildQueryString(queryObject),
            false,
            false,
            {"async": true}
        );
    } catch (e) {
        console.log(e);
    }
})(AWIN.Tracking.TRGDisplayPerformance);
```


# Repository Code

<https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/TRGDisplayPerformance/plugin.js>

# JIRA TICKET

<https://jira.awin.com/browse/PROD-8558>