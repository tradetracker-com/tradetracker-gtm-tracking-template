# TradeTracker.com Google Tag Manager Template

This tag template makes it easy for advertisers to add TradeTracker.com's conversion pixel to Google Tag Manager container. This template is now available through Google's [Communinity Template Gallery](https://tagmanager.google.com/gallery/#/owners/tradetracker-com/templates/tradetracker-gtm-tracking-template). If you have any questions or need any assistance with using this template, please contact your Account Manager or email at support@tradetracker.com.

### Contents: 
* [Configuring your Tag](#config)
* [Before setting up your tag](#preparation)
  * [Sales Tag Variables & Triggers](#sales)
  * [Leads Tag Variables & Triggers](#leads)
* [Other Tag Types](#other)

----

## <a name="config"></a>Configuring your Tag

1. Download the the .zip of this repository and extract (unzip) the archive  
1. Create a new template in Google Tag Manager and import the template.tpl file from the zip using the overflow menu at the top right
1. Add a new tag, search for the TradeTracker.com tag custom template and select it
1. Select a Tag Type from the drop-down menu
1. Add your Campaign Id as text or enter the variable name
1. Add your ProductGroup Id as text or enter the variable name
1. Enter the variable name for your Transaction  Id variable
1. Enter the variable name for your Transaction Amount variable ('Sales' tag type only)
1. Enter the currency code that transactions on your website will be made in
1. Select the correct firing trigger for the tag
1. Save the tag


## <a name="preparation"></a>Before setting up your TradeTracker.com Tag

Make sure you have a **Campaign Id** and **ProductGroup Id** that have been provided by your Account Manager at TradeTracker.com. You'll need to enter these during the tag configuration.

You'll also need to ensure that you have GTM (Google Tag Manager) Variables configured that capture the data that you want to track, and GTM Triggers to fire the tag on these events. 

## <a name="sales"></a>Sales Tag Variables & Triggers
If you want to track retail sales from your website you will need to capture the transaction (order) details, and fire this tag on the purchase event. For this we highly recommend using Google's [Enhanced Ecommerce](https://developers.google.com/tag-manager/enhanced-ecommerce#purchases) model for pushing purchase events to the dataLayer. We require these two specific variables:

### Trasaction ID:
This variable should capture the unique Transaction or Order ID for the sale. This should be the same ID that you use to track your sales internally, and it's important that it's unique for every sale. 

In the Enhanced Ecommerce purchase model this variable can be found in the dataLayer at `ecommerce.purchase.actionField.id`. If you need to create new GTM variable for this value, create a new dataLayer type variable, and enter this address in the "Data Layer Variable Name" field.


### Transaction Amount:
This variable should capture the total monetary amount for the sale **excluding** any applicable tax such as VAT. It should be formatted as a "string", and should be a dot-decimal number to two decimal places. 

Examples: 
```
Sale amount:      $9.81 => "9.81"
Sale amount: € 2.145,99 => "2145.99"
```

The transaction amount cannot be taken directly from the Enhanced Ecommerce purchase object, as the "revenue" variable typically contains the total amount *including* tax. 

The recommended way to capture this amount is with a "Custom JavaScript Variable" in GTM. You will first need to create dataLayer variables for the transaction revenue (`ecommerce.purchase.actionField.revenue`) and transaction tax (`ecommerce.purchase.actionField.tax`) amounts.

Once this is done you can then create a new Custom JavaScipt Variable that should look something like this: 

```javascript
function () {
  return ({{your_transaction_revenue_variable}} - {{your_transaction_tax_variable}}).toFixed(2)
}
```

### Currency:
This variable should capture the currency code that your transactions on your website are made in. If this will always be the same you can just type in the three letter [ISO 4217 currency code](https://en.wikipedia.org/wiki/ISO_4217#Active_codes). If it will vary, you may need to create a custom variable that will capture this transaction currency and provide it to the tag.


### Purchase Trigger:
This GTM Trigger should be set to fire either when a "purchase" event is pushed to the dataLayer, or to match the url of your post-purchase "thank-you" page and fire the tag there. 

Firing on the purchase event is a more reliable way to fire the tag, and if you use the Enhanced Ecommerce purchase model you can create a "Custom Event" trigger, and enter `purchase` as the "Event name" to create this trigger.

Alternatively if you need to create a trigger based on the thank-you page url or another event, test it thoroughly to make sure that it fires reliably and that the transaction detail variables will be avialable to the tag when the trigger fires it.

----


## <a name="leads"></a>Leads Tag Variables and Triggers
If you want to track custom leads events such as email signups or demo requests, you will need to create some custom variables to provide to the TradeTracker.com tag. Due to the highly customizable nature of these events, we cannot offer as much advice as we can for the sales tag, but we do have a few guidelines.

### Transaction ID: 
The Leads tag still requires a Transaction Id. In this case the transaction id tracks a unique user event on your website. If this will track something like email signups where an id is returned from the submitted form, you could provide this id so that these leads events can be matched from TradeTracker.com's tracking to your own analytics. 

If you are tracking an event that does not have an provide it's own id, you could create a unique identifier for events by combining a random number and a timestamp in a GTM Custom JavaScript variable. For example:  

```javascript
function () {
  return Date.now() + Math.random() 
}
```

### Event Trigger
The trigger for your leads tag will be defined by the type of user event that you wish to track. If the event includes a click on a particular button, or a post-signup page you can create GTM triggers for these events. Alternatively you may want to look at creating a custom event trigger. More information on how to set up these triggers can be found on Google's [Trigger types](https://support.google.com/tagmanager/topic/7679108?hl=en&ref_topic=7679384) article.

----

## <a name="other"></a>Other Tag Types:
This Google Tag Manager template only supports the most common tracking scenarios for TradeTracker.com marketing campaigns. If you run a more complex performance marketing campaign that makes use of multiple campaigns for different brands, multiple ProductGroups, Exclusive Voucher Codes or needs to support multiple countries, please get in touch with your TradeTracker.com Account Manager for further support and guidance on how implement our tracking. If you're unsure of how to contact your Account Manager, please email us at support@tradetracker.com

