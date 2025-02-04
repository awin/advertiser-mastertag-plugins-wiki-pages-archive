
## Technical Requirements

- You MUST have the [Container plugin](Staff:Product_Scraper "wikilink")
  already set up before adding this plugin
- Merchant needs to have PLT so that we can pass basket data to Ultimate
  Feed on the confirmation page
- Merchant has a unique \`Company ID\` issued by Ultimate Feed

## Tag Plugin

Please fill the form on the tag management page (old provider area) as
illustrated below.
{\| border = '1'

\| PluginType:

\| Ultimate Feed

\|-

\| Plugin Setup:

\| "See Code Below"

\|-

\| Active:

\| "Tick The Check Box"

\|}


== Plugin setup code == The code below goes into the plugin setup field
in the tag management form. Replace \`COMPANY_ID\` with real value
supplied by Ultimate Feed.


``` javascript
AWIN.Tracking.UltimateFeed = {};
AWIN.Tracking.UltimateFeed.companyId = "COMPANY_ID";
```

