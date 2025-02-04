# OneTribe plugin

## DEPRACATED

**This plugin is not available since Awin is not working with OneTribe
anymore. Reference: <https://jira.awin.com/browse/PROD-9396>**

## Description

OneTribe is a back-end plugin which is sending server-to-server requests
in batches (every 2 hours) to the API / endpoint of OneTribe for each
transaction from the program which has been activated.

## Endpoint

<https://apixel.onetribeglobal.com/awin/track?merchantId=%7BadvertiserId%7D&totalAmount=%7BtransactionValue%7D&trackedCurrency=%7Bcurrency%7D&transactionDate=%7BtransactionDate%7D&orderId=%7BtransactionId%7D>

## Plugin Integration Reference

<https://jira.awin.com/browse/PROD-8819>

## Plugin Activation

In order to activate plugin for given advertiser, please create a
SOLUTION ticket and provide the advertiser ID, for which the plugin
should be activated. Your ticket will be forwarded to PROD backlog
shortly after. Please bear in mind activation requires amendments to the
code and will be reviewed by an engineer and once the ticket is closed
you can consider the activation process as completed.

## Plugin Requirements

Awin Tracking code (any) must be implemented on the confirmation page,
also for any other event types (like sign-up, registration, etc). Please
bear in mind, currently the endpoint of the partner does not accept
totalAmount passed with 0, this integration of tracking code for LEAD
should use the totalAmount of 1.

## Plugin Known Issues

Currently API / endpoint of the partner does not support requests where
the totalAmount is passed with 0 and following response is expected:


``` javascript
{
"success": false,
"code": 400,
"message": "Bad Request"
}
```


Reference: <https://jira.awin.com/browse/PROD-8993>

## Plugin evaluation

Currently partner is evaluating an option of receiving more granular
data from Awin (like commission groups, product details) in order to
introduce more tailored solution for clients who would like to reward
partner for specific product categories or products.

## List of activated advertisers

New advertisers (ID's) are added and included in the crontab table in
the \#CUSTOM COMMANDS# section
<https://github.com/awin/offline-transaction-importer/blob/master/cron/crontab>