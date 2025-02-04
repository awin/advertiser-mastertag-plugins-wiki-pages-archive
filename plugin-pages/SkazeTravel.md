
# Integration requirements

The Dwin1 tag needs to be displayed on every page including the
confirmation page as part of the Awin conversion tracking.

# How is the tag implemented?

Skaze Travel plugin has been developed for travel advertisers.
Implementation for retail advertisers is also available. For more
information please refer to Skaze Retail plugin.

The Skaze Travel plugin has different tags depending on the type of page
visited and requires providing custom data via variables described
below.

Plugin supports following `PAGETYPE`: funnel2-book, funnel3-pay.

Generic pages, such as Home, landing, all or funnel 1 implement the same
script, therefore they do not have dedicated pageTypes implemented
within the plugin.

Default Skaze API calls will be automatically added to all pages and
checkout page will be automatically detected if AWIN.Tracking.Sale tag
is implemented.

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | Skaze Retail      |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

## IMPORTANT:

advertiserId must be provided on every page for this plugin to work
(ideally defined once as a top level variable)

Page keys must be provided for funnel 1 and funnel 2 pages, otherwsise
the plugin will not work as expected.

(values in `UPPER_CASE_WITH_UNDERSCORES` should be replaced with the
appropriate values)

# General Page Configuration \|\| Funnel 1 \|\| Landing Page \|\| Home page \|\| All Pages

The code below goes into the plugin setup field in the tag management
form.

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.

In order to implement plugin on all pages the below configuration is
required:


``` javascript
//Object should be created in our configuration
AWIN.Tracking.skazeTravel = AWIN.Tracking.skazeRetailer || {};
AWIN.Tracking.skazeTravel.advertiserId =ADVERTISER_ID; //Assigned in Awin cofiguration
AWIN.Tracking.skazeTravel.pageName = PAGE NAME; //Assigned in Awin configuration
```



Example:


``` javascript
AWIN.Tracking.skazeTravel = AWIN.Tracking.skazeRetailer || {};
AWIN.Tracking.skazeTravel.advertiserId = "1001";
AWIN.Tracking.skazeTravel.pageName = "my home page";
```




## Funnel 2 - book Page

This plugin requires a lot of custom parameters unavailable from Awin
MasterTag, therefore it certain fields to be provided by the client on
their page.

Please refer to comments in the script for information about which
variables can be configured by us and which should be provided by the
client. If a variable is not provided, it will be replaced with an empty
space.


``` javascript
AWIN.Tracking.skazeTravel = AWIN.Tracking.skazeRetailer || {};
AWIN.Tracking.skazeTravel.pageName = PAGE_Name;
AWIN.Tracking.skazeTravel.advertiserId = ADVERTISER_ID;
//Fields to be provided by the client
AWIN.Tracking.skazeTravel.pageType = PAGE_Name;
AWIN.Tracking.skazeTravel.price = PRICE;
AWIN.Tracking.skazeTravel.travelers = TRAVELLERS;
AWIN.Tracking.skazeTravel.going = {
checkIn: CHECK_IN,
checkOut: CHECK_OUT,
cityIn: CITY_IN,
cityOut: CITY_OUT,
plan: PLAN,
price: PRICE,
};
AWIN.Tracking.skazeTravel.coming = {
checkIn: CHECK_IN,
checkOut: CHECK_OUT,
cityIn: CITY_IN,
cityOut: CITY_OUT,
plan: PLAN,
price: PRICE,
};
```




## Funnel 3 - pay Page

If a variable is not provided, it will be replaced with a empty text


``` javascript
AWIN.Tracking.skazeTravel = AWIN.Tracking.skazeRetailer || {};
AWIN.Tracking.skazeTravel.pageName = PAGE_Name</code>;
AWIN.Tracking.skazeTravel.advertiserId = ADVERTISER_ID;
//Fields to be provided by the client
AWIN.Tracking.skazeTravel.pageType = PAGE_Name;
AWIN.Tracking.skazeTravel.price = ADVERTISER_ID;
AWIN.Tracking.skazeTravel.travelers = TRAVELLERS;
AWIN.Tracking.skazeTravel.going = {
checkIn: CHECK_IN,
checkOut: CHECK_OUT,
cityIn: CITY_IN,
cityOut: CITY_OUT,
plan: PLAN,
price: PRICE,
};
AWIN.Tracking.skazeTravel.coming = {
checkIn: CHECK_IN,
checkOut: CHECK_OUT,
cityIn: CITY_IN,
cityOut: CITY_OUT,
plan: PLAN,
price: PRICE,
};
```




## Checkout Page

The plugin will automatically detect if the user is located on the
checkout page if AWIN.Tracking.Sale variable is preset. However,
specifying the pageType variable will override this behaviour.

Order Id, order value, promo code (voucher code) and currency will be
populated based on the data recieved in AWIN.Tracking.Sale, however
other fields will need to be provided.


``` javascript
AWIN.Tracking.skazeTravel = AWIN.Tracking.skazeRetailer || {};
AWIN.Tracking.skazeTravel.advertiserId = ADVERTISER_ID;
AWIN.Tracking.skazeTravel.pageName = PAGE_NAME;
//All fields below should be provided by the client
AWIN.Tracking.skazeTravel.alreadyClient = IS_ALREADY_CLIENT;
AWIN.Tracking.skazeTravel.emailMD5 = EMAIL_MD5;
AWIN.Tracking.skazeTravel.emailSHA256 = EMAIL_SHA256;
AWIN.Tracking.skazeTravel.phoneMD5 = PHONE_MD5;
AWIN.Tracking.skazeTravel.phoneSHA256 = PHONE_SHA256;
AWIN.Tracking.skazeTravel.travelers = TRAVELLERS;

AWIN.Tracking.skazeTravel.going = {
checkIn: CHECK_IN,
checkOut: CHECK_OUT,
cityIn: CITY_IN,
cityOut: CITY_OUT,
plan: PLAN,
price: PRICE,
};

AWIN.Tracking.skazeTravel.coming = {
checkIn: CHECK_IN,
checkOut: CHECK_OUT,
cityIn: CITY_IN,
cityOut: CITY_OUT,
plan: PLAN,
price: PRICE,
};
```




## Plugin Code


``` javascript
AWIN.Tracking.skazeTravel = AWIN.Tracking.skazeTravel || {};
AWIN.Tracking.skazeTravel.url = AWIN.Tracking.skazeTravel.url || "//events.sk.ht/";

var event = {};

(function ($a) {
    let urlWithParams = AWIN.Tracking.skazeTravel.url + $a.advertiserId + "/lib.js";
    AWIN.Tracking.scriptAppend(urlWithParams, null, null, {async: "async"});

    var skaze = skaze || {};
    skaze.cmd = skaze.cmd || [];

    event = {
        name : $a.advertiserId + " " + $a.pageName || "",
        properties: {}
    };

    if (typeof $a.pageType !== "undefined" && typeof AWIN.Tracking.Sale === "undefined") {
        switch ($a.pageType.toLowerCase()) {
            case "funnel2-book":
            case "funnel3-pay":
                event.properties = {
                    price: $a.price || "",
                    travelers: $a.travelers || "",
                    going: {
                        checkIn: $a.going.checkIn || "",
                        checkOut: $a.going.checkOut || "",
                        cityIn: $a.going.cityIn || "",
                        cityOut: $a.going.cityOut || "",
                        plan: $a.going.plan || "",
                        price: $a.going.price || "",
                    },
                    coming: {
                        checkIn: $a.coming.checkIn || "",
                        checkOut: $a.coming.checkOut|| "",
                        cityIn: $a.coming.cityIn || "",
                        cityOut: $a.coming.cityOut || "",
                        plan: $a.coming.plan || "",
                        price: $a.coming.price || "",
                    }
                };
                break;
        }
    } else if (typeof AWIN.Tracking.Sale !== "undefined") {
        event.properties = {
            orderId: AWIN.Tracking.Sale.orderRef,
            orderValue: AWIN.Tracking.Sale.saleAmount,
            emailMD5: $a.emailMD5 || "",
            emailSHA256: $a.emailSHA256 || "",
            phoneMD5: $a.phoneMD5 || "",
            phoneSHA256: $a.phoneSHA256 || "",
            travelers: $a.travelers || "",
            going: {
                checkIn: $a.going.checkIn || "",
                checkOut: $a.going.checkOut || "",
                cityIn: $a.going.cityIn || "",
                cityOut: $a.going.cityOut || "",
                plan: $a.going.plan || "",
                price: $a.going.price || "",
            },
            coming: {
                checkIn: $a.coming.checkIn || "",
                checkOut: $a.coming.checkOut || "",
                cityIn: $a.coming.cityIn || "",
                cityOut: $a.coming.cityOut || "",
                plan: $a.coming.plan || "",
                price: $a.coming.price || "",
            }
        };
    }

    skaze.cmd.push(function() {
        skaze.init({ siteIdentifier : $a.advertiserId });
        skaze.pushEvent(event);
    });
})(AWIN.Tracking.skazeTravel);
```


