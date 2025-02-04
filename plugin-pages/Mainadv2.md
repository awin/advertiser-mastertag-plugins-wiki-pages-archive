
# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Home Page Configuration

``` javascript
AWIN.Tracking.Mainadv2 = AWIN.Tracking.Mainadv2 || {};
AWIN.Tracking.Mainadv2.pagetype = "PAGETYPE";
AWIN.Tracking.Mainadv2.key = "KEY";
AWIN.Tracking.Mainadv2.token = "TOKEN";
```



## Configuration Example


``` javascript
AWIN.Tracking.Mainadv2 = AWIN.Tracking.Mainadv2 || {};
AWIN.Tracking.Mainadv2.key = "KEY";
AWIN.Tracking.Mainadv2.token = "TOKEN";
AWIN.Tracking.Mainadv2.pagetype = "generic";

if(dataLayer[0].pageType == "StartPage"){
    AWIN.Tracking.Mainadv2.pagetype = "home";
}else if(dataLayer[0].pageType == "CategoryPage"){
    AWIN.Tracking.Mainadv2.pagetype = "category";
}else if(dataLayer[0].pageType == "ProductPage"){
    AWIN.Tracking.Mainadv2.pagetype = "product";
}else if(dataLayer[0].pageType == "BasketPage"){
    AWIN.Tracking.Mainadv2.pagetype = "basket";
}
```




# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/mainadv2/plugin.js)