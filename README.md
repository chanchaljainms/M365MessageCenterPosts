# Microsoft 365 - Message Center Posts Automation

## Summary

This solution brings the power of SharePoint and extensibility of SharePoint to Message Center Posts.

Admins struggle managing Message Center posts lists and come up with various solutions to track and manage M365 Message Center Posts. Some use Excel, Planner, Word, Email etc.

There is a Microsoft provided Import to Planner as well, but not easy to manage and view and extend as if this information was living in SharePoint.

This solution uses a List Template, Azure AD App, Graph API calls (and more) in Power Automate and brings the information in SharePoint.

We have created some default views to get started and some default columns in addition to the information column to track, manage each post.

Customers\\User can extend it to build powerful solutions on top of the SharePoint list to extend it. Like build a workflow to notify, remind, auto assign etc. (Not part of this solution)

## Features

*   Bring Message Center Posts weekly to a SharePoint list
    
*   Views by Technology and Severity
    
*   Views with boards to easily track and update status
    

## Pre-Requisites

*   Azure AD app creation permissions
    
*   Account that has Power Automate license for Premium Connector
    
*   New or Existing SharePoint site with Site Owner permissions
    

# Setup Instructions

## Azure AD Setup

1.  Register an App following the steps at [https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-register-app](https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-register-app)
    
2.  Use the following values during App registration
    
    *   Name – A name that suits your organization standards (example - M365 Message Center Power Automate)
        
    *   Supported Account Types - Accounts in this organizational directory only
        
    *   Redirect URI - **N\\A**
        
3.  Once the app is registered grant the following API permissions
    
    *   Microsoft Graph – Application - ServiceMessage.Read.All
![AZ AD App](https://github.com/chanchaljainms/M365MessageCenterPosts/blob/main/Images/AzureADAppReg.png)


4.  Generate a Client Secret for the app and keep it safe. The value will be used in the flow.
    
5.  Configure other properties as required by your Organizational standards but is not needed for the current solution


## SharePoint Setup

1.  Create a new Teams site or use an existing modern Teams site.
    
2.  Navigate to the relative URL for the site /\_catalogs/lt/
    
    *   EX: https://XXX.sharepoint.com/sites/M365MessageCenter/\_catalogs/lt/
        
3.  Upload the list template M365MessageCenterPosts.stp file which is part of the solution. Download Link
    
4.  Once the upload is complete, we will create a new list based of the template. Navigate to the relative URL for the site /\_layouts/15/new.aspx?CustomTemplate=M365MessageCenterPosts.stp
    
    *   Ex: https://XX.sharepoint.com/sites/M365Messagecenterposts/_layouts/15/new.aspx?CustomTemplate=M365MessageCenterPosts.stp
![SP List Create](https://github.com/chanchaljainms/M365MessageCenterPosts/blob/main/Images/SPListCreate.png)
5.	Enter the Name of the list as "M365MCPosts"
6.	Enter a meaningful Description.
7.	Click on "Create"
8.	Once the list is created, it will navigate to the newly created list page
![SP List Created](https://github.com/chanchaljainms/M365MessageCenterPosts/blob/main/Images/SPList.png)


## Flow Setup
1.  Navigate to [https://make.powerautomate.com/](https://make.powerautomate.com/)
    
2.  Once signed-in, select the correct Environment where you want to deploy the flow.
    
    *   **IMPORTANT:** The flow uses Premium Connector, so make sure the license setup etc. is done to ensure the flow will execute.
![Flow Environment](https://github.com/chanchaljainms/M365MessageCenterPosts/blob/main/Images/FlowEnv.png)
        
3.  Once the correct environment is selected, click on "My Flows" on the left navigation.
    
4.  When the "My Flows" page loads, click on "Import" button on the top toolbar and Select "Import Package (legacy)".
    
5.  On the Import Package page, Click on the "Upload" button and select the **M365-MessageCenterPosts-ImportToSPV3\_20250223053108.zip** file (part of the solution) from the file explorer (navigate to the folder where you have the file saved).
    
6.  Once the package has uploaded, and the screen to update the information comes up, update the "Name" and the "Connections".
    ![Flow Import](https://github.com/chanchaljainms/M365MessageCenterPosts/blob/main/Images/FlowImportS2.png)
7.  Click on "Import".
    
8.  After the flow has imported successfully, navigate to "My Flows" page and find the flow with the name provided. Click on the Edit button (pencil icon).
    
9.  Once in the Flow Designer page, update the "Recurrence" of the flow.
    
10.  Update the values for the variables that start with "MODIFY" with the correct values
    

*   TenantId (Value from the Azure AD registered application)
    
*   ClientId  (Value from the Azure AD registered application)
    
*   Secret (Value from the Azure AD registered application)
    
*   SiteURL (URL of the SharePoint site that was created)
    
*   M365PostsListTitle (Title of the List that was created)
    
*   EmailToBeNotified (Email Address of the mailbox to notify of errors in flow)
    
*   NumberofDaysPosts (Default Value is 7 – Increase or decrease depending on how often you want the flow to run and how many past days post you want it to process).
    
    *   Example if you plan to run the flow every week once, set it to 7 so it will bring any posts generated in the last 7 day.
        
*   If required, update the Body of the Email to be sent on Error by updating the actions as shown in the screenshots below.
  
![Update Flow Vars](https://github.com/chanchaljainms/M365MessageCenterPosts/blob/main/Images/FlowUpdateVars.png)  
![Update Error Email](https://github.com/chanchaljainms/M365MessageCenterPosts/blob/main/Images/FlowError.png)

11.  Once the values have been updated, "Save" the flow and "Test" run it.
  

## The Solution is provided as-is. Please test it in a Non-Prod environment before deploying it to Production.
    
13.  If everything was setup correctly, including the Azure AD app, the SPO site, the Message Center Posts list, the flow should run without error.
    
14.  Once the Test run is successful, do not forget to "Turn On" the flow.

