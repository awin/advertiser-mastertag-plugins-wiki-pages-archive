
## Integration Requirements

- Dwin tag to be shown for these pages:
  - product
  - checkout
  - lead
  - generic

## Plugin Setup code for AWIN integrations


``` javascript
AWIN.Tracking.AntVoice = AWIN.Tracking.AntVoice || {};
AWIN.Tracking.AntVoice.projectId = "PROJECT_ID";
```


- Replace `PROJECT_ID` with real value.

## Antvoice Plugin


``` javascript
AWIN.Tracking.AntVoice = AWIN.Tracking.AntVoice || {};
AWIN.Tracking.AntVoice.url = AWIN.Tracking.AntVoice.url || AWIN.sProtocol + "ads.avads.net/v1/tracking?type=behavior&";

(function ($n) {

  if ((typeof $n.projectId === "undefined") || (typeof $n.pagetype === "undefined")) {
    return;
  }

  var pagetype = $n.pagetype;

  if (AWIN.Tracking.Sale) {
    pagetype = "checkout";
  } else if ("checkout" === pagetype.toLowerCase()) {
    AWIN.Tracking.Sale = {};
  }

  $n.fetchBasketData = function () {
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

  var query = {
    owner: $n.projectId,
    market:'FR',
    lang: 'fr-FR'
  };

  var lineItems = [];

  switch (pagetype.toLowerCase()) {
    case "product" :
      query.id = $n.identifier;
      query.act = 'view';
      break;
    case "checkout" :
      lineItems = $n.fetchBasketData();
      query.trId = AWIN.Tracking.Sale.orderRef;
      query.act = 'buy';
      break;
    case "lead":
      query.act = 'buy';
      query.id = $n.projectId;
      break;
    case "generic":
      query.act = 'view';
      query.id = $n.projectId;
      break;
    default:
      break;
  }

  if (lineItems.length > 0) {
    lineItems.forEach(function (product) {
      query.id = product.identifier;
      query.pr = product.amount;
      query.cur = 978;
      query.qty = product.quantity;
      AWIN.Tracking.pixelAppend(AWIN.Tracking.AntVoice.url + AWIN.Tracking.buildQueryString(query));
    });
  } else {
    AWIN.Tracking.pixelAppend(AWIN.Tracking.AntVoice.url + AWIN.Tracking.buildQueryString(query));
  }

})(AWIN.Tracking.AntVoice);
```



== Antvoice Pïxels called ==

Then dwin mastertag will fire pixels:

**Product page** :


``` text

Pixel called : http://ads.avads.net/v1/tracking?type=behavior&owner=PROJECT_ID&market=FR&lang=fr-FR&id=PROD12&act=view
```



**Checkout page** :


``` text

Pixel called : http://ads.avads.net/v1/tracking?type=behavior&owner=PROJECT_ID&market=FR&lang=fr-FR&trId=code&act=buy&id=PRODUCT_ID&pr=PRODUCT_PRICE&cur=978&qty=1
```



**Lead page** :


``` text

Pixel called : http://ads.avads.net/v1/tracking?type=behavior&owner=PROJECT_ID&market=FR&lang=fr-FR&act=buy&id=PROJECT_ID
```



**Generic page** :


``` text

Pixel called : http://ads.avads.net/v1/tracking?type=behavior&owner=PROJECT_ID&market=FR&lang=fr-FR&act=view&id=PROJECT_ID
```


