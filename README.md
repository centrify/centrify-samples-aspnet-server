# centrify-samples-aspnet-server

Notes: This repository contains the source code for an example ASP.net web site that showcases the ability to integrate features of the Centrify Identity Service Platform using the platforms API's. 
The solution centrify-samples-aspnet-server.sln (VS 2015) contains two projects:
  1. Centrify.Samples.DotNet.ApiLib - Includes a general REST client for communicating with the CIS Platform, as well as
  multiple classes that utilize the REST client to make calls to specific platform API's.
  2. Centrify.Samples.AspNet.ApiDemo - An example web site which utilizes the ApiLib project to perform many operations based on the interaction of the user in the web based UI.
  
This example web site is also provided as a hosted, and fully functioning, example and can be accessed at https://apidemo.centrify.com. The hosted version of this site is connected to its own Centrify tenant, allowing anyone 
to register and test out the example with out needing to go through the installation of this project in their own environment.

The ApiDemo example is the best place to start when learning how to integrate the Centrify Identity Platform into custom UI's, be it a web application, a mobile application, or even a desktop application.
The ApiDemo example is also a great starting point in creating custom portals for users from scratch, or other custom pages such as custom login screens. The code in the ApiDemo example is meant to be isolated from
most other pages in the project so that it can easily be lifted from this project and easily inserted into other C# based projects (with some exceptions). The code can also be used as a whole to customize and host as desired in order to jump start 
the development needed to create a custom web based UI. 

# Included Features:

  1. Login.aspx
      - The Login sample page is a full integration of the Centrify Authentication API's. (Described in the Centrify Development Portal at https://developer.centrify.com/v1.0/reference#post_security-startauthentication)
        The integration includes support for the Centrify Adaptive Authentication Profiles, User Self Service (lock out and forgot password), and Social Login.
  2. Register.aspx
      - The Registration sample page is a simple example of user self-registration. This page uses an admin service account to call the Centrify Create User API ( https://developer.centrify.com/v1.0/reference#post_cdirectoryservice-createuser)
        to create users based on the information that the user populates in the page UI. This is meant to be a simple example that could be expanded on depending on internal use cases (i.e. admin approval flows, etc.). 
  3. Register_oAuth.aspx
     - This example is an alternative to Register.aspx that uses OAuth Client Credentials Flow, with the site acting as a confidential client, to call the create user API. OAuth is a more preferred, and secure, way of handling the service account need. OAuth documentation can be found at https://developer.centrify.com/docs/oauth.
  4. Manage.aspx
      -  The Management page is an example of integrating management functions from the Centrify Management Portal into a custom UI. This page only appears in the API Demo site if the logged in user is a sysadmin in Centrify. This will not be available in the hosted site at https://apidemo.centrify.com
         but is included in this project as an example. The management page supports the creation and modification of users, and the creation and modification of Centrify Roles.
  5. Applications.aspx
      -  The Apps page is an example of integrating the Centrify GetUPData API (https://developer.centrify.com/v1.0/reference#post_uprest-getupdata), which pulls a list of all Single Sign On applications that the logged in user has access to, and displays
         the application icons and information in the same way as the Centrify User Portal. 
  6. MyAccount.aspx
      - The My Account page is an example of user self-service, allowing the user to edit some portions of their user profile. 
  7. Logout.aspx
      - The Logout page contains logic to assist with logging the user out of their Centrify session.
      
# Website Design Details:    
 
 The API Demo sample project was built using ASP.Net (HTML, CSS, and JavaScript), and C# (server side code). 
 
 The API Demo project makes use of the following third party libraries:
 - http://getbootstrap.com/
 - http://fontawesome.io/
 - https://github.com/lipis/bootstrap-social
 
 The API Demo project is based on the standard ASP.Net sample project template in Visual Studio 2015. All Pages use the master page Site.Master. 
 The Web.config for the API Demo contains many settings that need to be configured on a per environment basis. 
      

# Installation and use Instructions:

Note: Installation may differ from environment to environment. Below are the most common steps needed.
 
 Note: 2: The API Demo project can also be installed via The Publish Web feature in Visual Studio. This automates deployment completely.

1. Install IIS on a Windows Server and ensure that all .NET and ASP features are installed via server manager. A majority of all deployment issues where the site will not launch is caused by not having the correct features installed.

2. Download the API Demo repository and place in the Windows Server wwwroot folder or a folder of your choice. 

3. Make sure folder permissions are set to your appropriate audience and user level on your network. 

4. Set up the web application in IIS and point it to the folder created in step 2. Please reference Microsoft documentation on how to do this.

5. Customize the site Web.config. The Web.Config will have the following options that need to be customized.

 "TenantUrl" value="https://tenant.centrify.com"
 
   Note: This can be found by logging into your tenant and looking at the URL after login. Do not include anything after .com here.
    
 "AdminServiceAccount" value="user@domain"
 
   Note: The user account used as an admin service account needs to have a policy set up in Centrify that does not require MFA. The service account in this example is coded to only use User/Pass for authentication.
    
 "AdminServicePass" value="pass" 
 
 Note: If using OAuth for the user registration page, "Register_oAuth.aspx", the Client ID and Client Secret are used in place of the admin service account. For details on configuring a confidential client, please see https://developer.centrify.com/docs/oauth.
 
 "ClientId" value = "pass"
 
 "ClientSecret" value="ClientId@Domain"
 
 "DefaultDomain" value="@yourdomain.com"
 
   Note: This domain is hidden from the user. This is the domain that all users that use the registration screen will be created under and it is the domain that all usernames will be concatenated with in the login page.
   
6. Start the web site in IIS and navigate to it.
    
 


