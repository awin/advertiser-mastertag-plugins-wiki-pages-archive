# RTB House

## Description

**Note:** This plugin was migrated from zanox Mastertag so supports
legacy parameters but clients should be encouraged to use our standard
parameters.

## Integration Requirements

|                      |                        |
|----------------------|------------------------|
| **Plugin Type**      | RTBHouse               |
| **Plugin Setup**     | See Code Below         |
| **Active**           | Tick the box           |
| **Required Plugins** | Product Level Tracking |

### Plugin Setup code

The code below goes into the plugin setup field in the tag management
form.

Replace `TOKEN` with real value supplied by RTB House.

``` javascript
AWIN.Tracking.RTBHouse = {};
AWIN.Tracking.RTBHouse.token = "TOKEN";
```

## Merchant page configurations

The following details the requirements of merchant’s pages for this
plugin at this time. These are based on the configuration system of the
older Mastertag implementation so should not require reconfiguration for
migration.

Replace `PAGETYPE` with the appropriate value from the below sections.

``` javascript
AWIN.Tracking.RTBHouse.pagetype = "PAGETYPE";
```

### Home Page

- Replace `PAGETYPE` above with `"home"`.

### Checkout Page

- Does not require the pagetype parameter. Uses `AWIN.Tracking.Sale` to
  detect this page.

### Product Page

- Replace `PAGETYPE` above with `"product"`.
- Replace `IDENTIFIER` with the product ID.

``` javascript
AWIN.Tracking.RTBHouse.identifier = "IDENTIFIER";
```

### Basket Page

- Replace `PAGETYPE` above with `"basket"`.

## Mastertag Legacy configuration documents

[Advertiser Mastertag Set-up Guide](Media:MasterTagSetup.pdf "wikilink")