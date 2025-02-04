# MyThings Europe (Mastertag version)

## Description

**Note:** This plugin was migrated from zanox Mastertag so supports
legacy parameters but clients should be encouraged to use our standard
parameters.

## Integration Requirements

|                      |                        |
|----------------------|------------------------|
| **Plugin Type**      | MyThingsZanox          |
| **Plugin Setup**     | See Code Below         |
| **Active**           | Tick the box           |
| **Required Plugins** | Product Level Tracking |

### Plugin Setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `ADVERTISERTOKEN` with value supplied by MyThings Europe.

``` javascript
AWIN.Tracking.MyThingsZanox = {};
AWIN.Tracking.MyThingsZanox.advertiserToken = "ADVERTISERTOKEN";
```

## Merchant page configurations

The following details the requirements of merchant’s pages for this
plugin at this time. These are based on the configuration system of the
older Mastertag implementation so should not require reconfiguration for
migration.

Replace `PAGETYPE` with the appropriate value from the below sections.

``` javascript
AWIN.Tracking.MyThingsZanox.pagetype = "PAGETYPE";
```

### Home Page

- Replace `PAGETYPE` above with `"home"`

### Basket Page

- Replace `PAGETYPE` above with `"basket"`

### Category Page

- Replace `PAGETYPE` above with `"category"`
- Replace `URL` with the category url.
- Replace `CATEGORY` with the category.

``` javascript
AWIN.Tracking.MyThingsZanox.detailUrl = "URL";
AWIN.Tracking.MyThingsZanox.category = "CATEGORY";
```

### Checkout Page

- Does not require the pagetype parameter. Uses \`AWIN.Tracking.Sale\`
  to detect this page.

### Registration Page

- Replace `PAGETYPE` above with `"registration"`
- Replace `TRANSACTIONID` with the transaction ID.
- Replace `TOTALAMOUNT` with the total transaction amount.
- Replace `TOTALCURRENCY` with the currency of the total.

### Product Page

- Replace `PAGETYPE` above with `"product"`
- Replace `IDENTIFIER` with the product ID.
- Replace `PRODUCTNAME` with the product name.
- Replace `CATEGORY` with the product category.
- Replace `BRAND` with the brand name.
- Replace `PRICE` with the product price.
- Replace `CURRENCY` with the sale currency.
- Replace `URL` with the product URL.
- Replace `IMAGEURL` with the URL for the product image.

``` javascript
AWIN.Tracking.MyThingsZanox.identifier = "IDENTIFIER";
AWIN.Tracking.MyThingsZanox.productName = "PRODUCTNAME";
AWIN.Tracking.MyThingsZanox.category = "CATEGORY";
AWIN.Tracking.MyThingsZanox.brand = "BRAND";
AWIN.Tracking.MyThingsZanox.price = "PRICE";
AWIN.Tracking.MyThingsZanox.currency = "CURRENCY";
AWIN.Tracking.MyThingsZanox.detailUrl = "URL";
AWIN.Tracking.MyThingsZanox.imageUrl = "IMAGEURL";
```

### Search Page

- Replace `PAGETYPE` above with `"search"`
- Replace `SEARCHQUERY` with the search query.
- Replace `IDENTIFIER` with a unique identifier.

``` javascript
AWIN.Tracking.MyThingsZanox.searchQuery = "SEARCHQUERY";
AWIN.Tracking.MyThingsZanox.identifier = "IDENTIFIER"
```

### Search Page with Location

- Replace `PAGETYPE` above with `"search"`
- Replace `SEARCHQUERY` with the search query.
- Replace `SEARCHCITY` with the destination city.
- Replace `SEARCHCOUNTRY` with the destination country.

``` javascript
AWIN.Tracking.MyThingsZanox.searchQuery = "SEARCHQUERY";
AWIN.Tracking.MyThingsZanox.searchCity = "SEARCHCITY";
AWIN.Tracking.MyThingsZanox.searchCountry = "SEARCHCOUNTRY";
```

## Mastertag Legacy configuration documents

[Advertiser Mastertag Set-up Guide](Media:MasterTagSetup.pdf "wikilink")