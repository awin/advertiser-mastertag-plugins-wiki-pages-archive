
## Description

**Notes:** This plugin was migrated from zanox Mastertag so supports
legacy parameters but clients should be encouraged to use our standard
parameters.

## Integration Requirements

|                  |                |
|------------------|----------------|
| **Plugin Type**  | Fanplayr       |
| **Plugin Setup** | See Code Below |
| **Active**       | Tick the box   |

### Plugin Setup code

The code below goes into the plugin setup field in the tag management
form.

- Replace `ACCOUNT_ID` with real value supplied by Fanplyr.
- Replace `DOMAIN` with the domain value (matches the `d` parameter in
  the url).
- Replace `PAGETYPE` with the pagetype value (matches the `pt` parameter
  in the url).
- Replace `CART_URL` with the "apply to cart URL" value (matches the
  `atc` parameter in the url).
- Replace `DEPUTIZE_URL` with the "deputize URL" value (matches the
  `dep` parameter in the url).
- Replace `TOTALLY_CUSTOM_SCRIPT` with the "totally custom script" value
  (matches the `tcs` parameter in the url).
- Replace `DOT_AS_DECIMAL` with the "dot as decimal" value (matches the
  `dd` parameter in the url).


``` javascript
AWIN.Tracking.Fanplayr = {};
AWIN.Tracking.Fanplayr.accountId = "ACCOUNT_ID";
AWIN.Tracking.Fanplayr.domain = "DOMAIN";
AWIN.Tracking.Fanplayr.pagetype = "PAGETYPE";
AWIN.Tracking.Fanplayr.cartUrl = "CART_URL";
AWIN.Tracking.Fanplayr.deputizeUrl = "DEPUTIZE_URL";
AWIN.Tracking.Fanplayr.totallyCustomScript = "TOTALLY_CUSTOM_SCRIPT";
AWIN.Tracking.Fanplayr.dotAsDecimal = "DOT_AS_DECIMAL";
```


## Mastertag Legacy configuration documents

[Advertiser Mastertag Set-up Guide](Media:MasterTagSetup.pdf "wikilink")

## Working Example


``` javascript
AWIN.Tracking.Fanplayr = AWIN.Tracking.Fanplayr || {};
AWIN.Tracking.Fanplayr.accountId = "0cd4bb73b6012bc071c3b137d31b07d5";
AWIN.Tracking.Fanplayr.domain = "emozione3.it";
AWIN.Tracking.Fanplayr.pagetype = "generic";
AWIN.Tracking.Fanplayr.cartUrl = "http://pro.emozione3.it/zax-fp1511?discountCode=%c";
AWIN.Tracking.Fanplayr.deputizeUrl = "";
AWIN.Tracking.Fanplayr.totallyCustomScript = "";
AWIN.Tracking.Fanplayr.dotAsDecimal = "";

if (dataLayer[1].pagytype == "product") {
    AWIN.Tracking.Fanplayr.pagetype = "product";
} else if (dataLayer[1].pagytype == "category"){
    AWIN.Tracking.Fanplayr.pagetype = "category";
}
```

