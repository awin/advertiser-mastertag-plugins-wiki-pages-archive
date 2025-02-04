# Spotney

## Description

**Note:** This plugin was migrated from zanox Mastertag so supports
legacy parameters but clients should be encouraged to use our standard
parameters.

## Integration Requirements

|                  |                |
|------------------|----------------|
| **Plugin Type**  | Spotney        |
| **Plugin Setup** | See Code Below |
| **Active**       | Tick the box   |

### Plugin Setup code

The code below goes into the plugin setup field in the tag management
form.
**Note:** All fields are required though there can be as many tokens as
you need.

- Replace `CATEGORYTEST` with the text to match the category against.
- Replace `TOKENVALUE` with the token for the url if the category
  matches.
- Change `DEFAULTACTIVE` to enable a default token if no check succeeds
  (`true`\|`false`)
- Replace `DEFAULTVALUE` with the default token.

``` javascript
AWIN.Tracking.Spotney = {};
AWIN.Tracking.Spotney.tokens = [
  {
    check: "CATEGORYTEST",
    value: "TOKENVALUE"
  }, {
    // ... Additional tokens allowed
  }
];
AWIN.Tracking.Spotney.checkAll = {
  active: "DEFAULTACTIVE",
  value: "DEFAULTVALUE"
};
```

## Merchant page configurations

The following details the requirements of merchant’s pages for this
plugin at this time. These are based on the configuration system of the
older Mastertag implementation so should not require reconfiguration for
migration.

Replace `PAGETYPE` with the appropriate value from the below sections.

``` javascript
AWIN.Tracking.Spotney.pagetype = "PAGETYPE";
```

### Product Page

- Replace `PAGETYPE` above with `"product"`.

### Category Page

- Replace `PAGETYPE` above with `"category"`.

## Mastertag Legacy configuration documents

[Advertiser Mastertag Set-up Guide](Media:MasterTagSetup.pdf "wikilink")