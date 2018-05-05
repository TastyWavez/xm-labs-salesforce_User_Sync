
# Salesforce Data Sync
* Version 1.0 of Salesforce Customer Data Sync
* Written by B. Walton 5.4.2018

This Salesforce Data Sync Add-on is designed to sync Salesforce Contact Records with xMatters. Sync is triggered by using a custom field on the Contact Record called 'Sync With xMatters'.  


<kbd>
  <img src="https://github.com/xmatters/xMatters-Labs/raw/master/media/disclaimer.png">
</kbd>

# Pre-Requisites
* Admin Access to an xMatters account - If you don't have one, get started with [xMatters](https://www.xmatters.com)
* Admin Access to a Salesforce account - If you don't have one, you can setup a free  [Salesforce Developer Org](https://developer.salesforce.com)

# Files
* [SalesForceDataSync.zip](SalesForceDataSync.zip) - xMatters Communication Plan for Salesforce Data Sync 
* [xMattersHttpCalloutMock.apxc](xMattersHttpCalloutMock.apxc) - APEX Class for xMatters HTTP Mock Callouts.  Required to pass Code Coverage in Salesforce. Add this file to your Salesforce Developer Console.
* [xMattersHttpCalloutMock.apxc](xMattersHttpCalloutMock.apxc) - APEX Class for xMatters HTTP Mock Callouts.  Required to pass Code Coverage in Salesforce. Add this file to your Salesforce Developer Console.
* [xMattersTest.apxc](xMattersTest.apxc) - APEX Class for testing xMatters HTTP Mock Callouts.  Required to pass Code Coverage in Salesforce. Add this file to your Salesforce Developer Console.
* [xMattersreq.apxc](xMattersreq.apxc) - APEX Class for sending HTTP Calls to xMatters. Add this file to your Salesforce Developer Console.
* [xmattersSyncContactTrigger.apxt](xmattersSyncContactTrigger.apxt) - APEX Trigger for initiating HTTP Call to xMatters.  This Trigger also creates the Payload used for the injection. Customize this to modify the Salesforce Fields being sent to xMatters (Only if you know what you're doing). Add this file to your Salesforce Developer Console.


# How it works
This Integration uses a custom property added to the Salesforce Contact Record.  Using a Trigger on the Contact Record, Salesforce sends user Details to xMatters Integration Builder to process the Sync, either Create/Updating Contact or Deleting the Contact.
* This Integration uses the Salesforce Unique Identifier as the xMatters Login.
* Additional Modifications Could be made to Sync with Salesforce Users, or to Create xMatters Login with other properties. Those are not covered in this Integration. 
* Contact [xMatters Consulting Services](mailto:bwalton@xmatters.com) if you'd like assistance with Modifications and Customizations

# Installation
The following section covers installation details 

## xMatters set up
1. Import [SalesForceDataSync.zip](SalesForceDataSync.zip) Communication Plan
2. Navigate to the 'Integration Builder' Section of the Communication Plan and expand the Inbound Integrations view
* Do this by clicking the blue '2 Configured' link
3. Click into the 'Create Contact' link and scroll to the the bottom of the page to Copy the Trigger. 
* Confirm URL Authentication as authentication method in Step 4. 
* Copy the Trigger as it will be used for our Salesforce Setup 
* Example: https://xxx.xmatters.com/api/integration/1/functions/xxx-xxx-xxx-xxx/triggers?apiKey=xxx
4. Repeat Step 3 for 'Delete Contact'


## Salesforce set up
1. Setup xMatters as a 'Remote Site': [Adding Remote Site Settings](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_callouts_remote_site_settings.htm)
2. Open your Salesforce Developer Console: [Steps for Opening Developer Console] (https://help.salesforce.com/articleView?id=code_dev_console_opening.htm&type=5)
3. From the Developer Console, Copy APEX Triggers & Classes from this Repository into your Salesforce Org Instance by creating new APEX Triggers & Classes (File -> New -> Apex Class || Apex Trigger)
* Be sure file names are created correctly and Test classes are loaded
4. On the [xmattersSyncContactTrigger.apxt](xmattersSyncContactTrigger.apxt) Trigger. 
* Update the String endpoint on line 3 with the xMatters 'Create Contact' link, from your xMatters Communication Plan.
* Update the String endpoint on line 17 with the xMatters 'Delete Contact' link, from your xMatters Communication Plan.
* Update the Payload with the fields you will be sharing with xMatters.  For this Use Case, Department will be used as the xMatters Group for this User.
* Save Changes
5. Navigate back to your Salesforce Admin Menu and type 'Contact' in your 'Quick Search' menu to add a new Field to the Contact Record
*[Adding New Fields to Records in Salesforce](https://help.salesforce.com/articleView?id=adding_fields.htm&type=5)
6. Add a new Field with the following Properties:
* Field Data Type = CheckBox
* Field Name = Sync_With_xMatters
* Field Label = Sync With xMatters
* Save and confirm new Checkbox field with API Name Sync_With_xMatters__c has been created on the Contact Record
7. Add New Field to Contact Layout Page
* [Customizing Page Layouts with the Page Layout Editor](https://help.salesforce.com/articleView?id=customize_layoutcustomize_ple.htm&type=5)

# Testing
## Adding a New User
1. While Logged into Salesforce, Navigate to a Contact Record
2. Select 'Edit' Contact Record, Check the Sync With xMatters Checkbox and Save
3. While Logged into xMatters, Navigate to xMatters Reports Tab and search for an 'xMatters Person' event
* New Search -> Message Subject contains 'xMatters Person'
* Find xMatters Person [Create New].
4. Confirm User has been Created in the Users Section
5. Confirm Group has been Created in the Groups Section
6. If Event, User or Group is Missing Check [xMatters Activity Stream](https://help.xmatters.com/OnDemand/xmodwelcome/integrationbuilder/activity-stream.htm)
7. If Activity Stream is Empty, Check your  [Salesforce Execution Logs](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_debugging_system_log_console.htm)

## Updating a User
1. While Logged into Salesforce, Navigate to a Contact Record
2. Select 'Edit' Contact Record, Confirm the Sync With xMatters Checkbox is selected and Edit The User Data. Click Save
3. While Logged into xMatters, Navigate to xMatters Reports Tab and search for an 'xMatters Person' event 
* New Search -> Message Subject contains 'xMatters Person')
* Find xMatters Person [Update].
4. Confirm User has been Updated in the Users Section
5. If Event, User or Group is Missing Check [xMatters Activity Stream](https://help.xmatters.com/OnDemand/xmodwelcome/integrationbuilder/activity-stream.htm)
6. If Activity Stream is Empty, Check your  [Salesforce Execution Logs](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_debugging_system_log_console.htm)

## Deleting a User
1. While Logged into Salesforce, Navigate to a Contact Record
2. Select 'Edit' Contact Record, Uncheck the Sync With xMatters Checkbox and Save
3. While Logged into xMatters, Navigate to xMatters Reports Tab and search for an 'xMatters Person' event 
* New Search -> Message Subject contains 'xMatters Person'. 
* Find xMatters Person [Delete].
4. Confirm User has been Removed in the Users Section
5. If the User is the only Member of the Group Roster, Group should be Deleted
6. If Event is missing, User or Group has not been deleted Check [xMatters Activity Stream](https://help.xmatters.com/OnDemand/xmodwelcome/integrationbuilder/activity-stream.htm)
7. If Activity Stream is Empty, Check your  [Salesforce Execution Logs](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_debugging_system_log_console.htm)

# Troubleshooting
Still Having Issues?

Check for errors and additional information in the following places:
1. [Check xMatters Activity Stream](https://help.xmatters.com/OnDemand/xmodwelcome/integrationbuilder/activity-stream.htm)
2. [Check Salesforce Logs](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_debugging_system_log_console.htm)

Alternatively, contact xMatters Consulting Services if you'd like us to implement or modify this integration for you: [Contact Consulting Services](mailto:bwalton@xmatters.com)