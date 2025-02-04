# Requirements

- Mastartag must be displayed across all pages in the shop
- javascript based tracking code must be loaded unconditionally on the
  order confirmation page.


==Consent== This plugins supports **TCF2.0 framework** and if compliant
CMP (Consent Management Platform) is implemented in the advertiser shop,
&gdpr and gdpr_consent parameters will be automatically included in
request URL of plugin provider.
**Example:**
&gdpr=1&gdpr_consent=CPMGfKhPMGfKhAGABCENBqCgAAAAAEKAAB5YAAAJWgBADNASsAAA.YAAAAAAAAAAA

==Manual consent configuration== If the advertiser is using **non-TCF2.0
compliant** consent tool / platform, consent information must be
configured manually by setting up condition in the configuration:

``` javascript
AWIN.Tracking.ADCMedia = AWIN.Tracking.ADCMedia || {};
    if (condition: consent given to ADC Media / Doubleclick) {
        AWIN.Tracking.ADCMedia.gdpr = 1;
    } else {
        AWIN.Tracking.ADCMedia.gdpr = 0;
    }
```


Please bear in mind, the consent requirements for this provider are
still being investigated and could change.
=Supported Pages=

- generic, product, basket, checkout

# Configuration

Replace `"VALUE_PLACEHOLDERS"` with real values. Checkout success page
will be automatically detected, when AWIN.Tracking.Sale object is
available.

## Configuration Example

Configurable tokens per PageType (supplied by ADC Media):

- activity1Id
- activity2Id
- activity3Id
- activity4Id
- GMP ID

``` javascript
AWIN.Tracking.ADCMedia = AWIN.Tracking.ADCMedia || {};
AWIN.Tracking.ADCMedia.gmpId = "GMP ID"; // value supplied by ADC Media

AWIN.Tracking.ADCMedia.activity4Id = "REPLACE_with_activity4Id"; // token for checkout success page
AWIN.Tracking.ADCMedia.activity3Id = "REPLACE_with_activity3Id"; // token for basket page
AWIN.Tracking.ADCMedia.activity2Id = "REPLACE_with_activity2Id"; // token for product page
AWIN.Tracking.ADCMedia.activity1Id = "REPLACE_with_activity1Id"; // token for generic page

AWIN.Tracking.ADCMedia.vendorId = 755; // required and static value, since ADC Media is using Doubleclick/Google Technology

if (document.location.href.match(/cart/)) {
    AWIN.Tracking.ADCMedia.pageType = "basket";
} else if (document.location.href.match(/product/)) {
    AWIN.Tracking.ADCMedia.pageType = "product";
} else if (document.location.href.match(/whatSoEver/)) {
        AWIN.Tracking.ADCMedia.pageType = "generic";
}
```



# Relevant Tickets

[PROD-9676](https://jira.awin.com/browse/PROD-9676)
[PROD-9879](https://jira.awin.com/browse/PROD-9879)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/adcMedia/plugin.js)