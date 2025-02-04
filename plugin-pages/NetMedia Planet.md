# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Home Page Configuration


``` javascript
AWIN.Tracking.NetMedia = AWIN.Tracking.NetMedia || {};
AWIN.Tracking.NetMedia.merchantName = "MERCHANT_NAME";
```




# Plugin Source Code

[on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/netMedia/plugin.jsView)

# Plugin Code


``` javascript
AWIN.Tracking.NetMedia = AWIN.Tracking.NetMedia || {};

(function(nm){

    if (!nm.merchantName) {
        return;
    }

    if (AWIN.Tracking.Sale) {
        // sale page tracking code
        var url = 'https://4405841.fls.doubleclick.net/activityi;src=4405841;type=AWINS0;cat=AWINS0;qty=1;cost=' + encodeURIComponent(AWIN.Tracking.Sale.amount) +
        ';u1=' + encodeURIComponent(nm.merchantName) + ';u2=' + AWIN.Tracking.iMerchantId + ';u3=' + encodeURIComponent(stripEmail()) + ';u6=0;ord=' + encodeURIComponent(AWIN.Tracking.Sale.orderRef) + '?';
    } else {
        // non-sale page tracking code
        var axel = Math.random() + "";
        var randomValue = axel * 10000000000000;
        var url = 'https://4405841.fls.doubleclick.net/activityi;src=4405841;type=Count0;cat=AWINP0;u1=' +
        encodeURIComponent(nm.merchantName) + ';u2=' + AWIN.Tracking.iMerchantId + ';u3=' + encodeURIComponent(stripEmail()) + ';ord=' + randomValue + '?';
    }

    if (document.getElementsByTagName("body")[0]) {
        var iframe = document.createElement("iframe");
        iframe.src = url;
        iframe.height = 1;
        iframe.width = 1;
        iframe.frameborder = 0;
        AWIN.Tracking.hideElement(iframe);
        document.getElementsByTagName("body")[0].appendChild(iframe);
    }

    function stripEmail() {
        try {
            var url = decodeURIComponent(document.URL) || "";
            url = url.replace(/[a-zA-Z0-9._+-]+@[a-zA-Z0-9._+-]+\.[a-zA-Z0-9._+-]+/gi, '');

            return url;
        }
        catch(err) {
            return document.URL;
        }
    }

})(AWIN.Tracking.NetMedia);
```


