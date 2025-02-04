# Description

Merchenta are a CPA retargeter who are also able to offer FB dynamic
uplift through the network. They can provide in depth real time
reporting for advertisers in order to optimise campaigns. They are able
to work across all verticals but do particularly well where there is the
potential to increase AOV, x-sell and up-sell. They require product
level tracking in order to integrate with a merchant.

Payment Model: Post View CPA

PS contact: Vicky

Client contact: neil.mcclements@merchenta.com

# Integration requirements

- The Dwin1 tag should be unconditionally displayed on all products
  pages.

<!-- -->

- The Dwin1 tag needs to be displayed on the confirmation page as part
  of the Awin conversion tracking.

<!-- -->

- Product IDs on the client site should match the Awin feed. As the
  retargeter will use the Awin feed as a pool of products, matching the
  id scraped from the product view tag to this.

<!-- -->

- Ensure post view transactions are enabled for the account in the
  provider area and cookie duration is correct

<!-- -->

- If an adblocker solution is enabled - 'Click redirect to custom
  domain' **must** be enabled to ensure pv cookies are dropped on the
  alternate domain.

**Note:** You MUST have the [Product
Scraper](Staff:Product_Scraper "wikilink") tag already set up before
adding this tag.

**De-duping clients**

Post click only - Modifications to the tracking will need to be made to
allow Merchenta visibility on other channels conversions. This can
either be done by the client also implementing our tag in testmode,
shown for all other traffic or by the client using the AW channel
functionality. Consult a senior member of the team if unsure.

Post view- The client will need to implement a secondary tracking tag
with the pv modifications according to the de-duping rules set out in
the IO.

Conditional Tracking information here: [MyThings Merchant Tracking
Guide](Staff:MyThings_Merchant_Tracking_Guide "wikilink")


= Tag Plugin =

|               |                      |
|---------------|----------------------|
| PluginType:   | Merchenta            |
| Plugin Setup: | "See Code Below"     |
| Active:       | "Tick The Check Box" |


== Plugin setup code == The code below goes into the plugin setup field
in the tag management form. Replace RETAILERCODE with real values.


``` javascript
AWIN.Tracking.Merchenta = {};
AWIN.Tracking.Merchenta.retailerCode = "RETAILERCODE";
```



== Successful integration tracking calls (served via the Dwin tag) ==
Product page script append:


``` javascript
<script type="text/javascript" id="_aw_script_0" src="http://cdn.merchenta.com/track/t.js"></script>
```



== Ensure appropriate tracking links are used for example: ==

- Post View (Post Impression) Cookie Link :
  <http://awin1.com/appshow.php?a=AFFILIATE_ID&m=MERCHANT_ID>

<!-- -->

- Post Click link to merchant site:
  <http://www.awin1.com/awclick.php?mid=MERCHANT_ID&id=AFFILIATE_ID>