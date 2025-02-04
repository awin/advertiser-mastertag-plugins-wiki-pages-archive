
# Description

Retarget your customers in Facebook Messenger. Send out triggered
messages to your customers and skyrocket your conversion rate! Easy
integration in just 5 minutes.

# Contact

Awin commercial \[Global Publisher Team\]: Ines Filsack
ines.filsack@awin.com

chatchamp tech \[CTO\]: Dominik Grusemann dominik.grusemann@chatchamp.io

chatchamp commercial \[Co-Founder\]: Felix Schroeder
felix.schroeder@chatchamp.io

# Integration requirements

Chatchamp technology can be easily activated through supported
plugins/extensions available for most common shop systems and this is
desired integration type, which doesn't require implementation of
mastertag.

**List of supported shop systems:**

WooCommerce
<https://wordpress.org/plugins/messenger-marketing-for-woocommerce/>

Shopify <https://apps.shopify.com/messenger-marketing-for-shopify>

Magento is coming up (May 2018)

**Custom integration**

If there is no extension available for clients shop system (or client
has very customized shop system), you can proceed with
custom-integration.

In this case,

- Dwin tag to be shown unconditionally on the basket/cart page\*
- The Dwin tag needs to be displayed on the confirmation page as part of
  the Awin conversion tracking. \*
- Plugin requires also basket data on the basket/cart page; zanox legacy
  variables (zx_products) is supported. \*

In order to ensure chatchamp script works correctly, following snippet
must be added on the basket page:


``` javascript
<div class='chatchamp-messenger-checkbox'></div>
```


Please be aware this should be ideally handled by the client and
chatchamp should advise them where exactly the element should be placed.

\[chatchamp\] Custom integration doc

<https://www.chatchamp.io/docs/custom_integration>

# How is the tag implemented?

The ChatChamp plugin has different tags depending on the type of page
visited.

Plugin supports following `PAGETYPE`: basket, checkout

Use if statements to assign `PAGETYPE_IDENTIFIER` based on properties of
the page.

## Plugin setup code

The code below goes into the plugin setup field in the tag management
form. Replace \`ChatChampID\` with its real value supplied by
**Chatchamp** for the merchant.


``` javascript
AWIN.Tracking.ChatChamp = AWIN.Tracking.ChatChamp || {};
AWIN.Tracking.ChatChamp.ChatChampID = "ChatChampID";
AWIN.Tracking.ChatChamp.pagetype= "PAGETYPE_IDENTIFIER";
```


## Plugin URL request

When you replace **ChatChampID** by
**81445027bef03005e151263fe4c706c6238c1baa27fe291f63bd6dfdeadd2a30** ,
here is the request you will see in your tracker :


``` text
http://api.chatchamp.io/js/chatchamp-loader.js?id=81445027bef03005e151263fe4c706c6238c1baa27fe291f63bd6dfdeadd2a30
```


## Basket Page

Plugin requires product data (productIds) on the basket page. Data can
be supplied to the plugin with an array of products (zx_products) or
with the PLT form.

Example:


``` javascript
var zx_products = [];
for (var i = 0; i < google_tag_params.prodid.length; i++) {
    var o = {};
    o.identifier = google_tag_params.prodid[i];
    o.amount = google_tag_params.price[i];
    o.currency = google_tag_params.currency[i];
    zx_products.push(o);
}
```




# Example Complete Setup

Example below is written on the basis that there is no PLT implemented
on the checkout page.


``` javascript


AWIN.Tracking.ChatChamp = AWIN.Tracking.ChatChamp || {};
AWIN.Tracking.ChatChamp.ChatChampID = "81445027bef03005e151263fe4c706c6238c1baa27fe291f63bd6dfdeadd2a30";
AWIN.Tracking.ChatChamp.pagetype = "generic";

if (document.location.href.match(/cart/i)) {
    AWIN.Tracking.ChatChamp.pagetype = "basket";
    var zx_products = [];
    for (var i = 0; i < google_tag_params.prodid.length; i++) {
        var o = {};
        o.identifier = google_tag_params.prodid[i];
        o.amount = google_tag_params.price[i];
        o.currency = google_tag_params.currency[i];
        zx_products.push(o);
    }
}
```

