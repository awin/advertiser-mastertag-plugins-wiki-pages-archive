# Requirements

- Mastertag must be displayed across all pages in the shop
- javascript based tracking code must be loaded unconditionally on the
  order confirmation page.



# Configuration

The publisher will provide a token which should replace the <TOKEN>
placehoder.

### Config code


``` javascript

AWIN.Tracking.Orpiva = AWIN.Tracking.Orpiva || {};
AWIN.Tracking.Orpiva.token = '<TOKEN>';
```


### Configuration example


``` javascript

AWIN.Tracking.Orpiva = AWIN.Tracking.Orpiva || {};
AWIN.Tracking.Orpiva.token = 'C7C2N0D20CB88FJSNAT9';
```


# Relevant Tickets

[PROD-10201](https://jira.awin.com/browse/PROD-10201)

# Plugin Source Code

[View on
GitHub](https://github.com/awin/tracking-advertiser-mastertag/blob/master/src/plugins/thirdParty/orpiva/plugin.js)