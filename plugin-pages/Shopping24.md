
# Integration requirements

The Dwin1 tag needs to be displayed on the confirmation page.

# How is the tag implemented?

The Shopping24 plugin is triggered when `AWIN.Tracking.Sale` and
`AWIN.Tracking.Shopping24.hashId` are defined.

# Tag example

[http://tracking.s24.com/TrackOrder?shopId=aaabbbcccdddeeefffggg&orderNumber=test1234&lineItems=2&netRevenue=11.21&shipping=1.23&products=sku2116,sku232\\AAA](http://tracking.s24.com/TrackOrder?shopId=aaabbbcccdddeeefffggg&orderNumber=test1234&lineItems=2&netRevenue=11.21&shipping=1.23&products=sku2116,sku232\,AAA)

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.


``` javascript
AWIN.Tracking.Shopping24 = AWIN.Tracking.Shopping24 || {};
AWIN.Tracking.Shopping24.hashId="HASH_ID";
AWIN.Tracking.Shopping24.delivery=DELIVERY_COST;

AWIN.Tracking.Sale.amount=SALE_AMOUNT;
AWIN.Tracking.Sale.orderRef="ORDER_REFERENCE"
```





``` javascript
AWIN.Tracking.Shopping24 = AWIN.Tracking.Shopping24 || {};
AWIN.Tracking.Shopping24.hashId="dd98e81b00ee8f8bab4849cf7e8e493f";
AWIN.Tracking.Shopping24.delivery=1.23;

AWIN.Tracking.Sale.amount=9.98;
AWIN.Tracking.Sale.orderRef="OrderA6554-455-887"
```



(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

# Plugin code


``` javascript
AWIN.Tracking.Shopping24 = AWIN.Tracking.Shopping24 || {};
AWIN.Tracking.Shopping24.saleUrl = AWIN.Tracking.Shopping24.saleUrl || AWIN.sProtocol + 'tracking.s24.com/TrackOrder';

(function($s) {

    if (!AWIN.Tracking.Sale || !$s.hashId) {
        return;
    }

    var products = AWIN.Tracking.getBasketData();

    var queryObject = {
        "shopId": $s.hashId,
        "orderNumber": AWIN.Tracking.Sale.orderRef,
        "lineItems": products.length,
        "netRevenue": Number(AWIN.Tracking.Sale.amount)
    };

    if (("undefined" !== typeof $s.delivery)  && !isNaN($s.delivery)) {
        queryObject['netRevenue'] += Number($s.delivery);
        queryObject['shipping'] = $s.delivery;
    }

    var query = AWIN.Tracking.buildQueryString(queryObject);

    if (products.length>0) {
        var skus=[],sku;
        for (var i = 0; i < products.length; i++) {
            sku=products[i].sku.split(',').join('(,)');
            sku = encodeURIComponent(sku);
            sku = sku.split('(%2C)').join('\\,');
            skus.push(sku);
        }
        query += '&products='+skus.join(',');
    }

    AWIN.Tracking.pixelAppend($s.saleUrl + '?' + query);

})(AWIN.Tracking.Shopping24);
```

