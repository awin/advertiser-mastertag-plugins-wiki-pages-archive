## Zero

## Plugin information

This release introduces a new plugin Zero.

The purpose of this plugin is to use the unique BIN (first 4-6 digits of
a card number) issued from the publisher to associate any sales from the
consumer using those issued cards back to the publisher on the Awin
platform.

The plugin will check the credit card field for a prefix. If this is
spotted, it will then use bounceless tracking to create a click for the
publisher linked to that prefix.

No information is taken from the card payment page.

## Plugin set up

The code below goes into the plugin setup field in the tag management
form. This code should be fired on the on the purchase page


``` javascript
AWIN.Tracking.Zero.Inputs: ['input_field_card_number_id']

AWIN.Tracking.Zero.PrefixPublisherPairs: {
    Prefix: publisherID,
    prefix: publisherID
}

AWIN.Tracking.Zero.PublisherConfigs: {
    publisherID: { baseUrl: 'https://..', clickRef: 'clickref' },
    publisherID: { baseUrl: 'https://..' },
}
```


Example:


``` javascript
AWIN.Tracking.Zero.Inputs: ['input_field_card_number_id']

AWIN.Tracking.Zero.PrefixPublisherPairs: {
    111111: 464009,
    999999: 45628
}

AWIN.Tracking.Zero.PublisherConfigs: {
    45628: { baseUrl: 'https://..', clickRef: 'clickref_45628' },
    464009: { baseUrl: 'https://..' },
}
```

