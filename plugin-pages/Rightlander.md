
# Requirements

Advertiser MasterTag must to be fired unconditionally on landing page.

The affiliate ID should be present in the advertisers' click appends
setup. The plugin will try grab the affiliate ID from the Singleview
appends (from the `sv_campaign_id` parameter), and if this is not found
then it looks for a `rl_aff_id` parameter.

If the `sv_campaign_id=!!!id!!!` parameter is not in the advertisers'
click appends setup, then you should add `&rl_aff_id=!!!id!!!` to their
click appends setup.

# How To Enable the Plugin

The plugin can be activated via one-click activation from the Plugin
Store \> Discovery page.

# Relevant Tickets

[TECHSOL-10949](https://awin.atlassian.net/browse/TECHSOL-10949)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/rightlander/plugin.js)