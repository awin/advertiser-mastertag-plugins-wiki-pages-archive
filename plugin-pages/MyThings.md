
# Description

European based retargeting company. They offer fully customised
retargeting campaigns across all sectors and are able to work on
multiple pricing models including CPA, CPC, CPM, and Cost+. myThings are
also regarded as one of, if not the top Real-time bid (RTB) buyers and
are therefore able to offer premium placements to their clients.

Payment Model: Post View CPA (Can also run CPC campaigns)

PS Contact- Angelo

Client Contact- Dan Holmes danh@mythings.com

# Integration requirements

- The client should have Product Level Tracking implemented to work with
  !MyThings, however it is \[actually\] not mandatory

<!-- -->

- The Dwin1 tag should be unconditionally displayed on all category and
  products pages.

<!-- -->

- The Dwin1 tag needs to be displayed on the confirmation page as part
  of the Awin conversion tracking.

<!-- -->

- Ensure post view transactions are enabled for the account in the
  provider area and cookie duration is correct

<!-- -->

- If an adblocker solution is enabled - 'Click redirect to custom
  domain' **must** be enabled to ensure pv cookies are dropped on the
  alternate domain.

**Note:** The product scraper is <u>**not**</u> needed for this plugin

**De-duping clients**

**Post click only** - Modifications to the tracking will need to be made
to allow MyThings visibility on other channels conversions. This can
either be done by the client also implementing our tag in testmode,
shown for all other traffic or by the client using the AW channel
functionality. Consult a senior member of the team if unsure.

**Post view** - The client will need to implement a secondary tracking
tag with the pv modifications according to the de-duping rules set out
in the IO.

Conditional Tracking information here:[MyThings Merchant Tracking
Guide](Staff:MyThings_Merchant_Tracking_Guide "wikilink")

# Tag Plugin

|               |                      |
|---------------|----------------------|
| PluginType:   | MyThings             |
| Plugin Setup: | "See Code Below"     |
| Active:       | "Tick The Check Box" |


== Plugin setup code == The code below goes into the plugin setup field
in the tag management form. Replace \`MID\` with the real AWIN merchant
ID in the \`AWIN.Tracking.MyThings.advertiserToken\` value below. For
example, for merchant 1001 the token will be \`awin-1001-100-uk\`


``` javascript
AWIN.Tracking.MyThings = {};
AWIN.Tracking.MyThings.advertiserToken = "awin-MID-100-uk";
```



For US merchants also add this to the plugin setup code:


``` javascript
AWIN.Tracking.MyThings.url = "rainbow-us.mythings.com";
```




## Example of setting MyThings tracking to not fire on defined pages

Made for Vodafone but may be used for any other merchant.

Here we determine whether we should run the code by
\`tagmanParam.customerType\` global variable and setting
\`AWIN.Tracking.MyThings.norun\` to true.

Full setup code for Vodafone for this case is


``` javascript
AWIN.Tracking.MyThings = {};
AWIN.Tracking.MyThings.advertiserToken = "awin-1257-100-uk";

if ( typeof(tagmanParam) !== "undefined" &&
     typeof(tagmanParam.customerType) !== "undefined"
   )
{
    if ( tagmanParam.customerType == 'Business' ) {
        AWIN.Tracking.MyThings.norun = true;
    }
}
```



== Successful integration tracking calls (served via the Dwin tag) ==
**Product page script append:**

Our code uses the token value applied via the plugin to build the final
script append for MyThings.


``` javascript
<script id="_aw_script_1" type="text/javascript" src="http://rainbowx.mythings.com/c.aspx?atok=awin-1001-100-uk">
```



**Request made in headers:**

<https://rainbowx.mythings.com/c.aspx?atok=awin-1001-100-uk>

**Conversion pixel:**

A MyThings tracking (action 9902) request is built on conversion using
the values from the js of:


``` javascript
AWIN.Tracking.Sale.orderRef
AWIN.Tracking.Sale.amount
AWIN.Tracking.Sale.currency
```



Example:
<https://rainbowx.mythings.com/pix.aspx?atok=awin-2186-100-uk&eventtype=4&aid=9902&trx=2332915&tam=28.30&cur=GBP&.Referrer=https://stagingadmin.thorntons.co.uk/checkout/basket.jsp&mode=html&ver=2.5&ref=https://stagingadmin.thorntons.co.uk/checkout/basket.jsp&r=0.5312457358696273>

## Ensure appropriate tracking links are used for example:

- Post View (Post Impression) Cookie Link :
  <http://awin1.com/appshow.php?a=AFFILIATE_ID&m=MERCHANT_ID>

<!-- -->

- Post Click link to merchant site:
  <http://www.awin1.com/awclick.php?mid=MERCHANT_ID&id=AFFILIATE_ID>