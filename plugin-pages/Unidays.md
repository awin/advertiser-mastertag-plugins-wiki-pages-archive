
# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

The Unidays plugin has two different tags that need to be implemented on
every page.

# Tag Plugin

|               |                      |
|---------------|----------------------|
| PluginType:   | Unidays              |
| Plugin Setup: | "See Code Below"     |
| Active:       | "Tick The Check Box" |


== Plugin setup code == The code below goes into the plugin setup field
in the tag management form.

Replace valubes between double quotes `"..."` with real values.

AWIN.Tracking.Sale variables should be implemented on final transaction
page (typically checkout page).

AWIN.Tracking.Unidays variables should be implemented on every page.


``` javascript
AWIN.Tracking.Unidays.Sale.amount = "AMOUNT";
AWIN.Tracking.Unidays.Sale.currency = "URL";
AWIN.Tracking.Unidays.Sale.orderRef = "UUID";
AWIN.Tracking.Unidays.Sale.parts = "DEFAULT:90";
AWIN.Tracking.Unidays.Sale.voucher = "URL";
AWIN.Tracking.Unidays.Sale.test = "UUID";
```

``` javascript
AWIN.Tracking.Unidays = AWIN.Tracking.Unidays || {};
AWIN.Tracking.Unidays.url = "URL";
AWIN.Tracking.Unidays.customerId = "ID";
AWIN.Tracking.Unidays.signingKey = "SIGNING_KEY";
AWIN.Tracking.Unidays.unidaysDiscount = "DISCOUNT";
AWIN.Tracking.Unidays.code = "CODE";
AWIN.Tracking.Unidays.tax = "TAX";
AWIN.Tracking.Unidays.shipping = "SHIPPING";
AWIN.Tracking.Unidays.shippingDiscount = "SHIPPING_DISCOUNT";
AWIN.Tracking.Unidays.itemsAmount = "ITEMS AMOUNT";
AWIN.Tracking.Unidays.itemsDiscount = "ITEMS DISCOUNT";
AWIN.Tracking.Unidays.unidaysPercentage = "UNIDAYS_PERCENTAGE";
AWIN.Tracking.Unidays.newCustomer = "IS_NEW_CUSTOMER?";
```



Example:


``` javascript
AWIN.Tracking.Unidays.Sale.amount = "9.98";
AWIN.Tracking.Unidays.Sale.currency = "EUR";
AWIN.Tracking.Unidays.Sale.orderRef = "test1234";
AWIN.Tracking.Unidays.Sale.parts = "DEFAULT:1";
AWIN.Tracking.Unidays.Sale.voucher = "VOUCHER12";
AWIN.Tracking.Unidays.Sale.test = "1";
```

``` javascript
AWIN.Tracking.Unidays.url = "https://tracking.myunidays.com/perks/redemption/v1.1-test.js";
AWIN.Tracking.Unidays.customerId = "1234";
AWIN.Tracking.Unidays.signingKey = "1234";
AWIN.Tracking.Unidays.unidaysDiscount = .02;
AWIN.Tracking.Unidays.code = "TEST";
AWIN.Tracking.Unidays.tax = 0.29;
AWIN.Tracking.Unidays.shipping = 0;
AWIN.Tracking.Unidays.shippingDiscount = 0;
AWIN.Tracking.Unidays.itemsAmount = 9.98;
AWIN.Tracking.Unidays.itemsDiscount = .02;
AWIN.Tracking.Unidays.unidaysPercentage = 0.2;
AWIN.Tracking.Unidays.newCustomer = 1;
```



(values in `UPPER_CASE` should be replaced with the appropriate values)

Below you will find code for this plugin:

``` javascript
AWIN.Tracking.Unidays = AWIN.Tracking.Unidays || {};
AWIN.Tracking.Unidays.url = AWIN.Tracking.Unidays.url
    || AWIN.sProtocol + "tracking.myunidays.com/perks/redemption/v1.1.js";
AWIN.Tracking.CryptoJS = AWIN.Tracking.CryptoJS || {};
AWIN.Tracking.CryptoJS.url = "https://cdnjs.cloudflare.com/ajax/libs/crypto-js/3.1.2/rollups/hmac-sha512.js";
AWIN.Tracking.CryptoJS.base64url = "https://cdnjs.cloudflare.com/ajax/libs/crypto-js/3.1.2/components/enc-base64-min.js";

(function ($u) {
    if ("undefined" === typeof $u.customerId || "undefined" === typeof $u.signingKey
        || "undefined" === typeof AWIN.Tracking.Sale) {

        return;
    }

    $u.cryptoEncCallback = function () {
        var query = AWIN.Tracking.buildQueryString({
            CustomerId: $u.customerId,
            TransactionId: AWIN.Tracking.Sale.orderRef,
            MemberId: '',
            Currency: AWIN.Tracking.Sale.currency,
            OrderTotal: (Math.round(AWIN.Tracking.Sale.amount * 100) / 100).toFixed(2),
            ItemsUNiDAYSDiscount: (Math.round($u.unidaysDiscount * 100) / 100).toFixed(2),
            Code: $u.code || '',
            ItemsTax: (Math.round($u.tax * 100) / 100).toFixed(2),
            ShippingGross: (Math.round($u.shipping * 100) / 100).toFixed(2),
            ShippingDiscount: (Math.round($u.shippingDiscount * 100) / 100).toFixed(2),
            ItemsGross: (Math.round($u.itemsAmount * 100) / 100).toFixed(2),
            ItemsOtherDiscount: (Math.round($u.itemsDiscount * 100) / 100).toFixed(2),
            UNiDAYSDiscountPercentage: (Math.round($u.unidaysPercentage * 100) / 100).toFixed(2),
            NewCustomer: (Math.round($u.newCustomer * 100) / 100).toFixed(0)
        });

        var secret = CryptoJS.enc.Base64.parse($u.signingKey);
        var hash = CryptoJS.HmacSHA512(query, secret);
        var sig = CryptoJS.enc.Base64.stringify(hash);

        query += "&" + AWIN.Tracking.buildQueryString({
            Signature: sig
        });

        AWIN.Tracking.scriptAppend($u.url + "?" + query);
    };

    $u.cryptoJSCallback = function () {
        AWIN.Tracking.scriptAppend(AWIN.Tracking.CryptoJS.base64url, null, "AWIN.Tracking.Unidays.cryptoEncCallback()");
    };

    AWIN.Tracking.scriptAppend(AWIN.Tracking.CryptoJS.url, null, "AWIN.Tracking.Unidays.cryptoJSCallback()");
})(AWIN.Tracking.Unidays);
```