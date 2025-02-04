# Supported Pages

- Generic Page set up only (for all pages)

# Configuration

Replace `"CYBBA_ID"` with real values.

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | Cybba             |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

## Generic Page Configuration

The code below goes into the plugin setup field in the tag management
form. Replace \`CYBBA_ID\` with its real value supplied by Cybba for the
merchant. The Cybba ID should have the following format:
"XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXX" and can contain letters and
numbers.


``` javascript
AWIN.Tracking.Cybba = AWIN.Tracking.Cybba || {};
AWIN.Tracking.Cybba.id = "CYBBA_ID"; //REQUIRED
```


## Example


``` javascript
AWIN.Tracking.Cybba = AWIN.Tracking.Cybba || {};
AWIN.Tracking.Cybba.id = "A94JSSE2-SD22-KN41-0G4S-9DMF04M3LD6"; //REQUIRED
```


# Relevant Tickets

[PROD-7013](https://jira.awin.com/browse/PROD-7013)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/cybba/plugin.js)