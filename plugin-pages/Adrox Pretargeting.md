# READ ME

Plugin is not supported on AWIN platform anymore. Reference:
[SOLUTION-41465](https://jira.awin.com/browse/SOLUTION-41465)

# Description

# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

The Adrox plugin has different tags depending on the type of page
visited.

Plugin supports following `PAGETYPE`: home, category, product, checkout

# Tag example

<https://ad.trsv3.com/track.php?q=>\[{%22customer%22:%22281%22,%22page%22:%22home%22,{%22url%22:%22https%3A%2F%2Fwww.lampara.es%2F%22},{%22referrer%22:%22https%3A%2F%2Fwww.lampara.es%2Filuminacion-led-lamparas-de-techo-led%2F%22},{%22window%22,{%22outerHeight%22:1160,%22outerWidth%22:1920,%22innerHeight%22:523,%22innerWidth%22:1920,%22iframe%22:0,
%22userAgent%22:%22Mozilla/5.0%20(Windows%20NT%206.1;%20Win64;%20x64)%20AppleWebKit/537.36%20(KHTML,
%20like%20Gecko)%20Chrome/64.0.3282.167%20Safari/537.36%22}}\]

# Tag Plugin

|              |                    |
|--------------|--------------------|
| PluginType:  | Adrox Pretargeting |
| PluginSetup: | See Code Below     |
| Active       | Tick The Checkbox  |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `SPECIFIC_ADROX_CUSTOMER_ID` with its real value.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.


``` javascript
AWIN.Tracking.Adrox = AWIN.Tracking.Adrox || {};
AWIN.Tracking.Adrox.customerId = "SPECIFIC_ADROX_CUSTOMER_ID";
AWIN.Tracking.Adrox.pagetype = "PAGETYPE_IDENTIFIER";
```





``` javascript
AWIN.Tracking.Adrox = AWIN.Tracking.Adrox || {};
AWIN.Tracking.Adrox.customerId = "197";
AWIN.Tracking.Adrox.pagetype = "generic";
```



(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

## Product Page

The plugin does not use the product scraper itself but you could use it
to fetch the ID if you prefer and supply it to the identifier config
variable.


``` javascript
AWIN.Tracking.Adrox.identifier = "ID_OF_THE_PRODUCT";
```



Example:


``` javascript
AWIN.Tracking.Adrox.identifier = tc_vars.product_id;
```




## Category Page


``` javascript
AWIN.Tracking.Adrox.category = "NAME_OF_CATEGORY";
```



Example:


``` javascript
AWIN.Tracking.Adrox.category = tc_vars.page_name;
```




## Checkout Page

Page type checkout will be automatically detected; requirement is to
have AWIN.Tracking.Sale implemented on the checkout success page.

# Example Complete Setup


``` javascript
AWIN.Tracking.Adrox = AWIN.Tracking.Adrox || {};
AWIN.Tracking.Adrox.customerId = "197";
AWIN.Tracking.Adrox.pagetype = "generic";

if (tc_vars.env_template == "Accueil") {
    AWIN.Tracking.Adrox.pagetype = "home";
} else if (tc_vars.env_template == "Liste") {
    AWIN.Tracking.Adrox.pagetype = "category";
    AWIN.Tracking.Adrox.category = tc_vars.page_name;
} else if (tc_vars.env_template == "FicheProduit") {
    AWIN.Tracking.Adrox.pagetype = "product";
    AWIN.Tracking.Adrox.identifier = tc_vars.product_id;
}
```


# Plugin Code


``` javascript
AWIN.Tracking.Adrox = AWIN.Tracking.Adrox || {};
AWIN.Tracking.Adrox.url = AWIN.Tracking.Adrox.url || AWIN.sProtocol + "ad.trsv3.com/track.php";

(function ($a) {
    var pagetype = $a.pagetype || AWIN.Tracking.fetchZxParam('pagetype');

    if (AWIN.Tracking.Sale) {
        pagetype = "checkout";
    } else if ("checkout" === pagetype.toLowerCase()) {
        AWIN.Tracking.Sale = {};
    }

    if ("undefined" === typeof pagetype) {
        return;
    }

    var _adrx = [{
        customer: $a.customerId || AWIN.Tracking.fetchZxParam('customerId'),
        page: pagetype.toLowerCase()
    }];

    switch (pagetype.toLowerCase()) {
        case "home":
            break;
        case "product":
            _adrx.push({
                product: {
                    id: $a.identifier || AWIN.Tracking.fetchZxParam('identifier')
                }
            });
            break;
        case "category":
            _adrx.push({
                category: {
                    id: $a.category || AWIN.Tracking.fetchZxParam('category')
                }
            });
            break;
        case "checkout":
            _adrx[0].page = 'conversion';
            _adrx.push({
                conversion: {
                    id: AWIN.Tracking.fetchZxParam('transaction') || AWIN.Tracking.Sale.orderRef,
                    type: 'sale',
                    value: AWIN.Tracking.fetchZxParam('total_amount') || AWIN.Tracking.Sale.amount,
                    commission: '0',
                    customer: '',
                    subid: '',
                    assigned: 0
                }
            });
            break;
        default:
            return;
    }

    var w = window,
        i = 0;

    while (true) {
        try {
            if (w !== w.parent) {
                w = w.parent;
            } else {
                break;
            }
        } catch (e) {
            i = 1;
            break;
        }
    }

    _adrx.push({
        url: encodeURIComponent(w.document.URL)
    });
    _adrx.push({
        referrer: encodeURIComponent(w.document.referrer)
    });
    _adrx.push({
        window: {
            outerHeight: w.outerHeight,
            outerWidth: w.outerWidth,
            innerHeight: w.innerHeight,
            innerWidth: w.innerWidth,
            iframe: i,
            userAgent: navigator.userAgent
        }
    });

    AWIN.Tracking.scriptAppend($a.url + "?q=" + JSON.stringify(_adrx));
})(AWIN.Tracking.Adrox);
```

