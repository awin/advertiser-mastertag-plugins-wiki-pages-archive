
# Description

Call Window, is Affiliate Window’s call tracking solution, which allows
merchants to replace the sales telephone number(s) on their website,
with a dynamically generated telephone number, that can be tracked to
the affiliate who referred the call. Guidance on setting up Freespee
accounts can be found here:
<http://wiki.awin.com/index.php/Staff:Call_Window>

# Tag Plugin

|              |                     |
|--------------|---------------------|
| PluginType:  | callWindow          |
| PluginSetup: | "See Code Below"    |
| Active:      | "Tick The Checkbox" |


=Standard Implementation=

## Plug-in Set Up


``` javascript
AWIN.Tracking.CallWindow = {};
AWIN.Tracking.CallWindow.advertiserId = "ADVERTISER_ID";
```



\*Replace ADVERTISER_ID with the unique customer identifier string
supplied by Freespee, for example 76efcb65-4b4a-40ae-871f-7bec736106a0


==Standard Implementation Example==


``` javascript
Call us now:<span class="fs-dynamic-number">020 7553 2459</span>
```



=="Call Us" Button Example==


``` javascript
<a class="fs-dynamic-number" href="tel:02075532459"><img border="0" height="50" src="/images/callus.png"
width="350"></a>
```



=Advanced Features=

## Use Custom Span Class Name


``` javascript
AWIN.Tracking.CallWindow = {};
AWIN.Tracking.CallWindow.advertiserId = "ADVERTISER_ID";
var __fs_conf = __fs_conf || [];
__fs_conf.push(['addElementClass', 'SPAN_CLASS_NAME']);
```



\*Replace ADVERTISER_ID with the unique customer identifier string
supplied by Freespee, for example a78aafbb-24c2-472c-867e-38791cfb1f7e

- Replace SPAN_CLASS_NAME with the custom span tag class name


==Locate Number Without Span Tag==


``` javascript
AWIN.Tracking.CallWindow = {};
AWIN.Tracking.CallWindow.advertiserId = "ADVERTISER_ID";
var __fs_conf = __fs_conf || [];
__fs_conf.push(['numberDetection', true]);
```



\*Replace ADVERTISER_ID with the unique customer identifier string
supplied by Freespee, for example a78aafbb-24c2-472c-867e-38791cfb1f7e
Please ensure the number to be replaced is added to the "Allowed
numbers" in the Freespee account \[Settings-\>Tracking-\>Allowed
numbers\]


=Connect To Other Number=


``` javascript
AWIN.Tracking.CallWindow = {};
AWIN.Tracking.CallWindow.advertiserId = "ADVERTISER_ID";
var __fs_conf = __fs_conf || [];
__fs_conf.push(['addNumberConfiguration', ['NUMBER_TO_REPLACE', {'connect_to':'CONNECT_TO_NUMBER'}]]);
```



\*Replace ADVERTISER_ID with the unique customer identifier string
supplied by Freespee, for example a78aafbb-24c2-472c-867e-38791cfb1f7e

- Replace NUMBER_TO_REPLACE with the telephone number that Freespee will
  cosmetically modify, for example 020 7553 2459
- Replace CONNECT_TO_NUMBER with the telephone number you want the end
  user to be connected to, for example: 020 7553 0413

Please ensure the number to be replaced is added to the "Allowed
numbers" in the Freespee account \[Settings-\>Tracking-\>Allowed
numbers\]

# Custom Set Ups

## Alpha Rooms


``` javascript
AWIN.Tracking.CallWindow = {};
AWIN.Tracking.CallWindow.advertiserId = "ADVERTISER_ID";
var awinCookieName = "COOKIE_NAME";
var awinCookieLength = COOKIE_LENGTH;
var freespeeSpanTagId = "FREESPEE_SPAN_TAG_ID";

var _readCookie = function(cookieName) {
    cookieName += "=";
    var cookies = document.cookie.split(";");
    for (var i = 0; i < cookies.length; i++) {
        var cookieData = cookies[i];
        while (cookieData.charAt(0) == " ") cookieData = cookieData.substring(1, cookieData.length);
        if (cookieData.indexOf(cookieName) == 0) {
            return cookieData.substring(cookieName.length, cookieData.length);
        }
    }
    return null;
};

callwinidRegExp = /^\d{3,8}$/;
var callwinid = AWIN.Tracking.getQueryVarValue("callwinid", document.location.search.substring(1));
if (callwinidRegExp.test(callwinid) || callwinid == "off") {
    var cookieDate = new Date();
    cookieDate.setTime(cookieDate.getTime() + (1000 * 60 * 60 * 24 * awinCookieLength));
    document.cookie = awinCookieName + "=" + callwinid + "; expires=" + cookieDate.toGMTString() + ";
path=/; domain=" + AWIN.Tracking._getCookieDomain();
}

if (document.getElementById(freespeeSpanTagId) && _readCookie(awinCookieName) == "off") {
    document.getElementById(freespeeSpanTagId).className = "ignore-fs-dynamic-number";
```



\*Replace ADVERTISER_ID with the Alpha Rooms (984) unique customer
identifier string supplied by Freespee.

- Replace COOKIE_NAME with the name of the cookie where you want to
  store last click referrer information; _callwindow is the recommended
  cookie name.
- Replace COOKIE_LENGTH with maximum cookie length in days, for example
  30.
- Replace FREESPEE_SPAN_TAG_ID with what has been populated to Id when
  declaring the Freespee span tag in the page source code, for example
  ctl00_HeaderContent_Header1_callusLbl2 from
  <span id="ctl00_HeaderContent_Header1_callusLbl2" class="fs-dynamic-number">0871
  911 0030</span>.


==Plusnet==


``` javascript
AWIN.Tracking.CallWindow = {};
AWIN.Tracking.CallWindow.advertiserId = "ADVERTISER_ID";

/**** Approved publishers must be added to one or both of the arrays ****/

var plusnetPublisherIds = new Array(PUBLISHER_IDS);
//var plusnetPublisherIds = PUBLISHER_ID;
var plusnetBusinessPublisherIds = new Array(PLUSNET_BUSINESS_PUBLISHER_IDS);
//var plusnetBusinessPublisherIds = PLUSNET_BUSINESS_PUBLISHER_ID;

/************************************************************************/

var _readCookie = function(cookieName, cookieValueType) {
    cookieName += "=";
    var cookies = document.cookie.split(";");
    for (var i = 0; i < cookies.length; i++) {
        var cookieData = cookies[i];
        while (cookieData.charAt(0) == " ") cookieData = cookieData.substring(1, cookieData.length);
        if (cookieData.indexOf(cookieName) == 0) {
            var cookieValue = cookieData.substring(cookieName.length, cookieData.length);
            if (cookieValueType == "awc") {
                awcRegExp = /\d+_\d+_.+/;
                if (awcRegExp.test(cookieValue)) {
                    var awc = cookieValue.split("_");
                    var awcClickTimestamp = awc[1];
                    var currentTimestamp = Math.round(+new Date() / 1000);
                    if (currentTimestamp - awcClickTimestamp < (60 * 60 * 24 * 30)) {
                        return cookieValue;
                    }
                }
            } else {
                return cookieValue;
            }
        }
    }
    return null;
};

var _inPublisherIds = function(publisherId, publisherIds) {
    if (typeof (publisherIds) === "object" || typeof (publisherIds) === "array") {
        for (var i = 0; i < publisherIds.length; i++) {
            if (publisherIds[i] == publisherId) {
                return true;
            }
        }
    } else if (typeof (publisherIds) === "string" || typeof (publisherIds) === "number") {
        if (publisherId == publisherIds) {
            return true;
        }
    }
    return false;
};

AWIN.Tracking.CallWindow.awc = _readCookie("_aw_m_2973", "awc");
var plusnetBusinessAwc = _readCookie("_aw_m_2974", "awc");
AWIN.Tracking.CallWindow.callwinid = _readCookie("_callwinid", false);

if (AWIN.Tracking.CallWindow.awc == null && plusnetBusinessAwc) {
    AWIN.Tracking.CallWindow.awc = plusnetBusinessAwc;
    AWIN.Tracking.CallWindow.advertiserId2 = "PLUSNET_BUSINESS_ADVERTISER_ID";
} else if (plusnetBusinessAwc) {
    var plusnetBusinessData = plusnetBusinessAwc.split("_");
    var plusnetData = AWIN.Tracking.CallWindow.awc.split("_");
    if (parseInt(plusnetBusinessData[1]) > parseInt(plusnetData[1])) {
        AWIN.Tracking.CallWindow.awc = plusnetBusinessAwc;
        AWIN.Tracking.CallWindow.advertiserId2 = "PLUSNET_BUSINESS_ADVERTISER_ID";
    }
}

if ((AWIN.Tracking.CallWindow.awc.substring(0, 4) == "2973"
&& _inPublisherIds(AWIN.Tracking.CallWindow.callwinid,
plusnetPublisherIds) == false) || (AWIN.Tracking.CallWindow.awc.substring(0, 4) == "2974"
&& _inPublisherIds(AWIN.Tracking.CallWindow.callwinid,
plusnetBusinessPublisherIds) == false)) {
    AWIN.Tracking.CallWindow.awc = null;
    AWIN.Tracking.CallWindow.callwinid = null;
```



\*Replace ADVERTISER_ID with the Plusnet (2973) unique customer
identifier string supplied by Freespee.

- Replace PLUSNET_BUSINESS_ADVERTISER_ID with the Plusnet
  Business (2974) unique customer identifier string supplied by
  Freespee.
- Replace PUBLISHER_IDS with a comma separated list of publisher IDs for
  the publishers that are enabled for call tracking on the
  Plusnet (2974) program (or just the publisher ID (declared as number;
  see line commented out) if only one publisher is enabled).
- Replace PLUSNET_BUSINESS_PUBLISHER_IDS with a comma separated list of
  publisher IDs for the publishers that are enabled for call tracking on
  the Plusnet Business (2974) program (or just the publisher ID
  (declared as number; see line commented out) if only one publisher is
  enabled).

For more information setting up Plusnet please see the following link,
[Plusnet Merchant Setup](Staff:Support_MerchantSetups "wikilink")


==Primus Saver==


``` javascript
AWIN.Tracking.CallWindow = {};
AWIN.Tracking.CallWindow.awc = AWIN.Tracking._getAWCValue();
if (AWIN.Tracking.CallWindow.awc.substring(0, 4) == "3552") {
    AWIN.Tracking.CallWindow.advertiserId = "ADVERTISER_ID";
} else if (AWIN.Tracking.CallWindow.awc.substring(0, 4) == "3815") {
    AWIN.Tracking.CallWindow.advertiserId2 = "PRIMUS_SAVER_TRACKER_ADVERTISER_ID";
}
```



\*Replace ADVERTISER_ID with the Primus Saver (3552) unique customer
identifier string supplied by Freespee.

- Replace PRIMUS_SAVER_TRACKER_ADVERTISER_ID with the Primus Saver
  Tracker (3815) unique customer identifier string supplied by Freespee.


=Freespee FTP Details=

|               |                 |          |              |                  |
|---------------|-----------------|----------|--------------|------------------|
| **Client**    | **Hostname**    | **Port** | **Username** | '''Password      |
| BusinessJuice | fs.freespee.net | 21       | awin_bj      | wFyhxZ!?P0R2(7d  |
| MadamVacances | fs.freespee.net | 21       | awin_mv      | Sx=08AYSp90bb\$P |
| Harveys       | fs.freespee.net | 21       | awin_hv      | P3SRz!QQKc!Wb&K  |
| ScottishPower | fs.freespee.net | 21       | awin_sp      | noQ=kp77s8OT6LI  |