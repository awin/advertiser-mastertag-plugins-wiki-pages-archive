# Integration requirements

- Client must already have or implement Product Level Tracking to work
  with Criteo

<!-- -->

- Product IDs on the client site should match the Awin feed. As the
  retargeter will use the Awin feed as a pool of products, matching the
  id scraped from the product view tag to this.

<!-- -->

- The Dwin1 tag should be unconditionally displayed on all products
  pages.

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

Note: product scraper is needed for this plugin. It should be added on
**before** the Criteo plugin
Please see the following link for more information about the product
scraper:
[Product Scraper](Staff:Product_Scraper "wikilink")

## De-duping clients

Post click only - Modifications to the tracking will need to be made to
allow Criteo visibility on other channels conversions. This can either
be done by the client also implementing our tag in testmode, shown for
all other traffic or by the client using the AW channel functionality.
Consult a senior member of the team if unsure.

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | Criteo            |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |


== Plugin setup code == The code below goes into the plugin setup field
in the tag management form.
Replace \`PARTNER_ID\`, \`WIDGET_ID\`, \`SALE_WIDGET_ID\`,
\`MERCHANT_HOMEPAGE_URL\` and \`POOL_ID\` with real values. The
different tokens will be supplied by Criteo.

- AWIN.Tracking.Criteo.partnerId - criteo partner ID for this merchant
- AWIN.Tracking.Criteo.widgetId - Used on the home page and product page
- AWIN.Tracking.Criteo.saleWidgetId - Used on the sale confirmation page
- AWIN.Tracking.Criteo.poolId - Used on every page




``` javascript
AWIN.Tracking.Criteo = {};
AWIN.Tracking.Criteo.partnerId = "PARTNER_ID";
AWIN.Tracking.Criteo.widgetId = "WIDGET_ID";
AWIN.Tracking.Criteo.saleWidgetId = "SALE_WIDGET_ID";
AWIN.Tracking.Criteo.poolId = "POOL_ID";
```



== Setting a Different Widget Server == Criteo may have a different
widget server for some of their merchants on a product page. For example
Best Buy have their own widget server but use the same secure widget
server. In this case you would have to set
AWIN.Tracking.Criteo.httpWidgetUrl


``` javascript
AWIN.Tracking.Criteo = {};
AWIN.Tracking.Criteo.partnerId = "PARTNER_ID";
AWIN.Tracking.Criteo.widgetId = "WIDGET_ID";
AWIN.Tracking.Criteo.saleWidgetId = "SALE_WIDGET_ID";
AWIN.Tracking.Criteo.poolId = "POOL_ID";

AWIN.Tracking.Criteo.httpWidgetUrl = "http://bestbuyuk.widget.criteo.com";
```



If a merchant happens to use a different secure widget server as well
then you can also set AWIN.Tracking.Criteo.httpsWidgetUrl


``` javascript
AWIN.Tracking.Criteo = {};
AWIN.Tracking.Criteo.partnerId = "PARTNER_ID";
AWIN.Tracking.Criteo.widgetId = "WIDGET_ID";
AWIN.Tracking.Criteo.saleWidgetId = "SALE_WIDGET_ID";
AWIN.Tracking.Criteo.poolId = "POOL_ID";

AWIN.Tracking.Criteo.httpWidgetUrl = "http://merchant-normal.widget.criteo.com";
AWIN.Tracking.Criteo.httpsWidgetUrl = "https://merchant-secure.widget.criteo.com";
```




## Successful integration tracking calls (served via the Dwin tag)


Product page:


``` javascript
<div id="pcto_dis_div" style="display: none; "> <iframe width="1px" height="1px" style=""
src=" http://dis.criteo.com/dis/dis.aspx?c=2&p=2305&cb=74130876408"></iframe></div>
```



Conversion pixel:
==Ensure appropriate tracking links are used for <example:==>

- Post View (Post Impression) Cookie Link :
  <http://awin1.com/appshow.php?a=AFFILIATE_ID&m=MERCHANT_ID>

<!-- -->

- Post Click link to merchant site:
  <http://www.awin1.com/awclick.php?mid=MERCHANT_ID&id=AFFILIATE_ID>