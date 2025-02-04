# Zanox Tracking Plugin

## Background Information

The main purpose of the Zanox plugin is to allow Affiliate Window
advertisers to seamlessly expand their affiliate marketing campaign into
Zanox regions without having to integrate additional tracking. It is
also a strong selling point for when it comes to pitching for global
brands as by utilising it, the client it in reality only will require
one integration.

## Integration Requirements



- The
  **[Mastertag](Advertiser_Tracking_Guide/Standard_Implementation#Journey_Tag_.2F_Mastertag "wikilink")**
  must be unconditionally appended to all pages to allow the plugin to
  fetch the Zanox partner ID (click checksum) and store it in a session,
  or alternatively persistent, cookie - this is not mandatory, however
  highly recommended!
- For advertisers displaying tracking unconditionally, then the minimal
  requirement is the
  **[Mastertag](Advertiser_Tracking_Guide/Standard_Implementation#Journey_Tag_.2F_Mastertag "wikilink")**
  and the **[Conversion
  Tag](Advertiser_Tracking_Guide/Standard_Implementation#Conversion_Tag "wikilink")**
  present on the confirmation page(s)
- De-duplicating advertisers must unconditionally append both the the
  **[Mastertag](Advertiser_Tracking_Guide/Standard_Implementation#Journey_Tag_.2F_Mastertag "wikilink")**
  and the **[Conversion
  Tag](Advertiser_Tracking_Guide/Standard_Implementation#Conversion_Tag "wikilink")**
  to the confirmation page(s) and furthermore instruct the plugin
  whether or not to display Zanox tracking by what is being declared to
  the **[Channel
  Parameter](Advertiser_Tracking_Guide/De-duplication#Channel_Parameter "wikilink")**

## Mandatory Settings


**Template**


``` text
AWIN.Tracking.Zanox = AWIN.Tracking.Zanox || {};
AWIN.Tracking.Zanox.programId = "{{programId}}";
AWIN.Tracking.Zanox.programChecksum = "{{programChecksum}}";
```


- Replace `{{programId}}` with the Zanox merchant program ID
- Replace `{{programChecksum}}` with the Zanox merchant program checksum

**Example**


``` javascript
AWIN.Tracking.Zanox = AWIN.Tracking.Zanox || {};
AWIN.Tracking.Zanox.programId = "11191";
AWIN.Tracking.Zanox.programChecksum = "C1878128339";
```


### Multiple Zanox Programs

If the advertiser wants to expand into more than one territory and each
localised site has its own confirmation page, then the approach below
could be utilised.

**Example**


``` javascript
AWIN.Tracking.Zanox = AWIN.Tracking.Zanox || {};
if (window.location.host.indexOf("de.advertiser-domain.com") != -1) {
    AWIN.Tracking.Zanox.programId = "11191";
    AWIN.Tracking.Zanox.programChecksum = "C1878128339";
} else if (window.location.host.indexOf("dk.advertiser-domain.com") != -1 || window.location.host.indexOf("no.advertiser-domain.com") != -1 || window.location.host.indexOf("se.advertiser-domain.com") != -1) {
    AWIN.Tracking.Zanox.programId = "11536";
    AWIN.Tracking.Zanox.programChecksum = "C7468124330";
}
```


However if the confirmation page is shared, then you will have to scrape
the URL or page for some other identifier to determine which program ID
and program checksum to declare.

## Optional Settings

### Conditional Tracking

Utilise the setting `AWIN.Tracking.Zanox.applicableChannels`, which can
be declared as a string or an array, to instruct the plugin what channel
or channels, as populated by the advertiser to the **[Channel
Parameter](Advertiser_Tracking_Guide/De-duplication#Channel_Parameter "wikilink")**
(`AWIN.Tracking.Sale.channel`), to display Zanox tracking for.

**Template**


``` text
AWIN.Tracking.Zanox.applicableChannels = "{{channelName}}";
```


- Replace `{{channelName}}` with the name of the channel for which the
  plugin should display Zanox tracking for

**Example**


``` javascript
AWIN.Tracking.Zanox = AWIN.Tracking.Zanox || {};
AWIN.Tracking.Zanox.programId = "11191";
AWIN.Tracking.Zanox.programChecksum = "C1878128339";
AWIN.Tracking.Zanox.applicableChannels = ["na", "zx"];
```


### Custom Partner ID Parameter

If the Zanox merchant program is utilising a custom parameter name for
populating the click checksum (or partner ID according to their
terminology), then configure the setting
`AWIN.Tracking.Zanox.zanpidParameterName` to instruct the plugin where
to pick it up from.

**Template**


``` text
AWIN.Tracking.Zanox.zanpidParameterName = "{{parameterName}}";
```


- Replace `{{parameterName}}` with the name for the parameter where the
  click ID will be populated to

**Example**


``` javascript
AWIN.Tracking.Zanox = AWIN.Tracking.Zanox || {};
AWIN.Tracking.Zanox.programId = "11191";
AWIN.Tracking.Zanox.programChecksum = "C1878128339";
AWIN.Tracking.Zanox.zanpidParameterName = "cid";
```


### Partner ID Cookie Handling

While Affiliate Window stores the captured click checksum (`awc`) in a
persistent cookie, Zanox recommends that their partner ID only is stored
within the active session. You can however instruct the plugin to
replicate the Affiliate Window behaviour by setting the parameter
`AWIN.Tracking.Zanox.persistentPartnerId`.

**Example**


``` javascript
AWIN.Tracking.Zanox = AWIN.Tracking.Zanox || {};
AWIN.Tracking.Zanox.programId = "11191";
AWIN.Tracking.Zanox.programChecksum = "C1878128339";
AWIN.Tracking.Zanox.persistentPartnerId = true;
```


### Force Customer ID

Utilise the setting `AWIN.Tracking.Zanox.customerId` to force the plugin
to always use a specific value for customer ID when triggering the Zanox
tracking requests.

**Template**


``` text
AWIN.Tracking.Zanox.customerId = "{{customerId}}";
```


- Replace `{{customerId}}` with the customer ID

**Example**


``` javascript
AWIN.Tracking.Zanox = AWIN.Tracking.Zanox || {};
AWIN.Tracking.Zanox.programId = "11191";
AWIN.Tracking.Zanox.programChecksum = "C1878128339";
AWIN.Tracking.Zanox.customerId = "N/A";
```


### Force Currency Code

Utilise the setting `AWIN.Tracking.Zanox.currency` to force the plugin
to always use a specific currency code.

**Template**


``` text
AWIN.Tracking.Zanox.currency = "{{currencyCode}}";
```


- Replace `{{currencyCode}}` with the currency code

**Example**


``` javascript
AWIN.Tracking.Zanox = AWIN.Tracking.Zanox || {};
AWIN.Tracking.Zanox.programId = "11191";
AWIN.Tracking.Zanox.programChecksum = "C1878128339";
AWIN.Tracking.Zanox.currency = "EUR";
```


### Force Commission Group Code

Utilise the setting `AWIN.Tracking.Zanox.commissionGroup` to force the
plugin to always use a specific code as the commission group.

**Template**


``` text
AWIN.Tracking.Zanox.commissionGroup = "{{commissionGroupCode}}";
```


- Replace `{{commissionGroupCode}}` with the commission group code (or
  CID using Zanox terminology) you want to utilise for calculating
  commission

**Example**


``` javascript
AWIN.Tracking.Zanox = AWIN.Tracking.Zanox || {};
AWIN.Tracking.Zanox.programId = "11191";
AWIN.Tracking.Zanox.programChecksum = "C1878128339";
AWIN.Tracking.Zanox.commissionGroup = "";
```


### Basket Tracking

The default tracking behaviour is that each individual commission group
code and amount pair will create its own request, however it's possible
to instead utilise basket tracking by setting the parameter
`AWIN.Tracking.Zanox.basketTracking`. Please note that this also will
create a basket tracking request even if `AWIN.Tracking.Sale.parts`
contains one commission group code and amount pair. It is also worth
keeping in mind that forcing a CID utilising
`AWIN.Tracking.Zanox.commissionGroup` will disable basket tracking.

**Example**


``` javascript
AWIN.Tracking.Zanox = AWIN.Tracking.Zanox || {};
AWIN.Tracking.Zanox.programId = "11191";
AWIN.Tracking.Zanox.programChecksum = "C1878128339";
AWIN.Tracking.Zanox.basketTracking = true;
```


### Delimiting Character

`AWIN.Tracking.Zanox.customDelimiter` can be used to set a custom
delimiting character for separating multiple **[Custom Tracking
Parameters](Advertiser_Tracking_Guide/Custom_Tracking_Parameters "wikilink")**
stored to `ReviewNote`. If this has not been declared, then a pipe
character ("`|`") will be used as delimiter.

**Template**


``` text
AWIN.Tracking.Zanox.customDelimiter = "{{delimiter}}";
```


- Replace `{{delimiter}}` with the character you want to use

**Example**


``` javascript
AWIN.Tracking.Zanox = AWIN.Tracking.Zanox || {};
AWIN.Tracking.Zanox.programId = "11191";
AWIN.Tracking.Zanox.programChecksum = "C1878128339";
AWIN.Tracking.Zanox.customDelimiter = ";";
```


# References

## Tracking Conversion Table



<table cellpadding="3" cellspacing="2" border="1">

<tr>

<td>

**Information**

</td>

<td>

**Affiliate Window**

</td>

<td>

**Zanox**

</td>

<td>

**Comments**

</td>

</tr>

<tr>

<td>

Total net order amount

</td>

<td>

`AWIN.Tracking.Sale.amount`

</td>

<td>

`TotalPrice`

</td>

<td>

If basket tracking has not been enabled and `AWIN.Tracking.Sale.parts`
contains more than one commission group code and amount pair, then the
plugin will construct and append one tracking request for each pair with
the associated parts amount populated to `TotalPrice`

</td>

</tr>

<tr>

<td>

**[Channel
Parameter](Advertiser_Tracking_Guide/De-duplication#Channel_Parameter "wikilink")**

</td>

<td>

`AWIN.Tracking.Sale.channel`

</td>

<td>

N/A

</td>

<td>

Possible to configure what channel or channels to display Zanox tracking
for by utilising the setting `AWIN.Tracking.Zanox.applicableChannels`

</td>

</tr>

<tr>

<td>

Currency code

</td>

<td>

`AWIN.Tracking.Sale.currency`

</td>

<td>

`CurrencySymbol`

</td>

<td>

Possible to force a value to this parameter by utilising
`AWIN.Tracking.Zanox.currency`

</td>

</tr>

<tr>

<td>

**[Custom Tracking
Parameters](Advertiser_Tracking_Guide/Custom_Tracking_Parameters "wikilink")**

</td>

<td>

`AWIN.Tracking.Sale.custom`

</td>

<td>

`ReviewNote`

</td>

<td>

Note that discount/voucher code information will be populated first.
Delimiting character is pipe ("`|`") by default, but can be customised
by declaring `AWIN.Tracking.Zanox.customDelimiter`

</td>

</tr>

<tr>

<td>

Merchant customer ID

</td>

<td>

`AWIN.Tracking.Sale.customer`

</td>

<td>

`CustomerID`

</td>

<td>

The **[Conversion
Tag](Advertiser_Tracking_Guide/Standard_Implementation#Conversion_Tag "wikilink")**
does currently not support recording the merchant customer ID, however
the plugin will pass on this information to Zanox. It is also possible
to force a value to this parameter by utilising
`AWIN.Tracking.Zanox.customerId`

</td>

</tr>

<tr>

<td>

Order reference

</td>

<td>

`AWIN.Tracking.Sale.orderRef`

</td>

<td>

`OrderID`

</td>

<td>

</td>

</tr>

<tr>

<td>

Commission allocation breakdown

</td>

<td>

`AWIN.Tracking.Sale.parts`

</td>

<td>

`CID`

</td>

<td>

Note that Affiliate Window's `DEFAULT` commission group automatically
and case insensitively is converted into Zanox's "" (no name). Use
`AWIN.Tracking.Zanox.commissionGroup` if you want to override the
automatic allocation and force a specific CID. Set
`AWIN.Tracking.Zanox.basketTracking` if you want to utilise basket
tracking (`CID=[[basket|basket]]` and the `XML` parameter)

</td>

</tr>

<tr>

<td>

Discount/voucher code

</td>

<td>

`AWIN.Tracking.Sale.voucher`

</td>

<td>

`ReviewNote`

</td>

<td>

</td>

</tr>

<tr>

<td>

Click checksum / Partner ID

</td>

<td>

`awc` (default parameter name)
`_aw_m_{{merchantId}}` (cookie)
`cks` (request)

</td>

<td>

`zanpid` (default parameter name)
`_zx_m_{{programId}}` (cookie)
`PartnerID` (request)

</td>

<td>

If the partner ID is being populated to a custom URL request string
parameter, then declare the name to
`AWIN.Tracking.Zanox.zanpidParameterName`. Set
`AWIN.Tracking.Zanox.persistentPartnerId` to utilise a persistent cookie
instead of a session based one

</td>

</tr>

</table>

## Tracking Requests

### CID Tracking


**Plugin Setup**


``` javascript
AWIN.Tracking.Zanox = AWIN.Tracking.Zanox || {};
AWIN.Tracking.Zanox.programId = "11191";
AWIN.Tracking.Zanox.programChecksum = "C1878128339";
AWIN.Tracking.Zanox.applicableChannels = "zx";
```


**Conversion Tag**


``` javascript
var AWIN = {};
AWIN.Tracking = {};
AWIN.Tracking.Sale.amount = "9.00";
AWIN.Tracking.Sale.channel = "zx";
AWIN.Tracking.Sale.currency = "EUR";
AWIN.Tracking.Sale.custom = ["foo", "bar"];
AWIN.Tracking.Sale.customer = "15376";
AWIN.Tracking.Sale.orderRef = "AA000001";
AWIN.Tracking.Sale.parts = "Default:4.50|Sale:4.50";
AWIN.Tracking.Sale.test = "0";
AWIN.Tracking.Sale.voucher = "10PERCENTOFF2015";
```


**Requests**


``` text
https://www.zenaps.com/sread.js?a=1001&b=9.00&cr=EUR&c=AA000001&d=DEFAULT:4.50|SALE:4.50&vc=10PERCENTOFF2015&t=0&ch=zx&cks=&l=https%3A//www.advertiser-domain.com/confirmation&tv=2&tt=js&p1=foo&p2=bar
https://www.zenaps.com/sread.php?a=1001&b=9.00&cr=EUR&c=AA000001&d=DEFAULT:4.50|SALE:4.50&vc=10PERCENTOFF2015&t=0&ch=zx&cks=&l=https%3A//www.advertiser-domain.com/confirmation&tv=2&tt=ia&p1=foo&p2=bar
https://ad.zanox.com/pps/?11191C1878128339&mode=%5B%5B1%5D%5D&PartnerID=%5B%5B29522697C1532062743%5D%5D&OrderId=%5B%5BAA000001%5D%5D&TotalPrice=%5B%5B4.50%5D%5D&CurrencySymbol=%5B%5BEUR%5D%5D&CID=%5B%5B%5D%5D&CustomerID=%5B%5B15376%5D%5D&ReviewNote=%5B%5B10PERCENTOFF2015%7Cfoo%7Cbar%5D%5D
https://ad.zanox.com/pps/?11191C1878128339&mode=%5B%5B1%5D%5D&PartnerID=%5B%5B29522697C1532062743%5D%5D&OrderId=%5B%5BAA000001%5D%5D&TotalPrice=%5B%5B4.50%5D%5D&CurrencySymbol=%5B%5BEUR%5D%5D&CID=%5B%5BSale%5D%5D&CustomerID=%5B%5B15376%5D%5D&ReviewNote=%5B%5B10PERCENTOFF2015%7Cfoo%7Cbar%5D%5D
https://ad.zanox.com/ppv/images/onepixel.gif
https://ad.zanox.com/ppv/images/onepixel.gif
```


**Decoded Requests**


``` text
https://www.zenaps.com/sread.js?a=1001&b=9.00&cr=EUR&c=AA000001&d=DEFAULT:4.50|SALE:4.50&vc=10PERCENTOFF2015&t=0&ch=zx&cks=&l=https://www.advertiser-domain.com/confirmation&tv=2&tt=js&p1=foo&p2=bar
https://www.zenaps.com/sread.php?a=1001&b=9.00&cr=EUR&c=AA000001&d=DEFAULT:4.50|SALE:4.50&vc=10PERCENTOFF2015&t=0&ch=zx&cks=&l=https://www.advertiser-domain.com/confirmation&tv=2&tt=ia&p1=foo&p2=bar
https://ad.zanox.com/pps/?11191C1878128339&mode=[[1|1]]&PartnerID=[[29522697C1532062743|29522697C1532062743]]&OrderId=[[AA000001|AA000001]]&TotalPrice=[[4.50|4.50]]&CurrencySymbol=[[EUR|EUR]]&CID=[[]]&CustomerID=[[15376|]]&CustomerID=[[15376]]&ReviewNote=[[10PERCENTOFF2015|foo]]
https://ad.zanox.com/pps/?11191C1878128339&mode=[[1|1]]&PartnerID=[[29522697C1532062743|29522697C1532062743]]&OrderId=[[AA000001|AA000001]]&TotalPrice=[[4.50|4.50]]&CurrencySymbol=[[EUR|EUR]]&CID=[[Sale|Sale]]&CustomerID=[[15376|15376]]&ReviewNote=[[10PERCENTOFF2015|foo]]
https://ad.zanox.com/ppv/images/onepixel.gif
https://ad.zanox.com/ppv/images/onepixel.gif
```


### Basket Tracking


**Plugin Setup**


``` javascript
AWIN.Tracking.Zanox = AWIN.Tracking.Zanox || {};
AWIN.Tracking.Zanox.programId = "11191";
AWIN.Tracking.Zanox.programChecksum = "C1878128339";
AWIN.Tracking.Zanox.applicableChannels = "zx";
AWIN.Tracking.Zanox.basketTracking = true;
```


**Conversion Tag**


``` javascript
var AWIN = {};
AWIN.Tracking = {};
AWIN.Tracking.Sale.amount = "9.00";
AWIN.Tracking.Sale.channel = "zx";
AWIN.Tracking.Sale.currency = "EUR";
AWIN.Tracking.Sale.custom = ["foo", "bar"];
AWIN.Tracking.Sale.customer = "15376";
AWIN.Tracking.Sale.orderRef = "AA000001";
AWIN.Tracking.Sale.parts = "Default:4.50|Sale:4.50";
AWIN.Tracking.Sale.test = "0";
AWIN.Tracking.Sale.voucher = "10PERCENTOFF2015";
```


**Requests**


``` text
https://www.zenaps.com/sread.js?a=1001&b=9.00&cr=EUR&c=AA000001&d=DEFAULT:4.50|SALE:4.50&vc=10PERCENTOFF2015&t=0&ch=zx&cks=&l=https%3A//www.advertiser-domain.com/confirmation&tv=2&tt=js&p1=foo&p2=bar
https://www.zenaps.com/sread.php?a=1001&b=9.00&cr=EUR&c=AA000001&d=DEFAULT:4.50|SALE:4.50&vc=10PERCENTOFF2015&t=0&ch=zx&cks=&l=https%3A//www.advertiser-domain.com/confirmation&tv=2&tt=ia&p1=foo&p2=bar
https://ad.zanox.com/pps/?11191C1878128339&mode=%5B%5B1%5D%5D&PartnerID=%5B%5B29522697C1532062743%5D%5D&OrderId=%5B%5BAA000001%5D%5D&TotalPrice=%5B%5B9.00%5D%5D&CurrencySymbol=%5B%5BEUR%5D%5D&CID=%5B%5Bbasket%5D%5D&XML=%5B%5B%3Cz%3E%3Co%3E%3Cso%20up%3D%224.50%22%20cid%3D%22%22%20%2F%3E%3Cso%20up%3D%224.50%22%20cid%3D%22Sale%22%20%2F%3E%3C%2Fo%3E%3C%2Fz%3E%5D%5D&CustomerID=%5B%5B15376%5D%5D&ReviewNote=%5B%5B10PERCENTOFF2015%7Cfoo%7Cbar%5D%5D
https://ad.zanox.com/ppv/images/onepixel.gif
```


**Decoded Requests**


``` text
https://www.zenaps.com/sread.js?a=1001&b=9.00&cr=EUR&c=AA000001&d=DEFAULT:4.50|SALE:4.50&vc=10PERCENTOFF2015&t=0&ch=zx&cks=&l=https://www.advertiser-domain.com/confirmation&tv=2&tt=js&p1=foo&p2=bar
https://www.zenaps.com/sread.php?a=1001&b=9.00&cr=EUR&c=AA000001&d=DEFAULT:4.50|SALE:4.50&vc=10PERCENTOFF2015&t=0&ch=zx&cks=&l=https://www.advertiser-domain.com/confirmation&tv=2&tt=ia&p1=foo&p2=bar
https://ad.zanox.com/pps/?11191C1878128339&mode=[[1|1]]&PartnerID=[[29522697C1532062743|29522697C1532062743]]&OrderId=[[AA000001|AA000001]]&TotalPrice=[[9.00|9.00]]&CurrencySymbol=[[EUR|EUR]]&CID=[[basket|basket]]&XML=[[<z><o><so_up="4.50"_cid=""_/><so_up="4.50"_cid="Sale"_/></o></z>|<z><o><so up="4.50" cid="" /><so up="4.50" cid="Sale" /></o></z>]]&CustomerID=[[15376|15376]]&ReviewNote=[[10PERCENTOFF2015|foo]]
https://ad.zanox.com/ppv/images/onepixel.gif
```

