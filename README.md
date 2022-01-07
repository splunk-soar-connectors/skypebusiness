[comment]: # "Auto-generated SOAR connector documentation"
# Skype for Business

Publisher: Splunk  
Connector Version: 2\.0\.1  
Product Vendor: Microsoft  
Product Name: Skype for Business  
Product Version Supported (regex): "\.\*"  
Minimum Product Version: 4\.8\.24304  

This app integrates with Skype for Business to support various investigative actions

[comment]: # " File: readme.md"
[comment]: # "  Copyright (c) 2019-2020 Splunk Inc."
[comment]: # ""
[comment]: # "Licensed under Apache 2.0 (https://www.apache.org/licenses/LICENSE-2.0.txt)"
[comment]: # ""
[comment]: # ""
## Registering the app on Azure portal

This app requires creating an Azure Application. To do so, navigate to <https://portal.azure.com/>
in a browser and log in with a Microsoft account, then follow the steps given below:  

1.  Go to Azure Active Directory → App Registrations and click on **+New Application Registration**
    .
2.  Give a name, select type as **“Web App/API”** and provide a sign-on URL.
3.  After saving the app, open Manifest, change the field **‘oauth2AllowImplicitFlow’** from *false*
    to *true* and Save Manifest.
4.  Go to App Settings → Properties, change **‘Multi-tenanted’** to &quotYES&quot.
5.  Go to App Settings → Required Permissions and click on **+Add** and select **&quotSkype for
    Business Online"**
6.  Add the following Delegated Permissions for your app
    -   Initiate conversations and join meetings
    -   Create Skype Meetings
    -   Read/write Skype user contacts and groups
7.  Go to App Settings → Keys → Password. In the description box, write *‘client_secret’* and
    provide a time duration.
8.  After saving, a key/password would be generated. **Please save it somewhere securely.** This
    would be used as your **client_secret** .

## Phantom Skype Asset

When creating an asset for **Skype for Business** app, place **Application Id/Client Id** of the app
in the **Client ID** field and place the key/password generated in the **Client Secret** field. User
can enter **Tenant** if he chooses, else &quotcommon" would be taken as default. Click **SAVE** .  
  
After saving, a new field will appear in the **Asset Settings** tab. Take the URL found in the
**POST incoming for Skype for Business to this location** field and place it in the **App Settings
-> Reply URLs** field of your registered app. To this URL, add **/result** . After doing so the URL
should look something like:  
  

    https://<phantom_host>/rest/handler/skypeforbusiness_42d0f6b6-c8bb-498c-ae35-a3fc21da8552/<asset_name>/result

  
Once again, click save at the bottom of the screen.

## Method to run test connectivity

  

1.  After setting up the asset and app, click the **TEST CONNECTIVITY** button.
2.  A window should pop up and display a URL.
3.  Navigate to this URL in a separate browser tab.
4.  This new tab will redirect to a Microsoft login page. Log in with a Microsoft account.
5.  After logging in, review the requested permissions listed, then click **Accept.**
6.  **Close that tab after authentication** .  
    -   NOTE:- Users may be required to repeat **Step-3** and **Step-4** multiple times.
7.  The test connectivity window should show a success.

  
The app should now be ready to use.


### Configuration Variables
The below configuration variables are required for this Connector to operate.  These variables are specified when configuring a Skype for Business asset in SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**client\_id** |  required  | string | Client ID
**client\_secret** |  required  | password | Client secret
**tenant** |  optional  | string | Tenant name or Tenant ID

### Supported Actions  
[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied configuration  
[send message](#action-send-message) - Send a message to a contact  
[list groups](#action-list-groups) - List all groups of a user  
[list contacts](#action-list-contacts) - List all contacts of a user  

## action: 'test connectivity'
Validate the asset configuration for connectivity using supplied configuration

Type: **test**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
No Output  

## action: 'send message'
Send a message to a contact

Type: **generic**  
Read only: **False**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**contact\_email** |  required  | Email or URI of a contact to send message to | string |  `skype contact uri`  `email` 
**message** |  required  | Message to send | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.contact\_email | string |  `skype contact uri`  `email` 
action\_result\.parameter\.message | string | 
action\_result\.data | string | 
action\_result\.summary | string | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list groups'
List all groups of a user

Type: **investigate**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.data\.\*\.7f9d3705\-81be\-4838\-8f33\-35910b128f6d | string | 
action\_result\.data\.\*\.\_links\.groupContacts\.href | string | 
action\_result\.data\.\*\.\_links\.self\.href | string | 
action\_result\.data\.\*\.\_links\.self\.revision | string | 
action\_result\.data\.\*\.\_links\.subscribeToGroupPresence\.href | string | 
action\_result\.data\.\*\.etag | string | 
action\_result\.data\.\*\.id | string | 
action\_result\.data\.\*\.name | string | 
action\_result\.data\.\*\.rel | string | 
action\_result\.summary\.total\_groups | numeric | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list contacts'
List all contacts of a user

Type: **investigate**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.data\.\*\.\_links\.contactLocation\.href | string | 
action\_result\.data\.\*\.\_links\.contactNote\.href | string | 
action\_result\.data\.\*\.\_links\.contactPhoto\.href | string | 
action\_result\.data\.\*\.\_links\.contactPresence\.href | string | 
action\_result\.data\.\*\.\_links\.contactPrivacyRelationship\.href | string | 
action\_result\.data\.\*\.\_links\.contactPrivacyRelationship\.revision | string | 
action\_result\.data\.\*\.\_links\.contactSupportedModalities\.href | string | 
action\_result\.data\.\*\.\_links\.self\.href | string | 
action\_result\.data\.\*\.emailAddresses | string |  `email` 
action\_result\.data\.\*\.etag | string | 
action\_result\.data\.\*\.expires | string | 
action\_result\.data\.\*\.name | string | 
action\_result\.data\.\*\.rel | string | 
action\_result\.data\.\*\.sourceNetwork | string | 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.uri | string |  `skype contact uri` 
action\_result\.data\.\*\.workPhoneNumber | string | 
action\_result\.summary\.total\_contacts | numeric | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric | 