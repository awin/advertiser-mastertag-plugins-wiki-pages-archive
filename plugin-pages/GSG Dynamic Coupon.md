# Supported Pages

- Generic Page
- Checkout Page
- Basket Page

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values.

## Generic & Basket Page Configuration

``` javascript
AWIN.Tracking.GSGDynamicCoupon = AWIN.Tracking.GSGDynamicCoupon || {};
AWIN.Tracking.GSGDynamicCoupon.id = "ID";
AWIN.Tracking.GSGDynamicCoupon.gTagConfig = {
                        u1: "mmm",
                        'send_to': 'DC-XXXXXX'
                    };
AWIN.Tracking.GSGDynamicCoupon.pagetype = "PAGE_TYPE";
```



## Checkout Page Configuration

Checkout page requires AWIN.Tracking.Sale object to be implemented on
merchant's website. Checkout page requires Awin basket to be implemented
on merchant's website.

``` javascript
AWIN.Tracking.GSGDynamicCoupon = AWIN.Tracking.GSGDynamicCoupon || {};
AWIN.Tracking.GSGDynamicCoupon.id = "ID";
AWIN.Tracking.GSGDynamicCoupon.gTagConfig = {
                        'u1': 'xxx',
                        'u2': 'xxx',
                        'u3': 'xxxx',
                        'send_to': 'DC-XXXXXX'
                    };
AWIN.Tracking.GSGDynamicCoupon.pagetype = "PAGE_TYPE";
```



# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/tree/master/src/plugins/thirdParty/gsgDynamicCoupon)