
# Description

SaleCycle use email to remarket to users who have abandoned an item in
their basket. Capturing users email addresses when using the site, they
then generate bespoke email creatives to try and increase conversion.
Usually work with Fashion or Travel sectors.

Payment Model: CPA

PS contact: Craig

Client contact: Darryn.hall@salecyle.com

# Integration requirements

- As a minimum the
  [Mastertag](http://wiki.affiliatewindow.com/index.php/Advertiser_Tracking_Guide/Standard_Implementation#Journey_Tag_.2F_Mastertag)
  must be displayed (or script appended) unconditionally on all
  applicable capture pages
- The
  [Mastertag](http://wiki.affiliatewindow.com/index.php/Advertiser_Tracking_Guide/Standard_Implementation#Journey_Tag_.2F_Mastertag)
  must also be present on the confirmation page.


**De-duping clients**

Modifications to the tracking set up is required to allow SaleCycle
visibility of all channels' conversions to close the loop. This can
easily be achieved by the client implementing \[and de-duplicating on
Affiliate Window's side\] via the [Channel
Parameter](http://wiki.affiliatewindow.com/index.php/Advertiser_Tracking_Guide/De-duplication#Channel_Parameter).
Consult a senior member of the team if unsure.

# Tag Plugin

|               |                      |
|---------------|----------------------|
| PluginType:   | SaleCycle            |
| Plugin Setup: | "See Code Below"     |
| Active:       | "Tick The Check Box" |

## Plugin setup code


``` javascript
AWIN.Tracking.SaleCycle = {};
AWIN.Tracking.SaleCycle.clientName = "CLIENTNAME";
AWIN.Tracking.SaleCycle.host = "d16fk4ms6rqz1v.cloudfront.net/capture/";
```



Replace \`CLIENTNAME\` with its real value supplied by !SaleCycle for
the advertiser campaign / program; this is mandatory or !SaleCycle's tag
will not load.

It is optional to declare \`AWIN.Tracking.SaleCycle.host\` however
according to the latest instructions from the vendor we should do it
like above. If a value is not declared then it defaults to
\`app.salecycle.com/capture/\`.

**<u>Inventory</u>**


``` mysql
SELECT
m.id AS 'advertiserId',
m.program_name AS 'programName',
IF(p.is_active = 1, 'Yes', 'No') AS 'enabled',
p.setup AS 'configuration'
FROM affiliatewindow.merchants m
JOIN affiliatewindow.merchant_tag_plugin p ON p.merchant_id = m.id AND p.is_active = 1
JOIN affiliatewindow.tag_plugin_type t ON t.id = p.tag_plugin_type_id
WHERE m.active IN (0, 1) AND
m.account_type != 18 AND
t.display_name = 'SaleCycle'
ORDER BY m.id ASC;
```



==Successful integration tracking calls (served via the Dwin tag) ==


``` html4strict
 <script type="text/javascript" id="_aw_script_N" src="http(s)://d16fk4ms6rqz1v.cloudfront.net/capture/CLIENTNAME.js"></script>
```


...where \`N\` is an incremental index for the number of scripts loaded.

## Ensure appropriate tracking links are used for example:

• Post Click link to merchant site:
<http://www.awin1.com/awclick.php?mid=MERCHANT_ID&id=AFFILIATE_ID>