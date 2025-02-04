
# Supported Pages

- Basket
- Category
- Checkout
- Product
- Search

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values. Plugin supports zanox
parameters. Refer to the [source
code](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/ad4matTravel.js)
for more details.

## Basket

Configuration object

``` javascript
AWIN.Tracking.Ad4matTravel = AWIN.Tracking.Ad4matTravel || {};
AWIN.Tracking.Ad4matTravel.adspaceId = "SPECIFIC_AD4MAT_ADVERTISER_ID";
AWIN.Tracking.Ad4matTravel.pagetype = "SPECIFIC_PAGE_TYPE"; //Required
AWIN.Tracking.Ad4matTravel.country = "COUNTRY";
AWIN.Tracking.Ad4matTravel.country2 = "COUNTRY_2";
```


Example Awin Basket (Required)

``` javascript
<form name="aw_basket_form">
    <textarea id="aw_basket">
        AW:P|1001|test1234|123456|Test Product 1|3.99|1|sku2116|DEFAULT|DVD
        AW:P|1001|test1234|23456|Test Product 2|5.99|2|sku232|DEFAULT|Electronics
    </textarea>
</form>
```



## Category

``` javascript
AWIN.Tracking.Ad4matTravel = AWIN.Tracking.Ad4matTravel || {};
AWIN.Tracking.Ad4matTravel.adspaceId = "SPECIFIC_AD4MAT_ADVERTISER_ID";
AWIN.Tracking.Ad4matTravel.pagetype = "SPECIFIC_PAGE_TYPE"; //Required
AWIN.Tracking.Ad4matTravel.category = "CATEGORY";
AWIN.Tracking.Ad4matTravel.searchQuery = "SEARCH_QUERY";
AWIN.Tracking.Ad4matTravel.destination = "DESTINATION_NAME";
AWIN.Tracking.Ad4matTravel.startDate = "START_DATE";
AWIN.Tracking.Ad4matTravel.endDate = "END_DATE";
AWIN.Tracking.Ad4matTravel.room = "ROOM_NUMBER";
AWIN.Tracking.Ad4matTravel.adult = "NUMBER_OF_ADULT";
AWIN.Tracking.Ad4matTravel.child = "NUMBER_OF_CHILDREN";
AWIN.Tracking.Ad4matTravel.stars = "NUMBER_OF_STARTS";
AWIN.Tracking.Ad4matTravel.country = "COUNTRY";
AWIN.Tracking.Ad4matTravel.country2 = "COUNTRY_2";
```



## Checkout

``` javascript
AWIN.Tracking.Ad4matTravel = AWIN.Tracking.Ad4matTravel || {};
AWIN.Tracking.Ad4matTravel.adspaceId = "SPECIFIC_AD4MAT_ADVERTISER_ID";
AWIN.Tracking.Ad4matTravel.pagetype = "SPECIFIC_PAGE_TYPE"; //Required
AWIN.Tracking.Ad4matTravel.country = "COUNTRY";
AWIN.Tracking.Ad4matTravel.country2 = "COUNTRY_2";
```



## Product

``` javascript
AWIN.Tracking.Ad4matTravel = AWIN.Tracking.Ad4matTravel || {};
AWIN.Tracking.Ad4matTravel.adspaceId = "SPECIFIC_AD4MAT_ADVERTISER_ID";
AWIN.Tracking.Ad4matTravel.pagetype = "SPECIFIC_PAGE_TYPE"; //Required
AWIN.Tracking.Ad4matTravel.identifier = "IDENTIFIER";
AWIN.Tracking.Ad4matTravel.category = "CATEGORY";
AWIN.Tracking.Ad4matTravel.destination = "DESTINATION_NAME";
AWIN.Tracking.Ad4matTravel.destination2 = "DESTINATION_NAME_2";
AWIN.Tracking.Ad4matTravel.startDate = "START_DATE";
AWIN.Tracking.Ad4matTravel.endDate = "END_DATE";
AWIN.Tracking.Ad4matTravel.image = "IMAGE";
AWIN.Tracking.Ad4matTravel.country = "COUNTRY";
AWIN.Tracking.Ad4matTravel.country2 = "COUNTRY_2";
```



## Search

``` javascript
AWIN.Tracking.Ad4matTravel = AWIN.Tracking.Ad4matTravel || {};
AWIN.Tracking.Ad4matTravel.adspaceId = "SPECIFIC_AD4MAT_ADVERTISER_ID";
AWIN.Tracking.Ad4matTravel.pagetype = "SPECIFIC_PAGE_TYPE"; //Required
AWIN.Tracking.Ad4matTravel.searchQuery = "SEARCH_QUERY";
AWIN.Tracking.Ad4matTravel.destination = "DESTINATION_NAME";
AWIN.Tracking.Ad4matTravel.startDate = "START_DATE";
AWIN.Tracking.Ad4matTravel.endDate = "END_DATE";
AWIN.Tracking.Ad4matTravel.room = "ROOM_NUMBER";
AWIN.Tracking.Ad4matTravel.adult = "NUMBER_OF_ADULT";
AWIN.Tracking.Ad4matTravel.child = "NUMBER_OF_CHILDREN";
AWIN.Tracking.Ad4matTravel.stars = "NUMBER_OF_STARTS";
AWIN.Tracking.Ad4matTravel.country = "COUNTRY";
AWIN.Tracking.Ad4matTravel.country2 = "COUNTRY_2";
```



# Relevant Tickets

Not Found

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/ad4matTravel.js)