
# Description

The purpose of the zRTB plugin is to fire mediamath pixels.
Mediamath is a Demand-Side platform. A DSP is a system that allows
buyers of digital advertising inventory to manage multiple ad exchange
and data exchange accounts through one interface
This platform is used by Real-time Bidding actors. RTB is a means by
which advertising inventory is bought and sold on a per-impression
basis, via programmatic instantaneous auction, similar to financial
markets)
Mediamath domain is mathtag.com

# Integration requirements

- Dwin tag to be shown unconditionally across all pages :
- 7 page types are available are :
  \* home page
  \* category page
  \* product page
  \* basket page
  \* checkout page
  \* search page
  \* registration page

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

## Template


``` javascript
AWIN.Tracking.ZRTB = AWIN.Tracking.ZRTB || {};

//activation of pages
AWIN.Tracking.ZRTB.home_retargetingOn = 1;
AWIN.Tracking.ZRTB.category_retargetingOn = 1;
AWIN.Tracking.ZRTB.product_retargetingOn = 1;
AWIN.Tracking.ZRTB.basket_retargetingOn = 1;
AWIN.Tracking.ZRTB.checkout_retargetingOn = 1;
AWIN.Tracking.ZRTB.search_retargetingOn = 1;
AWIN.Tracking.ZRTB.registration_retargetingOn = 1;

//define merchantIDs
AWIN.Tracking.ZRTB.merchantId1 = "ID";
AWIN.Tracking.ZRTB.merchantId2 = "ID";
AWIN.Tracking.ZRTB.merchantId3 = "ID";
AWIN.Tracking.ZRTB.merchantId4 = "ID";
AWIN.Tracking.ZRTB.merchantId5 = "ID";

//define pageIDs
AWIN.Tracking.ZRTB.home_mediamathId1 = "ID";
AWIN.Tracking.ZRTB.home_mediamathId2 = "ID";
AWIN.Tracking.ZRTB.home_mediamathId3 = "ID";
AWIN.Tracking.ZRTB.home_mediamathId4 = "ID";
AWIN.Tracking.ZRTB.home_mediamathId5 = "ID";

AWIN.Tracking.ZRTB.category_mediamathId1 = "ID";
AWIN.Tracking.ZRTB.category_mediamathId2 = "ID";
AWIN.Tracking.ZRTB.category_mediamathId3 = "ID";
AWIN.Tracking.ZRTB.category_mediamathId4 = "ID";
AWIN.Tracking.ZRTB.category_mediamathId5 = "ID";

AWIN.Tracking.ZRTB.product_mediamathId1 = "ID";
AWIN.Tracking.ZRTB.product_mediamathId2 = "ID";
AWIN.Tracking.ZRTB.product_mediamathId3 = "ID";
AWIN.Tracking.ZRTB.product_mediamathId4 = "ID";
AWIN.Tracking.ZRTB.product_mediamathId5 = "ID";

AWIN.Tracking.ZRTB.basket_mediamathId1 = "ID";
AWIN.Tracking.ZRTB.basket_mediamathId2 = "ID";
AWIN.Tracking.ZRTB.basket_mediamathId3 = "ID";
AWIN.Tracking.ZRTB.basket_mediamathId4 = "ID";
AWIN.Tracking.ZRTB.basket_mediamathId5 = "ID";

AWIN.Tracking.ZRTB.checkout_mediamathId1 = "ID";
AWIN.Tracking.ZRTB.checkout_mediamathId2 = "ID";
AWIN.Tracking.ZRTB.checkout_mediamathId3 = "ID";
AWIN.Tracking.ZRTB.checkout_mediamathId4 = "ID";
AWIN.Tracking.ZRTB.checkout_mediamathId5 = "ID";

AWIN.Tracking.ZRTB.search_mediamathId1 = "ID";
AWIN.Tracking.ZRTB.search_mediamathId2 = "ID";
AWIN.Tracking.ZRTB.search_mediamathId3 = "ID";
AWIN.Tracking.ZRTB.search_mediamathId4 = "ID";
AWIN.Tracking.ZRTB.search_mediamathId5 = "ID";

AWIN.Tracking.ZRTB.registration_mediamathId1 = "ID";
AWIN.Tracking.ZRTB.registration_mediamathId2 = "ID";
AWIN.Tracking.ZRTB.registration_mediamathId3 = "ID";
AWIN.Tracking.ZRTB.registration_mediamathId4 = "ID";
AWIN.Tracking.ZRTB.registration_mediamathId5 = "ID";

//identification of page types
AWIN.Tracking.Zx = AWIN.Tracking.Zx || {};
if (window.location.href.indexOf("www.example.com/category") > -1) {
    AWIN.Tracking.Zx.pageType = 'category';
} else if (window.location.href.indexOf("www.example.com/product") > -1) {
    AWIN.Tracking.Zx.pageType = 'product';
} else if (window.location.href.indexOf("www.example.com") > -1) {
    AWIN.Tracking.Zx.pageType = 'home';
}
```




## Example


If the plugin is activated with this code :


``` javascript
AWIN.Tracking.ZRTB = AWIN.Tracking.ZRTB || {};

AWIN.Tracking.ZRTB.home_retargetingOn = 1;
AWIN.Tracking.ZRTB.basket_retargetingOn = 1;
AWIN.Tracking.ZRTB.checkout_retargetingOn = 1;

//define merchantID
AWIN.Tracking.ZRTB.merchantId1 = "100001";
AWIN.Tracking.ZRTB.merchantId2 = "100002";

//define pageIDs
AWIN.Tracking.ZRTB.home_mediamathId1 = "111001";
AWIN.Tracking.ZRTB.home_mediamathId1 = "111002";

AWIN.Tracking.ZRTB.basket_mediamathId1 = "222001";

AWIN.Tracking.ZRTB.checkout_mediamathId1 = "333001";

//identification of page types
AWIN.Tracking.Zx = AWIN.Tracking.Zx || {};
if (window.location.href.indexOf("www.cartezero.fr/icc/assisto/nav") > -1) {
    AWIN.Tracking.Zx.pageType = 'checkout';
} else if (window.location.href.indexOf("www.cartezero.fr/Accueil/broker.jsp") > -1) {
    AWIN.Tracking.Zx.pageType = 'basket';
} else if (window.location.href.indexOf("www.cartezero.fr/Accueil") > -1) {
    AWIN.Tracking.Zx.pageType = 'home';
}
```



Then the dwin mastertag will fire 4 pixels :
**Home page** ( www.cartezero.fr/Accueil ) : 2 pixels


``` text
https://pixel.mathtag.com/event/img?mt_id=111001&mt_adid=100001&v1=&v2=&v3=&s1=&s2=home&s3=
https://pixel.mathtag.com/event/img?mt_id=111002&mt_adid=100002&v1=&v2=&v3=&s1=&s2=home&s3=
```



**Basket page** ( www.cartezero.fr/Accueil/broker.jsp ) : 1 pixel


``` text
https://pixel.mathtag.com/event/img?mt_id=222001&mt_adid=100001&v1=&v2=&v3=&s1=&s2=basket&s3=
```



**Checkout page** ( www.cartezero.fr/icc/assisto/nav ) : 1 pixel


``` text
https://pixel.mathtag.com/event/img?mt_id=333001&mt_adid=100001&v1=&v2=&v3=&s1=&s2=checkout&s3=
```


