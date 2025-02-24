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
        
4.  Generate a Client Secret for the app and keep it safe. The value will be used in the flow.
    
5.  Configure other properties as required by your Organizational standards but is not needed for the current solution


## SharePoint Setup

1.  Create a new Teams site or use an existing modern Teams site.
    
2.  Navigate to the relative URL for the site /\_catalogs/lt/
    
    *   EX: https://XXX.sharepoint.com/sites/M365MessageCenter/\_catalogs/lt/
        
3.  Upload the list template M365MessageCenterPosts.stp file which is part of the solution. Download Link
    
4.  Once the upload is complete, we will create a new list based of the template.
    
5.  Navigate to the relative URL for the site /\_layouts/15/new.aspx?CustomTemplate=M365MessageCenterPosts.stp
    
    *   Ex: https://m365x25136000.sharepoint.com/sites/M365Messagecenterposts/_layouts/15/new.aspx?CustomTemplate=M365MessageCenterPosts.stp


