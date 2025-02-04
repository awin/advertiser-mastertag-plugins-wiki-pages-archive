
# Description

AdGENIE focuses on ad space retargeting. AdGENIE’s software allows them
to target customers via on-site advertisements with a specific
retailer’s products that the customer has shown some previous interest
in. The served advertisements can be designed in-house by AdGENIE or
created by the retailer themselves. AdGENIE also practice prospecting,
which allows AdGENIE to target customers who have searched for a
specific product via a search engine, rather than just visiting the
retailer’s website directly.

As a requirement for working with AdGENIE, the retailer’s website must
already receive 100,000 unique visitors per month. AdGENIE do not have a
specific sector in which they work with, however the majority of their
clients are retail-based.

Payment Model: Post View CPA (Can also run CPC campaigns)

PS contact: Alex

Client contact: - mconnolly@adgenie.co.uk

# Integration Requirements

- The Dwin1 tag should be unconditionally displayed on all category and
  products pages.

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
  domain' must be enabled to ensure pv cookies are dropped on the
  alternate domain.


Note: The product scraper is needed for this plugin, it should be added
on **before** the AdGenie plugin **De-duping clients**.
Please see the following link for more information about the product
scraper:
[Product Scraper](Staff:Product_Scraper "wikilink")


Post click only - Modifications to the tracking will need to be made to
allow adGenie visibility on other channels conversions. This can either
be done by the client also implementing our tag in testmode, shown for
all other traffic or by the client using the AW channel functionality.
Consult a senior member of the team if unsure.

Post view- The client will need to implement a secondary tracking tag
with the pv modifications.

Conditional Tracking information here: [MyThings Merchant Tracking
Guide](Staff:MyThings_Merchant_Tracking_Guide "wikilink")


=Tag Plugin=
{\| border = '1'

\| PluginType:

\| AdGenie

\|-

\| Plugin Setup:

\|"See Code Below"

\|-

\| Active:

\| "Tick The Check Box"

\|}


=Plugin setup code= The code below goes into the plugin setup field in
the tag management form. Replace ADGENIE_COMPANY_ID and APPNEXUS_ID with
real values. The token will be supplied by AdGenie.


``` javascript
AWIN.Tracking.AdGenie = {};
AWIN.Tracking.AdGenie.companyId = "ADGENIE_COMPANY_ID";
AWIN.Tracking.AdGenie.addId = "APPNEXUS_ID";
```



**Example:**


``` javascript
AWIN.Tracking.AdGenie = {};
AWIN.Tracking.AdGenie.companyId = "dpbgpyHwBjfuGrsykwAy";
AWIN.Tracking.AdGenie.addId = "1784387";
```



=Successful integration tracking calls (served via the Dwin tag)=
Product page:


``` javascript
<img src="https://adverts.adgenie.co.uk/genieTracker.php?adgCompanyID=wgFGaaEGuzyxtcCmcopd&adgItem=PRODUCT_ID" alt="" width="1"/>
<img src=" http://ib.adnxs.com/seg?add=95298&t=2" width="1" height="1"/>
```



Conversion pixel:

=Ensure appropriate tracking links are used for <example:=>

- Post View (Post Impression) Cookie Link :
  <http://awin1.com/appshow.php?a=AFFILIATE_ID&m=MERCHANT_ID>
- Post Click link to merchant site:
  <http://www.awin1.com/awclick.php?mid=MERCHANT_ID&id=AFFILIATE_ID>