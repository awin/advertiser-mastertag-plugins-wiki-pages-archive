
# Tag Plugin

|              |                     |
|--------------|---------------------|
| PluginType:  | buyat               |
| PluginSetup: | "See Code Below"    |
| Active:      | "Tick The Checkbox" |


=Plugin setup code= The code below goes into the plugin setup field in
the tag management form. Replace the buyat merchant PROGRAM_ID with a
real value.


``` javascript
AWIN.Tracking.Buyat = {};
AWIN.Tracking.Buyat.programId = "PROGRAM_ID";
```

