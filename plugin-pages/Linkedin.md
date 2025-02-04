## Plugin Setup code for AWIN integrations

The code below goes into the plugin setup field in the tag management
form.

- Replace `PARTNER_ID` with real value supplied by linkedin.


``` javascript
AWIN.Tracking.linkedin = AWIN.Tracking.linkedin || {};
AWIN.Tracking.linkedin.partnerId = "PARTNER_ID";
```

