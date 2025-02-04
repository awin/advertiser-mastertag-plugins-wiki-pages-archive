
# Requirements

The MasterTag should fire unconditionally on the confirmation page.

# Plugin Configuration Code

The code below goes into *Awin UI \> Toolbox \> Advertiser MasterTag \>
My Plug-ins \> Set-up* (please select plugin name *Sovendus*).

Please replace "**TF_SOURCE_NUMBER**" and "**TF_MEDIUM_NUMBER**"
placeholders with the identifiers provided by the partner.


``` javascript
AWIN.Tracking.Sovendus = AWIN.Tracking.Sovendus || {};
AWIN.Tracking.Sovendus.trafficSourceNumber = 'TF_SOURCE_NUMBER';
AWIN.Tracking.Sovendus.trafficMediumNumber  = 'TF_MEDIUM_NUMBER';
```


# Example


``` javascript
AWIN.Tracking.Sovendus = AWIN.Tracking.Sovendus || {};
AWIN.Tracking.Sovendus.trafficSourceNumber = '1234';
AWIN.Tracking.Sovendus.trafficMediumNumber  = '1';
```


# Relevant Tickets

[TECHSOL-1881](https://awin.atlassian.net/browse/TECHSOL-1881)
[PROD-10683](https://awin.atlassian.net/browse/PROD-10683)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/tree/master/src/plugins/thirdParty/sovendus)