
# Description

NMP (formerly known as NetMediaPlanet) are international paid search
specialists. They are active in over 70 territories and their paid
search activity is present on all major search engines including Google,
Yahoo & Bing. NMP’s technology allows them to also target through search
engine image extensions and user location (geo-targeting). They operate
on a CPA remuneration model to reduce the risk for the client as opposed
to a standard PPC model.

Although they are best known for their paid search activity, they can
also provide advertisers with display activity in the form of search
retargeting. Their technology combines the initial interest of the user
and relevancy of the paid search to display an on-site add once clicked
through.

# Integration requirements

- The Dwin tag to be shown unconditionally across all product/landing
  pages.

<!-- -->

- The Dwin tag needs to also be displayed on the confirmation page.

# NMP Display

- NMP Display requires postview to be enabled and therefore for the
  merchant to be unconditionally tracking.

# What the tag does?

The tag inserts a HTML ‘<iframe>’ element with a link to the Advertisers
website that hits the Net Media Planet server to record some data passed
to it.

This will occur on every page the Dwin tag has been implemented on but
will hit an alternative url with other data when an AWIN.Tracking.Sale
Dwin tag object is set.

# How is the tag implemented?

The NMPi tag requires the Advertiser's name to be specified in the setup
code. As well as this there are other parameters that are passed in
automatically using the data supplied already in the Dwin tag from
AWIN.Tracking & AWIN.Tracking.Sale.

# Tag Plugin

|               |                      |
|---------------|----------------------|
| PluginType:   | Net Media            |
| Plugin Setup: | "See Code Below"     |
| Active:       | "Tick The Check Box" |


== Plugin setup code == The code below goes into the plugin setup field
in the tag management form. Replace THE_ADVERTISER_NAME with the
merchant whom is being setup.


``` javascript
AWIN.Tracking.NetMedia = AWIN.Tracking.NetMedia || {};
AWIN.Tracking.NetMedia.merchantName = "THE_ADVERTISER_NAME";
```




</source>


#### On sale/confirmation pages


``` html4strict

<iframe src="https://4405841.fls.doubleclick.net/activityi;src=4405841;type=AWINS0;cat=AWINS0;qty=1;cost=50;u1=Example%20Merchant;u2=1001;u3=http%3A%2F%2Fawin1tests.ashtonh.dev.affiliatewindow.com%2FthirdParty%2FnetMedia%2FsalePageTest.html;u6=0;ord=H1001REF?" height="1" width="1" style="height: 0px !important; width: 0px !important; visibility: hidden !important; display: inline !important; margin: 0px !important; border: 0px !important; padding: 0px !important;"></iframe>
```

