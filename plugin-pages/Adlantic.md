# Adlantic

## Description

**Note:** This plugin was migrated from zanox Mastertag so supports
legacy parameters but clients should be encouraged to use our standard
parameters.

## Integration Requirements

|                      |                        |
|----------------------|------------------------|
| **Plugin Type**      | Adlantic               |
| **Plugin Setup**     | See Code Below         |
| **Active**           | Tick the box           |
| **Required Plugins** | Product Level Tracking |

### Plugin Setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `TOKEN` with real value supplied by Adlantic.

``` javascript
AWIN.Tracking.Adlantic = {};
AWIN.Tracking.Adlantic.token = "TOKEN"
```

## Merchant page configurations

The following details the requirements of merchant’s pages for this
plugin at this time. These are based on the configuration system of the
older Mastertag implementation so should not require reconfiguration for
migration.

Replace `PAGETYPE` with the appropriate value from the below sections.

``` javascript
AWIN.Tracking.Adlantic.pagetype = "PAGETYPE";
```

### Checkout Page

- Does not require the pagetype parameter. Uses `AWIN.Tracking.Sale` to
  detect this page.

### Product Page

- Replace `PAGETYPE` above with `"product"`.
- Replace `IDENTIFIER` with the product ID.
- Replace `CATEGORY` with the product category.

``` javascript
AWIN.Tracking.Adlantic.identifier = "IDENTIFIER";
AWIN.Tracking.Adlantic.category = "CATEGORY";
```

### Category Page

- Replace `PAGETYPE` above with `"category"`.
- Replace `CATEGORY` with the product category.

``` javascript
AWIN.Tracking.Adlantic.category = "CATEGORY";
```

### Search Page

- Replace `PAGETYPE` above with `"search"`.
- Replace `SEARCHQUERY` with the search query text.

``` javascript
AWIN.Tracking.Adlantic.searchQuery = "SEARCHQUERY";
```

### Basket Page

- Replace `PAGETYPE` above with `"basket"`.

## Mastertag Legacy configuration documents

[Advertiser Mastertag Set-up Guide](Media:MasterTagSetup.pdf "wikilink")