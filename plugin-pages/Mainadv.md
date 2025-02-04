# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

Mainadv plugin has different tags depending on the type of page visited.
It requires only the configuration of the `PAGETYPE_IDENTIFIER`.

# Tag example

<https://www.mainadv.com/retargeting/live/zanox_rtg.aspx?Key=ZX&visitorIp=ZX-HOLA_ES&pagetype=home>

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `Mainadv_KEY` with its real value.

Replace `Mainadv_TOKEN` with its real value.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.


``` javascript
AWIN.Tracking.Mainadv = AWIN.Tracking.Mainadv || {};
AWIN.Tracking.Mainadv.pagekey = "Mainadv_KEY";
AWIN.Tracking.Mainadv.token = "Mainadv_TOKEN";
AWIN.Tracking.Mainadv.pagetype = "PAGETYPE_IDENTIFIER";
```





``` javascript
AWIN.Tracking.Mainadv = AWIN.Tracking.Mainadv || {};
AWIN.Tracking.Mainadv.pagekey = "ZX";
AWIN.Tracking.Mainadv.token = "ZX-HOLA_ES";
```



(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

# Example Complete Setup


``` javascript
AWIN.Tracking.Mainadv = AWIN.Tracking.Mainadv || {};
AWIN.Tracking.Mainadv.appId = "";
AWIN.Tracking.Mainadv.pagekey = "ZX";
AWIN.Tracking.Mainadv.token = "BLOOMANDWILD_FR";
AWIN.Tracking.Mainadv.pagetype = "generic";

if (document.body.getAttribute("ui-state") == "homepage") {
    AWIN.Tracking.Mainadv.pagetype = "home";
} else if (document.body.getAttribute("class") == "has-product-selected modal-open") {
    AWIN.Tracking.Mainadv.pagetype = "product";
    AWIN.Tracking.Mainadv.identifier = document.getElementsByClassName("modal-title flex-fill")[0].innerText.replace(/[^a-zA-Z]+/g, '');
}  else if (document.body.getAttribute("class") == "has-product-selected") {
    AWIN.Tracking.Mainadv.pagetype = "basket";
    var zx_products = [];
    zx_products.push({
        'identifier': document.getElementsByClassName("order-progress__content--heading serif")[0].innerText
    });
} else if (document.body.getAttribute("ui-state") == "category")  {
    AWIN.Tracking.Mainadv.pagetype = "category";
    AWIN.Tracking.Mainadv.category = location.pathname.split("tagonly")[1].slice(1);
}
```


# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/mainadv/plugin.js)