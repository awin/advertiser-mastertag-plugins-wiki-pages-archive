
## Description

The purpose of the eperflex plugin is to fire eperflex pixels.
Eperflex is a retargeting solution by emailing. This technology includes
a targeting tool crossover, non intrusive and completely anonymous,
which allows an advertiser to find potential customers looking to
consult a product on his website and to send them a personalized and
dedicated offer by email. This technology offers multiple scenarios,
retargeting animation programs and promotional campaigns
eperflex domain is mail-reflex.com

## Integration requirements

- Dwin tag to be shown unconditionally across all pages :
- 7 page types are available :
  \* home page
  \* category page
  \* product page
  \* basket page
  \* checkout page
  \* search page
  \* registration page

## Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

### Template


``` javascript

AWIN.Tracking.Eperflex = AWIN.Tracking.Eperflex || {};
AWIN.Tracking.Eperflex.id = "SPECIFIC_EPERFLEX_ID";

//activation of pages
AWIN.Tracking.Eperflex.home_retargetingOn = 1;
AWIN.Tracking.Eperflex.category_retargetingOn = 1;
AWIN.Tracking.Eperflex.product_retargetingOn = 1;
AWIN.Tracking.Eperflex.basket_retargetingOn = 1;
AWIN.Tracking.Eperflex.checkout_retargetingOn = 1;
AWIN.Tracking.Eperflex.checkout_excludeOn = 1; // to fire exclude pixel on checkout page
AWIN.Tracking.Eperflex.search_retargetingOn = 1;
AWIN.Tracking.Eperflex.registration_retargetingOn = 1;

//identification of page types & define variables
AWIN.Tracking.Zx = AWIN.Tracking.Zx || {};
if (window.location.href.indexOf("www.example.com/checkout") > -1) {
    AWIN.Tracking.Zx.pageType = 'checkout';
//if zx_total_amount is already define - do nothing else, define this variable :
//AWIN.Tracking.Zx.checkout_totalAmount = ID_ON_PAGE_(JS);
} else if (window.location.href.indexOf("www.example.com/basket") > -1) {
    AWIN.Tracking.Zx.pageType = 'basket';
//if zx_products is already define - do nothing. else, define this variable :
//AWIN.Tracking.Zx.basket_products = ARRAY_OF_PRODUCTS(JSON);
} else if (window.location.href.indexOf("www.example.com/product") > -1) {
    AWIN.Tracking.Zx.pageType = 'product';
//if zx_products is already define - do nothing. else, define this variable :
//AWIN.Tracking.Zx.product_productId = ID_ON_PAGE_(JS);
////this ID must match with datafeed
} else if (window.location.href.indexOf("www.example.com/category") > -1) {
    AWIN.Tracking.Zx.pageType = 'category';
//if zx_category is already define - do nothing. else, define this variable :
//AWIN.Tracking.Zx.category_categoryId = ID_ON_PAGE_(JS);
// this Name or ID must match with datafeed
} else if (window.location.href.indexOf("www.example.com") > -1) {
    AWIN.Tracking.Zx.pageType = 'home';
}
```




### Example


If the plugin is activated with this code :


``` javascript

AWIN.Tracking.Eperflex = AWIN.Tracking.Eperflex || {};
AWIN.Tracking.Eperflex.id = "550";

//activation of pages
AWIN.Tracking.Eperflex.home_retargetingOn = 1;
AWIN.Tracking.Eperflex.category_retargetingOn = 1;
AWIN.Tracking.Eperflex.product_retargetingOn = 1;
AWIN.Tracking.Eperflex.basket_retargetingOn = 1;
AWIN.Tracking.Eperflex.checkout_retargetingOn = 1;
AWIN.Tracking.Eperflex.checkout_excludeOn = 1;


//identification of page types & define variables
AWIN.Tracking.Zx = AWIN.Tracking.Zx || {};
if (window.location.href.indexOf("www.monsite.com/checkout") > -1) {
    AWIN.Tracking.Zx.pageType = 'checkout';
AWIN.Tracking.Zx.checkout_totalAmount = PRICE;
} else if (window.location.href.indexOf("www.monsite.com/basket") > -1) {
    AWIN.Tracking.Zx.pageType = 'basket';
AWIN.Tracking.Zx.basket_products = PRODUCT_LIST;
} else if (window.location.href.indexOf("www.monsite.com/product") > -1) {
    AWIN.Tracking.Zx.pageType = 'product';
AWIN.Tracking.Zx.product_productId = PRODUCT_ID;
} else if (window.location.href.indexOf("www.monsite.com/category") > -1) {
    AWIN.Tracking.Zx.pageType = 'category';
AWIN.Tracking.Zx.category_categoryId = CATEGORY_NAME;
} else if (window.location.href.indexOf("www.monsite.com") > -1) {
    AWIN.Tracking.Zx.pageType = 'home';
}

// Example of PRODUCT_LIST
bproducts = [{
    "identifier": "00",
    "amount": "00.00",
    "currency": "EUR",
    "quantity": "00" // WARNING : must be a String to avoid errors
}];
```



Then the dwin mastertag will fire 6 pixels :
**Home page** :


``` text
http://email-reflex.com/tags/target.php?source=550
```



**Category page**


``` text
http://email-reflex.com/tags/categorie.php?source=550&cid=Pieces_Auto
```



**Product page**


``` text
http://email-reflex.com/tags/target.php?source=550&pid=15361441
```



**Basket page**


``` text
http://email-reflex.com/tags/cart.php?source=550&p=%5B%5B9900CHABEIGE%2C129%5D%2C%5B1030101GRIS%2C27.3%5D%5D
after decode :
http://email-reflex.com/tags/cart.php?source=550&p=[[9900CHABEIGE,129],[1030101GRIS,27.3|9900CHABEIGE,129],[1030101GRIS,27.3]]
```



**Checkout page** : 2 pixels


``` text
http://email-reflex.com/tags/sell.php?source=500&amount=95.90
http://email-reflex.com/tags/exclude.php?source=500
```


