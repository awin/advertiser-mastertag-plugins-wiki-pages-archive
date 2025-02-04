
# Supported Pages

- Home Page
- Basket Page
- Category Page
- Product Page
- Checkout Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

Accepted pagetype values are: product, basket, category, home, checkout.

## Home Page Configuration

``` javascript
AWIN.Tracking.AdvantageMedia = AWIN.Tracking.AdvantageMedia || {};
AWIN.Tracking.AdvantageMedia.customerId = "CUSTOMER_ID";
AWIN.Tracking.AdvantageMedia.pagetype = "PAGE_TYPE";
```



## Basket Page Configuration

Basket Page requires Product Level Tracking to be implemented on
merchant's website.

``` javascript
AWIN.Tracking.AdvantageMedia = AWIN.Tracking.AdvantageMedia || {};
AWIN.Tracking.AdvantageMedia.customerId = "CUSTOMER_ID";
AWIN.Tracking.AdvantageMedia.pagetype = "PAGE_TYPE";
```



## Category Page Configuration

``` javascript
AWIN.Tracking.AdvantageMedia = AWIN.Tracking.AdvantageMedia || {};
AWIN.Tracking.AdvantageMedia.customerId = "CUSTOMER_ID";
AWIN.Tracking.AdvantageMedia.pagetype = "PAGE_TYPE";
AWIN.Tracking.AdvantageMedia.category = "CATEGORY";
```



## Product Page Configuration

Basket Page requires Product Level Tracking to be implemented on
merchant's website.

``` javascript
AWIN.Tracking.AdvantageMedia = AWIN.Tracking.AdvantageMedia || {};
AWIN.Tracking.AdvantageMedia.customerId = "CUSTOMER_ID";
AWIN.Tracking.AdvantageMedia.pagetype = "PAGE_TYPE";
AWIN.Tracking.AdvantageMedia.identifier = "IDENTIFYER";
```



## Checkout Page Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website.

``` javascript
AWIN.Tracking.AdvantageMedia = AWIN.Tracking.AdvantageMedia || {};
AWIN.Tracking.AdvantageMedia.customerId = "CUSTOMER_ID";
AWIN.Tracking.AdvantageMedia.pagetype = "PAGE_TYPE";
```



# Relevant Tickets

NOT FOUND

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/advantageMedia.js)