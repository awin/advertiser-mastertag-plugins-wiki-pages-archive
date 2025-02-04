# Requirements

- MasterTag must be displayed across all pages in the shop
- javascript based tracking code (Conversion Tag) must be loaded
  unconditionally on the order confirmation page.
- Plugin requires Product Level Tracking implemented on the checkout
  success page OR any alternative dataLayer.



# Configuration

Plugin supports following PAGETYPE: search, searchresult, itinerary,
basket, bookingconfirmation

## Config code

Replace `"TOKEN"` with the token provided by the publisher.

Necessary properties to be set: tokenId


``` javascript

AWIN.Tracking.PrecisoTravel = AWIN.Tracking.PrecisoTravel || {};
AWIN.Tracking.PrecisoTravel.tokenId = 'TOKEN';
```


## Search page

Necessary properties to be set: pagetype


``` javascript

AWIN.Tracking.PrecisoTravel.pagetype = 'home';
```


## Searchresult page

Necessary properties to be set: pagetype, category name

Replace placeholder surrounded by angular brackets (`<>`) with it's real
value scraped from advertiser's website.


``` javascript

AWIN.Tracking.PrecisoTravel.pagetype = 'searchresult';
AWIN.Tracking.PrecisoTravel.category= '<PRODUCT_CATEGORY>';
```


## Itinerary page

Necessary properties to be set: pagetype, product id, product category,
product name, product price, currency (hard-coded), start date, end
date, departure place, destination

Replace placeholder surrounded by angular brackets (`<>`) with it's real
value scraped from advertiser's website.


``` javascript
AWIN.Tracking.PrecisoTravel.pagetype = 'itinerary';
AWIN.Tracking.PrecisoTravel.identifier = '<PRODUCT_ID>';
AWIN.Tracking.PrecisoTravel.category = '<CATEGORY_NAME>';
AWIN.Tracking.PrecisoTravel.productName = '<PRODUCT_NAME>';
AWIN.Tracking.PrecisoTravel.productPrice = '<PROUCT_PRICE>';
AWIN.Tracking.PrecisoTravel.currency = 'EUR';
AWIN.Tracking.PrecisoTravel.startDate = '<START_DATE>';
AWIN.Tracking.PrecisoTravel.endDate = '<END_DATE>';
AWIN.Tracking.PrecisoTravel.departurePlace  = '<DEPARTURE_PLACE>';
AWIN.Tracking.PrecisoTravel.destination  = '<DESTINATION_PLACE>';
```


## Basket page

Necessary properties to be set: pagetype, product id, product category,
product name, product price, currency (hard-coded), start date, end
date, departure place, destination

The plugin will look for product ids in the "zx_products" array.

Replace placeholder surrounded by angular brackets (`<>`) with it's real
value scraped from advertiser's website.


``` javascript

AWIN.Tracking.PrecisoTravel.pagetype = 'basket';
AWIN.Tracking.PrecisoTravel.currency = 'EUR';
AWIN.Tracking.PrecisoTravel.startDate = '<START_DATE>';
AWIN.Tracking.PrecisoTravel.endDate = '<END_DATE>';
AWIN.Tracking.PrecisoTravel.departurePlace  = '<DEPARTURE_PLACE>';
AWIN.Tracking.PrecisoTravel.destination  = '<DESTINATION_PLACE>';

var zx_products = [];
for (var i = 0; i < dataLayer[0].cartContent.items.length; i++) {
    zx_products.push('<PRODUCT_ID>');
}
```


## bookingconfirmation page

Necessary properties to be set: pagetype

IF PLT is implemented the plugin will look for the product ids in the
PLT object, else the plugin will look for product ids in the
"zx_products" array.

Replace placeholder surrounded by angular brackets (`<>`) with it's real
value scraped from advertiser's website.


``` javascript

AWIN.Tracking.PrecisoTravel.pagetype = 'bookingconfirmation';
AWIN.Tracking.PrecisoTravel.currency = 'EUR';
AWIN.Tracking.PrecisoTravel.startDate = '<START_DATE>';
AWIN.Tracking.PrecisoTravel.endDate = '<END_DATE>';
AWIN.Tracking.PrecisoTravel.departurePlace  = '<DEPARTURE_PLACE>';
AWIN.Tracking.PrecisoTravel.destination  = '<DESTINATION_PLACE>';

var zx_products = [];
for (var i = 0; i < dataLayer.filter(x => x.event == 'purchase')[0].ecommerce.items.length; i++) {
    zx_products.push('<PRODUCT_ID>')
}
```


# Configuration Example

Replace `"TOKEN"` with the token provided by the publisher.


``` javascript

AWIN.Tracking.PrecisoTravel = AWIN.Tracking.PrecisoTravel || {};
AWIN.Tracking.PrecisoTravel.tokenId = 'TOKEN';

if (dataLayer[0].pagePostType == 'frontpage') {
    AWIN.Tracking.PrecisoTravel.pagetype = 'search';
} else if (dataLayer[0].pagePostType == 'product' && dataLayer[0].pagePostType2 == undefined) {
    AWIN.Tracking.PrecisoTravel.pagetype = 'searchresult';
    AWIN.Tracking.PrecisoTravel.category = 'shop';
} else if (dataLayer[0].pagePostType2 == 'single-product') {
    AWIN.Tracking.PrecisoTravel.pagetype = 'itinerary';
    AWIN.Tracking.PrecisoTravel.identifier = dataLayer[0].ecommerce.detail.products[0].id;
    AWIN.Tracking.PrecisoTravel.category = 'shop';
    AWIN.Tracking.PrecisoTravel.productName = dataLayer[0].ecommerce.detail.products[0].name;
    AWIN.Tracking.PrecisoTravel.productPrice = dataLayer[0].ecommerce.detail.products[0].price;
    AWIN.Tracking.PrecisoTravel.currency = 'EUR';
    AWIN.Tracking.PrecisoTravel.startDate = dataLayer[0].ecommerce.detail.products[0].startDate;
    AWIN.Tracking.PrecisoTravel.endDate = dataLayer[0].ecommerce.detail.products[0].endDate;
    AWIN.Tracking.PrecisoTravel.departurePlace  = dataLayer[0].ecommerce.detail.products[0].departure;
    AWIN.Tracking.PrecisoTravel.destination  = dataLayer[0].ecommerce.detail.products[0].destination;
} else if (location.href.includes('/cart/')) {
    AWIN.Tracking.PrecisoTravel.pagetype = 'basket';
    var zx_products = [];
    for (var i = 0; i < dataLayer[0].cartContent.items.length; i++) {
        zx_products.push(dataLayer[0].cartContent.items[i].id);
    }
    AWIN.Tracking.PrecisoTravel.startDate = dataLayer[0].ecommerce.detail.products[0].startDate;
    AWIN.Tracking.PrecisoTravel.endDate = dataLayer[0].ecommerce.detail.products[0].endDate;
    AWIN.Tracking.PrecisoTravel.departurePlace  = dataLayer[0].ecommerce.detail.products[0].departure;
    AWIN.Tracking.PrecisoTravel.destination  = dataLayer[0].ecommerce.detail.products[0].destination;
    AWIN.Tracking.PrecisoTravel.currency = 'EUR';
} else if (AWIN.Tracking.Sale) {
    AWIN.Tracking.PrecisoTravel.pagetype = 'bookingconfirmation';
    var zx_products = [];
    for (var i = 0; i < dataLayer.filter(x => x.event == 'purchase')[0].ecommerce.items.length; i++) {
        zx_products.push(dataLayer.filter(x => x.event == 'purchase')[0].ecommerce.items[i].id)
    }
    AWIN.Tracking.PrecisoTravel.currency = 'EUR';
    AWIN.Tracking.PrecisoTravel.startDate = dataLayer[0].ecommerce.detail.products[0].startDate;
    AWIN.Tracking.PrecisoTravel.endDate = dataLayer[0].ecommerce.detail.products[0].endDate;
    AWIN.Tracking.PrecisoTravel.departurePlace  = dataLayer[0].ecommerce.detail.products[0].departure;
    AWIN.Tracking.PrecisoTravel.destination  = dataLayer[0].ecommerce.detail.products[0].destination;
}
```


# Relevant Tickets

[PROD-10190](https://jira.awin.com/browse/PROD-10190)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/precisoTravel/plugin.js)