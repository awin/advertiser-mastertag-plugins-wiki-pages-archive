
# Description

Fraudlogix are a thirdparty fraud checks provider. They check user
details relating to a transaction against a database of ecommerce fraud
( <http://fraudlogix.com/> for more). We are currently use their tag to
monitor transactions on our merchants site for naughty affiliates.

# Tag Plugin

Using the tag manager, set up Fraudlogix plugin as below (no setup code
needed):
{\| border = '1'

\| PluginType: \| FraudLogix

\|-

\| PluginSetup:

\|-

\| Active \| Tick The Checkbox

\|}
= Affiliate ID tracking using click append = In order to make passing
Affiliate ID to FL possible:

- merchant's Clickthrough page must point to the merchant website with
  our container tag present- this is often the merchant homepage.
  However some merchants use a thirdparty as their Clickthrough URL in
  which case our click append will be lost through redirect to merchant
  website. You can see this on the merchant details page (explained
  below)

<!-- -->

- any custom click append for any promotion type should also be updated
  with the click append below. You can find promotional type specific
  click appends in the merchant promotional linking settings in darwin
  provider area

## Setting up click append

- Look up the merchant details in the old provider area
- Open the Tracking defaults section
- Add the following to the Click Append section: \`xid=!!!aid!!!\`