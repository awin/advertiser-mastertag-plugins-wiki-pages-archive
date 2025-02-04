
# Description

Uniqodo is the enabler of every voucher code a merchant puts out to the
market, allowing them to issue single-use unique voucher codes to every
shopper for every promotion, providing control of issuance and
redemption across all their marketing channels.

**Tech contact**

**Name:** Chris Giddins

**Email:** chris.giddins@uniqodo.com

**Tel:** 07787336688

# Integration requirements

- At a minimum Dwin tag to be shown unconditionally on capture pages
- The Dwin1 tag needs to be displayed on the confirmation page as part
  of the Awin conversion tracking.
- Merchant must be Unconditionally Tracking

# How is the tag implemented?

The Uniqodo plugin has one tag which will be fired on two occasions. For
each of these the Uniqodo specific \`uniqodoAdvertiserId\` will need to
be set.

The visit tag will fire on every page.

The other is the redemption tag which only fires on a sale page. This
call accepts parameters taken from the Awin Tracking Sale data, to
record the \`order ref\`, \`amount\`, \`voucher\` and \`currency\`.

The \`Uniqodo Advertiser ID\` is specified by Uniqodo which they
allocate to each individual client website.

# Tag Plugin

|              |                   |
|--------------|-------------------|
| PluginType:  | Uniqodo           |
| PluginSetup: | See Code Below    |
| Active       | Tick The Checkbox |

# Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace SPECIFIC_UNIQODO_ADVERTISER_ID with its real value supplied by
**Uniqodo** for the Advertiser.


``` javascript
AWIN.Tracking.Uniqodo = AWIN.Tracking.Uniqodo || {};
AWIN.Tracking.Uniqodo.id = "SPECIFIC_UNIQODO_ADVERTISER_ID";
```


