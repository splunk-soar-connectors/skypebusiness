[comment]: # "Auto-generated SOAR connector documentation"
# Skype for Business

Publisher: Splunk  
Connector Version: 2.0.2  
Product Vendor: Microsoft  
Product Name: Skype for Business  
Product Version Supported (regex): ".\*"  
Minimum Product Version: 6.2.1  

This app integrates with Skype for Business to support various investigative actions

[comment]: # " File: README.md"
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
**client_id** |  required  | string | Client ID
**client_secret** |  required  | password | Client secret
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
**contact_email** |  required  | Email or URI of a contact to send message to | string |  `skype contact uri`  `email` 
**message** |  required  | Message to send | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string |  |   success  failed 
action_result.parameter.contact_email | string |  `skype contact uri`  `email`  |   sip:testuser@example.onmicrosoft.com 
action_result.parameter.message | string |  |   hey buddy 
action_result.data | string |  |  
action_result.summary | string |  |  
action_result.message | string |  |   Message sent 
summary.total_objects | numeric |  |   1 
summary.total_objects_successful | numeric |  |   1   

## action: 'list groups'
List all groups of a user

Type: **investigate**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string |  |   success  failed 
action_result.data.\*.7f9d3705-81be-4838-8f33-35910b128f6d | string |  |   please pass this in a PUT request 
action_result.data.\*._links.groupContacts.href | string |  |   /ucwa/oauth/v1/applications/102004749826/people/contacts?groupId=P_B2yQ8EDVUY4YWwX0CUVEW4DvMCQsxpRCtECls3wcc%3d 
action_result.data.\*._links.self.href | string |  |   /ucwa/oauth/v1/applications/102004749826/people/groups/P_B2yQ8EDVUY4YWwX0CUVEW4DvMCQsxpRCtECls3wcc= 
action_result.data.\*._links.self.revision | string |  |   2 
action_result.data.\*._links.subscribeToGroupPresence.href | string |  |   /ucwa/oauth/v1/applications/102004749826/people/presenceSubscriptions?groupId=P_B2yQ8EDVUY4YWwX0CUVEW4DvMCQsxpRCtECls3wcc%3d 
action_result.data.\*.etag | string |  |   1641855850 
action_result.data.\*.id | string |  |   P_B2yQ8EDVUY4YWwX0CUVEW4DvMCQsxpRCtECls3wcc= 
action_result.data.\*.name | string |  |   my group 
action_result.data.\*.rel | string |  |   group 
action_result.summary.total_groups | numeric |  |   4 
action_result.message | string |  |   Total groups: 4 
summary.total_objects | numeric |  |   1 
summary.total_objects_successful | numeric |  |   1   

## action: 'list contacts'
List all contacts of a user

Type: **investigate**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string |  |   success  failed 
action_result.data.\*._links.contactLocation.href | string |  |   /ucwa/oauth/v1/applications/102407129166/people/testuser@example.onmicrosoft.com/location 
action_result.data.\*._links.contactNote.href | string |  |   /ucwa/oauth/v1/applications/102407129166/people/testuser@example.onmicrosoft.com/note 
action_result.data.\*._links.contactPhoto.href | string |  |   /ucwa/oauth/v1/applications/102407129166/photos/testuser@example.onmicrosoft.com 
action_result.data.\*._links.contactPresence.href | string |  |   /ucwa/oauth/v1/applications/102407129166/people/testuser@example.onmicrosoft.com/presence 
action_result.data.\*._links.contactPrivacyRelationship.href | string |  |   /ucwa/oauth/v1/applications/102407129166/people/testuser@example.onmicrosoft.com/privacyRelationship 
action_result.data.\*._links.contactPrivacyRelationship.revision | string |  |   2 
action_result.data.\*._links.contactSupportedModalities.href | string |  |   /ucwa/oauth/v1/applications/102407129166/people/testuser@example.onmicrosoft.com/supportedMedia 
action_result.data.\*._links.self.href | string |  |   /ucwa/oauth/v1/applications/102407129166/people/testuser@example.onmicrosoft.com 
action_result.data.\*.emailAddresses | string |  `email`  |   testuser@example.onmicrosoft.com 
action_result.data.\*.etag | string |  |   1269892302 
action_result.data.\*.expires | string |  |   /Date(1530275859757)/ 
action_result.data.\*.name | string |  |   testuser 
action_result.data.\*.rel | string |  |   contact 
action_result.data.\*.sourceNetwork | string |  |   SameEnterprise 
action_result.data.\*.type | string |  |   User 
action_result.data.\*.uri | string |  `skype contact uri`  |   sip:testuser@example.onmicrosoft.com 
action_result.data.\*.workPhoneNumber | string |  |   9876543210 
action_result.summary.total_contacts | numeric |  |   2 
action_result.message | string |  |   Total contacts: 2 
summary.total_objects | numeric |  |   1 
summary.total_objects_successful | numeric |  |   1 