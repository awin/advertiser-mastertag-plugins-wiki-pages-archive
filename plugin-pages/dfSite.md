
# Supported Pages

- Home page
- Product page
- Category page
- Basket page
- Checkout page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin supports Zanox parameters. Refer to the source code for more
details.

## Home Page Configuration

``` javascript
AWIN.Tracking.DFSites = AWIN.Tracking.DFSites || {};
AWIN.Tracking.DFSites.mtid = "MTID";
AWIN.Tracking.DFSites.token = "TOKEN";
AWIN.Tracking.DFSites.pagetype = "PAGE_TYPE";
```



## Basket Page Configuration

Requires Product Level Tracking to be implemented.

``` javascript
AWIN.Tracking.DFSites = AWIN.Tracking.DFSites || {};
AWIN.Tracking.DFSites.mtid = "MTID";
AWIN.Tracking.DFSites.token = "TOKEN";
AWIN.Tracking.DFSites.pagetype = "PAGE_TYPE";
```



Example Awin basket:

``` javascript
<form name="aw_basket_form">
    <textarea id="aw_basket">
        AW:P|1001|test1234|123456|Test Product 1|3.99|1|sku2116|DEFAULT|DVD
        AW:P|1001|test1234|23456|Test Product 2|5.99|2|sku232|DEFAULT|Electronics
    </textarea>
</form>
```



## Category Page Configuration

``` javascript
AWIN.Tracking.DFSites = AWIN.Tracking.DFSites || {};
AWIN.Tracking.DFSites.mtid = "MTID";
AWIN.Tracking.DFSites.token = "TOKEN";
AWIN.Tracking.DFSites.pagetype = "PAGE_TYPE";
AWIN.Tracking.DFSites.category = "CATEGORY";
```



## Checkout Page Configuration

Requires AWIN.Tracking.Sale object to be implemented on merchant's site.

``` javascript
AWIN.Tracking.DFSites = AWIN.Tracking.DFSites || {};
AWIN.Tracking.DFSites.mtid = "MTID";
AWIN.Tracking.DFSites.token = "TOKEN";
AWIN.Tracking.DFSites.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.DFSites = AWIN.Tracking.DFSites || {};
AWIN.Tracking.DFSites.mtid = "MTID";
AWIN.Tracking.DFSites.token = "TOKEN";
AWIN.Tracking.DFSites.pagetype = "PAGE_TYPE";
AWIN.Tracking.DFSites.identifier = "ID";
AWIN.Tracking.DFSites.productName = "PRODUCT_NAME";
AWIN.Tracking.DFSites.price = "PRICE";
```



# Relevant Tickets

[PROD-3312](https://jira.awin.com/browse/PROD-3312)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/dfSites.js)