
# Description

Payment Model: Post View CPA

PS contact: Vicky

Client contact: olumide.gomes@mail.rakuten.com

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


**Note:** The client <u>**does not**</u> need to implement Product Level
Tracking to work with mediaFORGE

**Note:** You MUST have the [Product
Scraper](Staff:Product_Scraper "wikilink") tag already set up before
adding this tag.

**De-duping clients**

Post click only - Modifications to the tracking will need to be made to
allow MediaForge visibility on other channels conversions. This can
either be done by the client also implementing our tag in testmode,
shown for all other traffic or by the client using the AW channel
functionality. Consult a senior member of the team if unsure.

Post view- The client will need to implement a secondary tracking tag
with the pv modifications according to the de-duping rules set out in
the IO.

Conditional Tracking information here: [MyThings Merchant Tracking
Guide](Staff:MyThings_Merchant_Tracking_Guide "wikilink")


== Tag Plugin ==

|              |                   |
|--------------|-------------------|
| PluginType:  | mediaFORGE        |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

## Plugin setup code

The code below goes into the plugin setup field in the tag management
form. Replace \`THE_ADVERTISER_SPECIFIC_ID\` with its real value
supplied by **mediaFORGE** for the merchant.


``` javascript
AWIN.Tracking.MediaForge = {};
AWIN.Tracking.MediaForge.id = "THE_ADVERTISER_SPECIFIC_ID";
```




## Ensure appropriate tracking links are used for example:

- Post View (Post Impression) Cookie Link :
  <http://awin1.com/appshow.php?a=AFFILIATE_ID&m=MERCHANT_ID>

<!-- -->

- Post Click link to merchant site:
  <http://www.awin1.com/awclick.php?mid=MERCHANT_ID&id=AFFILIATE_ID>