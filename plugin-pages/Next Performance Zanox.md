
# Supported Pages

- Home Page
- Category Page
- Product Page
- Basket Page
- Checkout Page
- Registration Page

# Configuration

Plugin supports Zanox parameters. Refer to the source code for more
details.

Replace `"VALUE_PLACEHOLDERS"` with real values.

### Language

If defined, allowed values are "fr" and "nl".


``` javascript
AWIN.Tracking.NextPerformanceZanox.language = "LANGUAGE_ID";
```




### Token

When language is set to fr, property tokenFR must be set. When language
is set to nl, property tokenNL must be set. When language is not set,
property token must be set.


``` javascript
AWIN.Tracking.NextPerformanceZanox.token = "TOKEN";
AWIN.Tracking.NextPerformanceZanox.tokenNL = "TOKEN NL";
AWIN.Tracking.NextPerformanceZanox.tokenFR = "TOKEN FR";
```




## Home Page Configuration


``` javascript
AWIN.Tracking.NextPerformanceZanox = AWIN.Tracking.NextPerformanceZanox || {};
AWIN.Tracking.NextPerformanceZanox.pagetype = "home";
AWIN.Tracking.NextPerformanceZanox.tokenFR = "TOKEN_FR";
AWIN.Tracking.NextPerformanceZanox.language = "fr";
```




## Registration Page Configuration


``` javascript
AWIN.Tracking.NextPerformanceZanox = AWIN.Tracking.NextPerformanceZanox || {};
AWIN.Tracking.NextPerformanceZanox.pagetype = "registration";
AWIN.Tracking.NextPerformanceZanox.tokenFR = "TOKEN_FR";
AWIN.Tracking.NextPerformanceZanox.language = "fr";
```




## Basket Page Configuration


``` javascript
AWIN.Tracking.NextPerformanceZanox = AWIN.Tracking.NextPerformanceZanox || {};
AWIN.Tracking.NextPerformanceZanox.pagetype = "basket";
AWIN.Tracking.NextPerformanceZanox.tokenFR = "TOKEN_FR";
AWIN.Tracking.NextPerformanceZanox.language = "fr";
```




## Category Page Configuration


``` javascript
AWIN.Tracking.NextPerformanceZanox = AWIN.Tracking.NextPerformanceZanox || {};
AWIN.Tracking.NextPerformanceZanox.pagetype = "category";
AWIN.Tracking.NextPerformanceZanox.tokenFR = "TOKEN_FR";
AWIN.Tracking.NextPerformanceZanox.language = "fr";
AWIN.Tracking.NextPerformanceZanox.categoryId = "CATEGORY_ID";
```




## Product Page Configuration


``` javascript
AWIN.Tracking.NextPerformanceZanox = AWIN.Tracking.NextPerformanceZanox || {};
AWIN.Tracking.NextPerformanceZanox.pagetype = "category";
AWIN.Tracking.NextPerformanceZanox.tokenFR = "TOKEN_FR";
AWIN.Tracking.NextPerformanceZanox.language = "fr";
AWIN.Tracking.NextPerformanceZanox.identifier = "IDENTIFIER_ID";
```




## Checkout Page Configuration


``` javascript
AWIN.Tracking.NextPerformanceZanox = AWIN.Tracking.NextPerformanceZanox || {};
AWIN.Tracking.NextPerformanceZanox.pagetype = "category";
AWIN.Tracking.NextPerformanceZanox.tokenFR = "TOKEN_FR";
AWIN.Tracking.NextPerformanceZanox.language = "fr";
AWIN.Tracking.NextPerformanceZanox.valid = "VALID_ID";
```




## Related JIRA Ticket

[PROD-3270](https://jira.awin.com/browse/PROD-3270)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/nextPerformanceZanox.js)