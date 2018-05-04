
# Salesforce Data Sync
This Salesforce Data Sync Add-on is designed to sync Salesforce CONTACTS with xMatters using a custom APEX trigger on the contact record (xmattersSyncContactTrigger.apxt).  


<kbd>
  <img src="https://github.com/xmatters/xMatters-Labs/raw/master/media/disclaimer.png">
</kbd>

# Pre-Requisites
* Version 1.0 of Salesforce Customer Data Sync
* Written by B. Walton 5.4.2018
* xMatters account - If you don't have one, [get one](https://www.xmatters.com)!
* Salesforce account - If you don't have one, you can setup a free Developer Org with Salesforce [Salesforce Developer Org](https://developer.salesforce.com)!

# Files
* [SalesForceDataSync.zip](SalesForceDataSync.zip) - xMatters Communication Plan for Salesforce Data Sync 
* [xMContactSync.apxc](xMContactSync.apxc) - APEX Class for xMatters Contact Sync. Add this file to your Salesforce Developer Console.
* [xMattersHttpCalloutMock.apxc](xMattersHttpCalloutMock.apxc) - APEX Class for xMatters HTTP Mock Callouts.  Required to pass Code Coverage in Salesforce. Add this file to your Salesforce Developer Console.
* [xMattersHttpCalloutMock.apxc](xMattersHttpCalloutMock.apxc) - APEX Class for xMatters HTTP Mock Callouts.  Required to pass Code Coverage in Salesforce. Add this file to your Salesforce Developer Console.
* [xMattersTest.apxc](xMattersTest.apxc) - APEX Class for testing xMatters HTTP Mock Callouts.  Required to pass Code Coverage in Salesforce. Add this file to your Salesforce Developer Console.
* [xMattersreq.apxc](xMattersreq.apxc) - APEX Class for sending HTTP Calls to xMatters. Add this file to your Salesforce Developer Console.
* [xmattersSyncContactTrigger.apxt](xmattersSyncContactTrigger.apxt) - APEX Trigger for initiating HTTP Call to xMatters.  This Trigger also creates the Payload used for the injection. Customize this to modify the Salesforce Fields being sent to xMatters (Only if you know what you're doing). Add this file to your Salesforce Developer Console.


# How it works
This integration uses a custom property added to the Salesforce Contact Record.  We've added a custom property An action happens in Application XYZ which triggers the thingamajig to fire a REST API call to the xMatters inbound integration on the imported communication plan. The integration script then parses out the payload and builds an event and passes that to xMatters. 

# Installation
Details of the installation go here. 

## xMatters set up
1. Steps to create a new Shared Library or (in|out)bound integration or point them to the xMatters online help to cover specific steps; i.e., import a communication plan (link: http://help.xmatters.com/OnDemand/xmodwelcome/communicationplanbuilder/exportcommplan.htm)
2. Add this code to some place on what page:
   ```
   var items = [];
   items.push( { "stuff": "value"} );
   console.log( 'Do stuff' );
   ```


## Salesforce set up
Any specific steps for setting up the target application? The more precise you can be, the better!

Images are encouraged. Adding them is as easy as:
```
<kbd>
  <img src="media/cat-tax.png" width="200" height="400">
</kbd>
```

<kbd>
  <img src="media/cat-tax.png" width="200" height="400">
</kbd>


# Testing
Be specific. What should happen to make sure this code works? What would a user expect to see? 

# Troubleshooting
Optional section for how to troubleshoot. Especially anything in the source application that an xMatters developer might not know about, or specific areas in xMatters to look for details - like the Activity Stream? 
