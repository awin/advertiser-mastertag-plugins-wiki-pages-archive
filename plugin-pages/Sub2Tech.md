
# Description

The Sub2Tech integration allows you to track user journeys across your
website.

Copied from the integration documentation:

*The Sub2 JavaScript code will ensure that visitors to your site can be
identified and additionally that any page impressions, email address and
order details such as value and items purchased can be captured and
stored on the Sub2 data hub.*

All of the above can be integrated through a single tag.

# Integration requirements

Below are the requirements for each Sub2Tech integration type:

- storeData - **Required** - Basic integration with Sub2Tech
  - Dwin tag to be shown unconditionally, as outlined on
    [here](http://wiki.awin.com/index.php/Advertiser_Tracking_Guide/Standard_Implementation#Journey_Tag_.2F_Mastertag)
- addOrder and addItem - **Optional** - Track conversions through
  Sub2Tech
  - Dwin tag to be shown unconditionally, as outlined on
    [here](http://wiki.awin.com/index.php/Advertiser_Tracking_Guide/Standard_Implementation#Journey_Tag_.2F_Mastertag)
  - Conversion tag to be present on the page, as outlined
    [here](http://wiki.awin.com/index.php/Advertiser_Tracking_Guide#Conversion_Tag).
  - Conversion tag must also include data for \`orderRef\`,
    \`affiliation\`, \`amount\`, \`tax\`, \`shipping\`, \`city\`,
    \`county\` and \`country\` where possible. E.g.
    \`AWIN.Tracking.Sale.affiliation = "some-affiliation";\`. *For field
    definitions, refer to the Sub2Tech integration documentation*
- sendBasket - **Optional** - Track basket items across the site
  - Dwin tag to be shown unconditionally, as outlined on
    [here](http://wiki.awin.com/index.php/Advertiser_Tracking_Guide/Standard_Implementation#Journey_Tag_.2F_Mastertag)
  - Product Level tracking should be implemented as outlined
    [here](http://wiki.awin.com/index.php/Advertiser_Tracking_Guide/Product_Level_Tracking)
  - The \`sendBasket\` functionality will be triggered on every page
    load, but if products are added/removed from the basket using
    Javascript without new page loads, then the following function
    should be executed after the contents are modified:
    \`AWIN.Tracking.Sub2Tech.sendBasket();\`

## Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

- Replace \`%%LICENSE_KEY%%\` with real license key supplied by Sub2Tech
  or the client.
- You can also populate the \`AWIN.Tracking.Sub2Tech.userData\` object
  with any data that should be submitted in the \`storeData\` function
  outlined in the Sub2Tech API integration documentation.

This would usually be dynamically populated with user data on the
publisher site.


``` javascript
AWIN.Tracking.Sub2Tech = {};
AWIN.Tracking.Sub2Tech.licenseKey = "%%LICENSE_KEY%%";
AWIN.Tracking.Sub2Tech.userData = {};
```



Example:


``` javascript
AWIN.Tracking.Sub2Tech = {};
AWIN.Tracking.Sub2Tech.licenseKey = "642281c3-2112-4bff-a6b1-9o9679ea1a7d";
AWIN.Tracking.Sub2Tech.userData = {};
AWIN.Tracking.Sub2Tech.userData.Email = 'tom@gmail.com';
```


