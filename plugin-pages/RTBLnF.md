# RTB LnF plugin

## DESCRIPTION

Application to reach the right user at the right time with the right ad.

Look&Feel is an Italian Advertising Agency. Our goal is to reach the
right customer at the right time. This remarketing application intercept
users' habits and behaviors on a website and make them available for a
very accurate advertising. This product shows the most relevant ads and
products to each user increasing the conversion rate.

**Contact details:**
Looknfeel: Francesco Audano adv@looknfeel.it // CEO & Adv Specialist
zanox commercial: Matheus Alves \<Matheus.Alves@zanox.com\> // Account
Manager Publisher \[BR\]
zanox tech: Marek Najman \<Marek.Najman@zanox.com\> // Global Technical
Services
**HELIX MIGRATION PLUGIN**
Application Store:
<http://apps.zanox.com/web/guest/home?appid=2E84843496CB593C404F>

## INTEGRATION REQUIREMENTS

Dwin tag to be displayed unconditionally across all pages.

8 page types are available : home, product, category, basket, checkout,
registration, generic, search.

## PLUGIN SETUP CODE

Please use the configuration in the tag management section.

Decalre pageType_siteScoutPixelId with the value supplied by LnF
publisher for dedicated page type on the advertiser site.

siteScoutId is generated on SiteScout RTB platform once the publisher
created his audience list.

You will find more information here:
<https://support.sitescout.com/hc/en-us/articles/204337583-Creating-An-Audience-List>

**TEMPLATE**


``` javascript
AWIN.Tracking.RTBLnF = AWIN.Tracking.RTBLnF || {};
AWIN.Tracking.RTBLnF.home_siteScoutPixelId = '[home page Site Scout ID]';
AWIN.Tracking.RTBLnF.category_siteScoutPixelId = '[category page Site Scout ID]';
AWIN.Tracking.RTBLnF.search_siteScoutPixelId = '[search page Site Scout ID]';
AWIN.Tracking.RTBLnF.registration_siteScoutPixelId = '[registration page Site Scout ID]';
AWIN.Tracking.RTBLnF.basket_siteScoutPixelId = '[basket page Site Scout ID]';
AWIN.Tracking.RTBLnF.checkout_siteScoutPixelId = '[checkout page Site Scout ID]';
AWIN.Tracking.RTBLnF.product_siteScoutPixelId = '[product page Site Scout ID]';
AWIN.Tracking.RTBLnF.generic_siteScoutPixelId = '[generic page Site Scout ID]';
```



**CONFIGURATION EXAMPLE**


``` javascript
AWIN.Tracking.RTBLnF = AWIN.Tracking.RTBLnF || {};
AWIN.Tracking.RTBLnF.home_siteScoutPixelId = 'cafb37c4d9c7b5ad';
AWIN.Tracking.RTBLnF.category_siteScoutPixelId = '0cc66dd47dd48b60';
AWIN.Tracking.RTBLnF.search_siteScoutPixelId = 'f6baa61513ed7244';
AWIN.Tracking.RTBLnF.registration_siteScoutPixelId = 'bb67da9e10af624f';
AWIN.Tracking.RTBLnF.basket_siteScoutPixelId = '4a5add3baf316baa';
AWIN.Tracking.RTBLnF.checkout_siteScoutPixelId = '5127a69b11bf4f04';
AWIN.Tracking.RTBLnF.product_siteScoutPixelId = '82a7dfaafefcd920';
AWIN.Tracking.RTBLnF.generic_siteScoutPixelId = '3b458b1c655d7056';
```



Please be aware that the publisher might provide you with original
SiteScrout tags (see below).

You can simply copy the value from the script tag path
~/iap/{siteScoutPixelId}


``` javascript
<script type="text/javascript">
var ssaUrl = ('https:' == document.location.protocol ? 'https://' : 'http://') +
'pixel.sitescout.com/iap/0cc66dd47dd48b60';
new Image().src = ssaUrl;
</script>
```




## Page type definition

In order to load corresponding tag on desired page type, please instruct
the plugin by declaring AWIN.Tracking.RTBLnF.pageType value:


``` javascript
if (window.location.href.indexOf("www.example.com") > -1) {
    AWIN.Tracking.RTBLnF.pageType = 'home';
}
else if (window.location.href.indexOf("www.example.com/category") > -1) {
    AWIN.Tracking.RTBLnF.pageType = 'category';
}
else if (window.location.href.indexOf("www.example.com/product") > -1) {
    AWIN.Tracking.RTBLnF.pageType = 'product';
else if (window.location.href.indexOf("www.example.com/cart") > -1) {
    AWIN.Tracking.RTBLnF.pageType = 'basket';
}
else if (AWIN.Tracking.Sale) {
        AWIN.Tracking.RTBLnF.pageType = 'checkout';
}
```




## Deactivate the tag on specific page type/landing page

In order to deactivate publisher script on desired page, use
AWIN.Tracking.RTBLnF.disableFlag = 'true';


``` javascript
if (window.location.href.indexOf("www.example.com/desired/page/") > -1) {
//  deactivate the script on specific page
    AWIN.Tracking.RTBLnF.disableFlag = 'true';
}
```




## Requests

**Tempalte**


``` javascript
http://pixel.sitescout.com/iap/{pageType_siteScoutPixelId}
```



**Example**


``` javascript
http://pixel.sitescout.com/iap/0cc66dd47dd48b60
```


