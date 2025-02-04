
# Supported Pages

- All

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Configuration

``` javascript
AWIN.Tracking.Constant = AWIN.Tracking.Constant || {};
AWIN.Tracking.Constant.url = "URL";
```



## Configuration for Very

``` javascript
AWIN.Tracking.Constant = AWIN.Tracking.Constant || {};
AWIN.Tracking.Constant.url =
    "https://cdn.constant.co/app/very/cc.js?" + (Date.now() / 3.6e+6).toFixed();
```



# Relevant Tickets

[PROD-8394](https://jira.awin.com/browse/PROD-8394)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/master/web/thirdparty/constant.js)