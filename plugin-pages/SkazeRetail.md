
# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

Skaze Retail plugin has been developed for retail advertisers.
Implementation for travel advertisers is also available. For more
information please refer to Skaze Travel plugin.

The Skaze Retail plugin has different tags depending on the type of page
visited and requires providing custom data via variables described
below.

Plugin supports following `PAGETYPE`: productslist, product, basket.

Default Skaze API calls will be automatically added to all pages and
checkout page will be automatically detected if AWIN.Tracking.Sale tag
is implemented.

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | Skaze Retail      |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

## IMPORTANT:

advertiserId must be provided on every page for this plugin to work
(ideally defined once as a top level variable)

Page keys must be provided for product list, product and basket pages,
otherwsise the plugin will not work as expected.

Compatible page type keywords are: productslist, product, basket.

(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

# General Page Configuration

The code below goes into the plugin setup field in the tag management
form.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.

In order to implement plugin on all pages (excluding productslist,
product, basket) the below configuration is required:


``` javascript
//Object should be created in our configuration
AWIN.Tracking.skazeRetailer = AWIN.Tracking.skazeRetailer || {};
AWIN.Tracking.skazeRetailer.advertiserId =ADVERTISER_ID; //Assigned in Awin cofiguration
AWIN.Tracking.skazeRetailer.pageName = PAGE NAME; //Assigned in Awin configuration
```





``` javascript
AWIN.Tracking.skazeRetailer = AWIN.Tracking.skazeRetailer || {};
AWIN.Tracking.skazeRetailer.advertiserId = "1001";
AWIN.Tracking.skazeRetailer.pageName = "my home page";
```




## Basket Page

This plugin requires a lot of custom parameters unavailable from Awin
MasterTag, therefore it certain fields to be provided by the client on
their page.

Please refer to comments in the script for information about which
variables can be configured by us and which should be provided by the
client.

If a variable is not provided, it will be replaced with a empty text.


``` javascript
AWIN.Tracking.skazeRetailer = AWIN.Tracking.skazeRetailer || {};
AWIN.Tracking.skazeRetailer.pageName = PAGE_Name</code>;
AWIN.Tracking.skazeRetailer.advertiserId = ADVERTISER_ID</code>;
////fields below should be provided by the client
AWIN.Tracking.skazeRetailer.pageType = PAGE_KEY</code>;
AWIN.Tracking.skazeRetailer.basketId = BASKET_ID</code>;
AWIN.Tracking.skazeRetailer.basketValue = BASKET_VALUE</code>;
AWIN.Tracking.skazeRetailer.aw_products = PRODUCTS_ARRAY</code>;
```



Example:


``` javascript
AWIN.Tracking.skazeRetailer = AWIN.Tracking.skazeRetailer || {};
AWIN.Tracking.skazeRetailer.pageType = "basket";
AWIN.Tracking.skazeRetailer.pageName = "- my basket";
AWIN.Tracking.skazeRetailer.advertiserId = "1001";
AWIN.Tracking.skazeRetailer.basketId = "#001";
AWIN.Tracking.skazeRetailer.basketValue = "12.03";
AWIN.Tracking.skazeRetailer.aw_products = [];
//Plese reffer to the last section of this document
//for instructions about implementing products array
```




## Product Page

Product page requires data for a single product, as shown below.


``` javascript
AWIN.Tracking.skazeRetailer = AWIN.Tracking.skazeRetailer || {};
AWIN.Tracking.skazeRetailer.pageName = PAGE_Name;
AWIN.Tracking.skazeRetailer.advertiserId = ADVERTISER_ID;
//All fields below should be provided by the client
AWIN.Tracking.skazeRetailer.pageType = PAGE_KEY;
AWIN.Tracking.skazeRetailer.id = PRODUCT_ID;
AWIN.Tracking.skazeRetailer.name = PRODUCT NAME;
AWIN.Tracking.skazeRetailer.price = PRODUCT_PRICE;
AWIN.Tracking.skazeRetailer.salePrice = SALE_PRICE;
AWIN.Tracking.skazeRetailer.currency = CURRENCY;
AWIN.Tracking.skazeRetailer.category = CATEGORY;
AWIN.Tracking.skazeRetailer.subCategory = SUB_CATEGORY;
AWIN.Tracking.skazeRetailer.brand = PRODUCT_BRAND;
AWIN.Tracking.skazeRetailer.color = PRODUCT_COLOR;
AWIN.Tracking.skazeRetailer.size = PRODUCT_SIZE;
AWIN.Tracking.skazeRetailer.description = PRODUCT_DESCRIPTION;
AWIN.Tracking.skazeRetailer.imageUrl = PRODUCT_IMAGE_URL;
AWIN.Tracking.skazeRetailer.productUrl = PRODUCT_URL;
```



Example:


``` javascript
AWIN.Tracking.skazeRetailer = AWIN.Tracking.skazeRetailer || {};
AWIN.Tracking.skazeRetailer.pageType = "product";
AWIN.Tracking.skazeRetailer.pageName = "- Product";
AWIN.Tracking.skazeRetailer.advertiserId = "1001";
AWIN.Tracking.skazeRetailer.id = "0009991";
AWIN.Tracking.skazeRetailer.name = "T-Shirt";
AWIN.Tracking.skazeRetailer.price = "999.99";
AWIN.Tracking.skazeRetailer.salePrice = "99.00";
AWIN.Tracking.skazeRetailer.currency = "GBP";
AWIN.Tracking.skazeRetailer.category = "clothes";
AWIN.Tracking.skazeRetailer.subCategory = "small clothes";
AWIN.Tracking.skazeRetailer.brand = "Awin Brand";
AWIN.Tracking.skazeRetailer.color = "blue";
AWIN.Tracking.skazeRetailer.size = "S";
AWIN.Tracking.skazeRetailer.description = "my t-shirt description";
AWIN.Tracking.skazeRetailer.imageUrl = "image.gif";
AWIN.Tracking.skazeRetailer.productUrl = "product.html";
```




## Products List

Product page requires data for a single product, as shown below.


``` javascript
AWIN.Tracking.skazeRetailer = AWIN.Tracking.skazeRetailer || {};
AWIN.Tracking.skazeRetailer.pageName = PAGE_Name;
//all fields below should be provided by the client
AWIN.Tracking.skazeRetailer.pageType = PAGE_KEY;
AWIN.Tracking.skazeRetailer.aw_products = PRODUCTS_ARRAY;
```



Example:


``` javascript
AWIN.Tracking.skazeRetailer = AWIN.Tracking.skazeRetailer || {};
AWIN.Tracking.skazeRetailer.pageName = "- PRODUCTS";
//provided by the client
AWIN.Tracking.skazeRetailer.pageType = "productsList";
AWIN.Tracking.skazeRetailer.aw_products = [];
//Plese reffer to the last section of this document
//for instructions about implementing products array
```




## Checkout Page

The plugin will automatically detect if the user is located on the
checkout page if AWIN.Tracking.Sale variable is preset. However,
specifying the pageType variable will override this behaviour.

Order Id, order value, promo code (voucher code) and currency will be
populated based on the data recieved in AWIN.Tracking.Sale, however
other fields will need to be provided.


``` javascript
AWIN.Tracking.skazeRetailer = AWIN.Tracking.skazeRetailer || {};
//All fields below should be provided by the client
AWIN.Tracking.skazeRetailer.alreadyClient = IS_ALREADY_CLIENT;
AWIN.Tracking.skazeRetailer.emailMD5 = EMAIL_MD5;
AWIN.Tracking.skazeRetailer.emailSHA256 = EMAIL_SHA256;
AWIN.Tracking.skazeRetailer.phoneMD5 = PHONE_MD5;
AWIN.Tracking.skazeRetailer.phoneSHA256 = PHONE_SHA256;
AWIN.Tracking.skazeRetailer.aw_products = PRODUCTS_ARRAY;
```



Example:


``` javascript
AWIN.Tracking.skazeRetailer = AWIN.Tracking.skazeRetailer || {};
AWIN.Tracking.skazeRetailer.alreadyClient = "yes";
AWIN.Tracking.skazeRetailer.emailMD5 = "encrypted email";
AWIN.Tracking.skazeRetailer.emailSHA256 = "encrypted email";
AWIN.Tracking.skazeRetailer.phoneMD5 = "encrypted email";
AWIN.Tracking.skazeRetailer.phoneSHA256 = "encrypted email";
AWIN.Tracking.skazeRetailer.aw_products = [];
//Please reffer to the last section of this document
//to learn about implementing products array
```




# Implementing Products Array

Certain pages require list of products. As product details required by
this array are different to our standard product level tracking, this
needs to be provied via a separate array. Below is a structure of
products array with two products in a list.


``` javascript
//Products array should be provided by the client
AWIN.Tracking.skazeRetailer.aw_products = aw_products: [
{
id: "product-id1",
price:"product-price1",
salePrice:"product-salePrice1",
currency:"EUR",
name: "product-name1",
category: "product-category1",
subCategory: "product-subCategory1",
brand: "product-brand1",
color: "product-color1",
size: "product-size1",
qty: "product-quantity1"
},
{
id: "product-id2",
price:"product-price2",
salePrice:"product-salePrice2",
currency:"EUR",
name: "product-name2",
category: "product-category2",
subCategory: "product-subCategory1",
brand: "product-brand2",
color: "product-color2",
size: "product-size2",
qty: "product-quantity2"
}
];
```


## Plugin Code


``` javascript
AWIN.Tracking.skazeRetailer = AWIN.Tracking.skazeRetailer || {};
AWIN.Tracking.skazeRetailer.url = AWIN.Tracking.skazeRetailer.url || "//events.sk.ht/";

var event = {};

(function ($a) {
    $a.getBasketData = function ()
    {
        if (typeof $a.aw_products === "undefined") {
            return [];
        }

        return $a.aw_products.map(function(product) {
            product.id = product.id || "";
            product.price = product.price || "";
            product.salePrice = product.salePrice || "";
            product.currency = product.currency || "";
            product.name = product.name || "";
            product.category = product.category || "";
            product.subCategory = product.subCategory || "";
            product.brand= product.brand || "";
            product.color = product.color || "";
            product.size = product.size || "";
            product.qty = product.qty || "";
            return product;
        });
    };

    let urlWithParams = AWIN.Tracking.skazeRetailer.url + $a.advertiserId + "/lib.js";
    AWIN.Tracking.scriptAppend(urlWithParams, null, null, {async: "async"});

    var skaze = skaze || {};
    skaze.cmd = skaze.cmd || [];

    event = {
        name : $a.advertiserId + " " + $a.pageName || "",
        properties: {}
    };

    if (typeof $a.pageType !== "undefined" && typeof AWIN.Tracking.Sale === "undefined") {
        switch ($a.pageType.toLowerCase()) {
            case "productslist":
                event.properties = {
                    products: $a.getBasketData()
                };
                break;
            case "product":
                event.properties = {
                    id: $a.id || "",
                    name: $a.name || "",
                    price: $a.price || "",
                    salePrice: $a.salePrice || "",
                    currency: $a.currency || "",
                    category: $a.category || "",
                    subCategory: $a.subCategory || "",
                    brand: $a.brand || "",
                    color: $a.color || "",
                    size: $a.size || "",
                    description: $a.description || "",
                    imageUrl: $a.imageUrl || "",
                    url: $a.productUrl || "",
                };
                break;
            case "basket":
                event.properties = {
                    basketId: $a.basketId || "",
                    basketValue: $a.basketValue || "",
                    products: $a.getBasketData()
                };

                break;
        }
    } else if (typeof AWIN.Tracking.Sale !== "undefined") {
        event.properties = {
            alreadyClient: $a.alreadyClient || "",
            orderId: AWIN.Tracking.Sale.orderRef,
            orderValue: AWIN.Tracking.Sale.saleAmount,
            promoCode: AWIN.Tracking.Sale.voucher,
            currency: AWIN.Tracking.Sale.currency,
            emailMD5: $a.emailMD5 || "",
            emailSHA256: $a.emailSHA256 || "",
            phoneMD5: $a.phoneMD5 || "",
            phoneSHA256: $a.phoneSHA256 || "",
            products: $a.getBasketData()
        };
    }

    skaze.cmd.push(function() {
        skaze.init({ siteIdentifier : $a.advertiserId });
        skaze.pushEvent(event);
    });
})(AWIN.Tracking.skazeRetailer);
```


