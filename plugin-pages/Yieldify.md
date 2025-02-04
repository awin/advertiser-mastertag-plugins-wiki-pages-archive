
# Description

**NOTE: This plugin failed to meet our minimum security requirements and
should not be used anymore.** Reference:
<https://jira.awin.com/browse/SOLUTION-26450>

Yieldify’s unique technology monitors user behaviour pattern and detects
when the visitor is about to leave the site. Once detected, a
personalised overlay message invites the user to leave their contact
information.

Tech contact (CTO): meelan@yieldify.com

Payment Model: CPA

# Integration requirements

- Dwin tag to be shown unconditionally across all product/landing pages
- The Dwin1 tag needs to be displayed on the confirmation page as part
  of the Awin conversion tracking.

**De-duping clients**

Post click - Modifications to the tracking will need to be made to allow
Yieldify visibility on other channels conversions and close the loop.
This can either be done by the client also implementing our tag in
testmode, shown for all other traffic or by the client using the AW
channel functionality. Consult a senior member of the team if unsure.

# How is the tag implemented?

The Yieldify tag is always is the same on every page, the only thing
that needs to change is the yieldify_id. This is a number Yieldify
allocate to each individual client website. ie for the example tags,
Regalar Flores has yieldify_id=406 and Chairpro has yieldify_id=405

|               |                      |
|---------------|----------------------|
| PluginType:   | Yieldify             |
| Plugin Setup: | "See Code Below"     |
| Active:       | "Tick The Check Box" |

## Plugin setup code

The code below goes into the plugin setup field in the tag management
form. Replace \`TAG_ID\` with its real value supplied by **Yieldify**
for the merchant.


``` javascript
AWIN.Tracking.Yieldify = {};
AWIN.Tracking.Yieldify.id = "TAG_ID";
```


## Plugin URL request

When you replace **TAG_ID** by **3892** , here is the request you will
see in your tracker :


``` text
https://app.yieldify.com/yieldify/code.js?yieldify_id=3892&loca=URL_REFERER
```


## Ensure appropriate tracking links are used for example:

• Post Click link to merchant site:
<http://www.awin1.com/awclick.php?mid=MERCHANT_ID&id=AFFILIATE_ID>