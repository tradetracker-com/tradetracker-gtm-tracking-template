# TradeTracker.com Google Tag Manager Template

This tag template makes it easy to add TradeTracker.com's conversion pixel to your Google Tag Manager container. If you have any questions or need any assistance please contact your Account Manager.

## Before setting up your TradeTracker.com Tag

* Make sure you have either dataLayer variables, or javascript-macro variables configured for transactions
* The TradeTracker Conversion Tag requires a variable for your trasaction id (order id), and the total order amount *excluding* tax
* Campaign Id can be found in the TradeTracker Advertiser Dashboard, it is a unique identifier for your campaign. You can enter this value as text, or you could create a constant variable for it
* Product Id can also be found in the TradeTracker Advertiser Dashboard, this identifier signals what product (commission type) should be used. You can again enter this as text or create a constant variable.
* Make sure you have Google Tag manager Trigger for firing a tag on your conversion or "thank-you" page when a transaction is complete. 

## Setting up your TradeTracker.com Tag

1. Download the the .zip of this repository, create a new template in Google Tag Manager and import the template.tpl file using the overflow menu at the top right
1. Add a new tag, search for the TradeTracker.com Conversion tag custom template and select it
1. Select a Tag Type from the drop-down menu
1. Add your Campaign Id as text or enter the variable name
1. Add your Product Id as text or enter the variable name
1. Enter the variable name for your Transaction (Order) Id variable
1. Enter the variable name for your Transaction (Order) Amount variable ('Conversion' tag type only)
1. Select the correct firing trigger for the tag
1. Save
