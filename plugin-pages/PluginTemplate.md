**NOTE**: this page is use as a template by Tech Solutions team, it is
not a genuine plugin page.


# Page types

The plugin will fire on all pages, including the confirmation page.

# Requirements

The Advetiser MasterTag should fire on all pages unconditionally.

# Plugin Configuration Template

Check the following link for details on how to enable AMT plugins: [How
To Configure And Enable AMT
Plugins](Staff:HowToConfigureAndEnableAMTPlugins "wikilink")

Please replace "**IDENTIFIER**" placeholder with the identifiers
provided by the partner.


``` javascript
AWIN.Tracking.Plugin = AWIN.Tracking.Plugin || {};
AWIN.Tracking.Plugin.identifier = "IDENTIFIER";
```


# Example


``` javascript
AWIN.Tracking.Plugin = AWIN.Tracking.Plugin || {};
AWIN.Tracking.Plugin.identifier = "1aw321e2131daw32";
```


# Relevant Tickets

[TECHSOL-4745](https://awin.atlassian.net/browse/TECHSOL-4745)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty)