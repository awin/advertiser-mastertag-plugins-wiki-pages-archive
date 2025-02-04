# Piwik plugin

## Description

Piwik is a free and open source web analytics application written by a
team of international developers that runs on a PHP/MySQL webserver. It
tracks online visits to one or more websites and displays reports on
these visits for analysis. As of September 2015, Piwik was used by
nearly 900 thousand websites, or 1.3% of all websites, and has been
translated to more than 45 languages. New versions are regularly
released every few weeks

## Plugin setup code

The code below goes into the plugin setup field in the tag management
form.

Replace "SITE_ID" with its real value supplied by **Piwik** for the
Advertiser.


``` javascript
AWIN.Tracking.Piwik = AWIN.Tracking.Piwik || {};
AWIN.Tracking.Piwik.siteId = "SITE_ID";
```



By default it will use zanox piwik system: <https://zanox.piwikpro.com>
but it's possible to use another piwik url by setting up this variable:


``` javascript
AWIN.Tracking.Piwik.url = "PIWIK_URL";
```


