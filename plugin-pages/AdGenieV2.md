
# Supported Pages

- Basket page
- Checkout page
- Product page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

Plugin has been developed as part of Helix migration. To see zanox
supported parameters view the source code at the bottom of this
document.

## Basket Page Configuration

``` javascript
AWIN.Tracking.AdGenieV2 = AWIN.Tracking.AdGenieV2 || {};
AWIN.Tracking.AdGenieV2.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.AdGenieV2.merchantId = "MERCHANT_ID";
AWIN.Tracking.AdGenieV2.pagetype = "PAGE_TYPE";
```


Example Awin basket (Required)

``` javascript
<form name="aw_basket_form">
    <textarea id="aw_basket">
         AW:P|1001|test1234|123456|Test Product 1|3.99|1|sku2116|DEFAULT|DVD
         AW:P|1001|test1234|23456|Test Product 2|5.99|2|sku232|DEFAULT|Electronics
    </textarea>
</form>
```



## Checkout Page Configuration

Plugin requires `AWIN.Tracking.Sale` to be implemented on merchant's
site on checkout pages.

``` javascript
AWIN.Tracking.AdGenieV2 = AWIN.Tracking.AdGenieV2 || {};
AWIN.Tracking.AdGenieV2.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.AdGenieV2.merchantId = "MERCHANT_ID";
AWIN.Tracking.AdGenieV2.pagetype = "PAGE_TYPE";
```



## Product Page Configuration

``` javascript
AWIN.Tracking.AdGenieV2 = AWIN.Tracking.AdGenieV2 || {};
AWIN.Tracking.AdGenieV2.advertiserId = "ADVERTISER_ID";
AWIN.Tracking.AdGenieV2.merchantId = "MERCHANT_ID";
AWIN.Tracking.AdGenieV2.pagetype = "PAGE_TYPE";
AWIN.Tracking.AdGenieV2.identifier = "IDENTIFIER";
```



# Relevant Tickets

[PROD-3261](https://jira.awin.com/browse/PROD-3261?jql=text%20~%20%22AdGenie%22)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/awin-tracking/blob/2c7308fe070ea030ccff538fc5375b368a52c1bf/web/thirdparty/adGenieV2.js)