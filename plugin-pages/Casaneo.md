
# Supported Pages

- Landing page
- Product page
- Cart View page (basket page)
- Search page
- Customer data page
- Category page
- Checkout Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Landing Page Configuration

``` javascript
AWIN.Tracking.Casaneo = AWIN.Tracking.Casaneo || {};
AWIN.Tracking.Casaneo.pagetype = "SPECIFY_PAGE_TYPE";
AWIN.Tracking.Casaneo.token = "TOKEN";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.Casaneo = AWIN.Tracking.Casaneo || {};
AWIN.Tracking.Casaneo.pagetype = "SPECIFY_PAGE_TYPE";
AWIN.Tracking.Casaneo.token = "TOKEN";
AWIN.Tracking.Casaneo.identifier = "ID";
AWIN.Tracking.Casaneo.name = "NAME";
AWIN.Tracking.Casaneo.amount = "AMOUNT";
```



## Cart View Page Configuration

Requires Awin basket or awin products array to be implemented on
merchant's site.

Example Awin products array is shown at the bottom of this document.

``` javascript
AWIN.Tracking.Casaneo = AWIN.Tracking.Casaneo || {};
AWIN.Tracking.Casaneo.pagetype = "SPECIFY_PAGE_TYPE";
AWIN.Tracking.Casaneo.token = "TOKEN";
```



## Search Page Configuration

``` javascript
AWIN.Tracking.Casaneo = AWIN.Tracking.Casaneo || {};
AWIN.Tracking.Casaneo.pagetype = "SPECIFY_PAGE_TYPE";
AWIN.Tracking.Casaneo.token = "TOKEN";
```



## Customer Data Page Configuration

``` javascript
AWIN.Tracking.Casaneo = AWIN.Tracking.Casaneo || {};
AWIN.Tracking.Casaneo.pagetype = "SPECIFY_PAGE_TYPE";
AWIN.Tracking.Casaneo.token = "TOKEN";
AWIN.Tracking.Casaneo.aw_products = "PROVIDE_AWIN_PRODUCTS_ARRAY";
```



## Category Page Configuration

``` javascript
AWIN.Tracking.Casaneo = AWIN.Tracking.Casaneo || {};
AWIN.Tracking.Casaneo.pagetype = "SPECIFY_PAGE_TYPE";
AWIN.Tracking.Casaneo.token = "TOKEN";
```



## Checkout Page Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented.

``` javascript
AWIN.Tracking.Casaneo = AWIN.Tracking.Casaneo || {};
AWIN.Tracking.Casaneo.pagetype = "SPECIFY_PAGE_TYPE";
AWIN.Tracking.Casaneo.token = "TOKEN";
```



## Example Awin Products Array

=

``` javascript
AWIN.Tracking.Casaneo.aw_products: [
    {id: "123456", price: "3.99", quantity: "1"},
    {id: "23456", price: "5.99", quantity: "
],
```



# Relevant Tickets

[PROD-6050](https://jira.awin.com/browse/PROD-6050)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/casaneo.js)