## Cross Device Attribution

Cross Device Tracking solution allows Affiliate Window to reward
publishers for multi-device journey transactions. The ability to track
cross-device will give advertisers true understanding of how the
performance channel drives customers, where previously anybody
interacting with the channel across more than one device was instantly
lost.

This solution now allows Affiliate Window to reward publishers for
multi-device purchasing journeys, functionality that has been missing
from the industry since users started to consume the internet on
multiple devices.

Here is the Cross Device Tracking guide which can be shared with clients
who want more information
![<File:Cross_Device.pdf>](Cross_Device.pdf "File:Cross_Device.pdf").

## How does cross device tracking work?

Our cross device tracking solution works by creating a unique ‘profile’
when the consumer is shopping on the advertiser’s website. To help us
build these profiles, advertiser’s site needs to pass Affiliate Window
an encrypted piece of data, which we call user-id.

The user-id is normally a hash of the email address that the user enters
to login to the advertiser’s site. It is encrypted (hashed) before it
leaves the advertiser’s site and can never be used by Affiliate Window
or any associated company to identify the person.

When a consumer clicks through an Affiliate Window link a browser id
cookie called bId will be placed on the user’s device and the click
event will be saved. When the user enters the email address the
mastertag will store the encrypted user-id to the browser id. When the
user makes the transaction on a different device another browser id
cookie will be placed which will link the click and the transaction to
each other.

The user-ids are valid for up to one year and if no transaction, click
or email hash is collect we will discard the user-id from our system. If
a browser id already exists for the consumer’s device a new browser id
will not be created but the current browser id will be renewed for
another one year. When a single device reaches 10 user-ids we will
discard it as these maybe collected from an internet cafe.

------------------------------------------------------------------------

<font color="red" style="font-size:120%">**From this point please do not
forward the information below onto clients as these are Technical
Services Notes.** </font>

## Two types of cross-device tracking

**Active:** the advertiser allows Affiliate Window to receive the
encrypted user-id. In this case the solution will be optimal at tracking
cross-device sales and the programme can expect a significant uplift.

**Passive:** the advertiser doesn’t allow Affiliate Window to receive
the encrypted user-id. In that case, the solution can still track
cross-device, but the uplift will be very limited. All programmes can
run passive cross-device tracking. It only requires configuring a
setting in the provider area. It will be the responsibility of the
technical teams to activate this setting.

**Do not talk about passive cross device tracking to advertisers. We're
not selling this as cross device tracking and it will just be part of
our normal tracking suite**

Our aim is obviously to encourage clients in doing active cross-device
tracking. The next section explains the steps you need to follow to run
active cross-device tracking on your accounts.

## Integration Requirements

The first thing you need to do is get the advertiser’s permission to
receive the user-id. This should be gained in writing, via email. It
will be important to explain to your client that the user-id is
encrypted before it leaves the advertiser’s site, which makes it
impossible for Affiliate Window or any associated company to identify
the person.

Next you need to ensure that the advertiser have the following
requirements for running active cross-device tracking:

- Dwin1 Mastertag on each page of their site

<!-- -->

- Their order references are unique and option ‘Order ref
  de-duplication’ is enabled

<!-- -->

- Confirmation tracking Tag called unconditionally (de-duplication run
  via the Channel Parameter is allowed)

In order to activate Cross device tracking you will need to contact
Sander (sander@affiliatewindow.com) for now. Later on technical services
will be enabling this.

If the programme does not have the required tracking set-up, then
contact technical services so that they help the advertiser implement
the requirements.

## Tag Plugin

|              |                       |
|:------------:|:---------------------:|
| PluginType:  | Cross Device Tracking |
| PluginSetup: |    See Code Below     |
|    Active    |   Tick The Checkbox   |

## Plugin setup code for active cross device tracking

In order to activate the plugin you will need to ensure you go to
provider area, search the advertiser you would like to activate the
plugin for, go to the Account Details section in the Account Settings
and then Enable Cross device Tracking.

The code below goes into the plugin setup field in the tag management
form. Replace emailAddress_textboxName with its real textbox name (or
id) in html (Can be seen within the inspect element of the merchant
site). If the Advertiser has multiple sections as to where they can
enter the email address such as newsletters, Login pages, mobile site
etc. you will also need to list these textbox names. Also make sure you
check the text name/ids on both the desktop and mobile sites as they can
be different.


``` javascript
AWIN.InputIdentifiers = [
    "emailAddress_textboxName",
    "emailAddress_textboxName"
];
```


For example the image below shows where the consumer will enter an email
address to login or signup for the newsletter and the text box name
within inspect element :

<figure>
<img src="Email_textbox.png" title="File:Email_textbox.png" />
<figcaption><a
href="File:Email_textbox.png">File:Email_textbox.png</a></figcaption>
</figure>


``` javascript
AWIN.InputIdentifiers = [
    "elysium_username",
    "customerEmail",
    "email",
    "username"
];
```


Please note that we'll need to have **fixed names** for the email
fields. If names of the email placeholder are randomly generated, then
you can't setup the active crossdevice

## Plugin URL request

If your merchant ID is **3892** , here is the request you will see in
your tracker :
<https://www.awin1.com/a/b.php?merchantId=3892&hash=EMAIL_HASHED&bId=ID_OF_THE_AWIN_bId_COOKIE>

## SETUP

\- For the moment, by default, cross device tracking is **off**

\- to make **passive** crossdevice tracking :
Go on Provider Area \> Merchant Settings \> Account Details \> Tick the
box bellow
![<File:cd1.png>](cd1.png "File:cd1.png")

\- to make **active** crossdevice tracking :
First enable passive crossdevice
then you need to activate the pluggin
![<File:cd2.jpg>](cd2.jpg "File:cd2.jpg")


This will make the option “enable” on merchant welcome page

<figure>
<img src="cd3.png" title="File:cd3.png" />
<figcaption><a href="File:cd3.png">File:cd3.png</a></figcaption>
</figure>

Keep in mind as well that the merchant either need to be unconditional
or allow us to track unknown/direct traffic using the channel parameter.

## How can I identify cross-device transactions?

The interface does not flag cross-device transactions and they will look
like any other transaction. When using the database you will be able to
indentify cross-device transactions as:

**Transaction Source (affiliatewindow.transaction.source)**

|     |                       |
|:---:|:---------------------:|
| 16  | Cross Device Tracking |

**Platform (affiliatewindow.transaction.platform)**

|     |              |
|:---:|:------------:|
| xd  | Cross Device |

## Positives

- Publishers will be rewarded fairly for the transactions which they
  were genuinely involved in the customer journey.

<!-- -->

- Advertiser's will now be able to receive Cross Device Stats as we can
  give them insights into cross device journeys for affiliate traffic.

<!-- -->

- New Advertisers which use Cross device tracking will be more
  attractive to publishers. For example if we have two very similar
  advertiser programs then in the future publishers will want to promote
  the ones with cross device tracking implemented.

## Potential Objections

- Advertiser will need to be unconditionally tracking in order to use
  cross device tracking. If the client would like to conditionally track
  they will need to de-duplicate via the channel parameter.

<!-- -->

- Maximum cookie length of 90 days. If a customer has a cookie length of
  a 100 days then cross device transactions will be only be tracked at
  90 days.

<!-- -->

- Cross device tracking cannot be used when an Advertiser is using
  Offline Tracking.

## FAQs

Coming soon...