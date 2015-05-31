#Office Mail App for Rallyteam#
####[Shawn Cicoria](https://twitter.com/cicorias "Twitter"), Software Architect – DX > TED, May 14, 2015####
The Microsoft Office Platform is focused on enhancing the collaboration experience. This case study introduces you to Office Mail Apps and the ease of both building, integrating, and enhancing the collaboration experience for users. The example shown here gets you up and running quickly with all the parts necessary to build a Mail App customized for your users.  Additionally, for IT Pros it illustrates the ease to which you can make your organization’s own Mail Apps or 3rd party apps available to your users.

Working with Rallyteam, a MS Ventures Accelerator participant, a simple but effective Mail App was created to demonstrate an action oriented add-in with activated within the Context of a Mail item.
##Audience##
The primary target audience are Developers and Solution Architects; IT Pros need to understand the deployment and Trust model that exists. 
##Tags##
Mail Apps, Office, Office 365, O365, Collaboration, Outlook, Contextual
##Background##
[Rallyteam](http://Rallyteam.com) provides a tool that facilitates project awareness and resource assignment within an organization. The platform is a matching service for projects and people for assignments that wouldn’t normally be visible within an organization. It attempt to achieve optimization of project assignments based upon numerous factors such as interests, kudos (which Rallyteam calls props for [*proper recognition*](http://en.wiktionary.org/wiki/props)), experience, and ratings of each person that participates. The essence is for self-forming teams and optimization of resource assignment through matching – thereby identifying unknown capacity and interests of people. It also has tools to help identify skills gaps or gluts.
##Opportunity##
Many organization users are email-centric people. They spend an enormous amount of time within an email client – either a desktop application like Outlook, browser-based (like Outlook Mail App – OWA), and their mobile devices.

During that day, there may be emails that could potentially trigger or should trigger some action, often requiring users to switch context or applications to focus on that action. This context switch is something Office Apps intends to minimize or eliminate by providing actionable visual elements within the productivity application they are currently using. 

With Office Mail Apps we have the ability to activate an actionable link, then provide a User Interface (UI) that allows the user to interact with an Application while never leaving the Outlook interface – reducing steps, decreasing context switching, and making things happen in a friction free manner.

Example of an email – NOT about a project or Opportunity
For a high level overview of the flow, see the diagram Figure 8 - High level deployment.
 
**Figure 1 - Mail app not about a project**
![Figure 1 - Mail app not about a project](https://github.com/cicorias/ProjectUnite/blob/master/img/1.png?raw=true "Figure 1 - Mail app not about a project")
In the email above (here we're using the Outlook desktop client) the normal action bar is showing the various Office Apps that have been installed by your Administrator or the User.

####Example of an Email – triggered####
**Figure 2 -Mail app about a project**
![Figure 2 - Mail app not about a project](https://github.com/cicorias/ProjectUnite/blob/master/img/2.png?raw=true "Figure 1 - Mail app not about a project")
####Mail App – Opened####
**Figure 3 - Mail App opened and ready for action**
![Figure 3 - Mail App opened and ready for action](https://github.com/cicorias/ProjectUnite/blob/master/img/3.png?raw=true "Mail App opened and ready for action")

***Also Working in Browser – Office Web App (OWA)***
***Figure 4 - App activated in Browser OWA***
![Figure 4 - App activated in Browser OWA](https://github.com/cicorias/ProjectUnite/blob/master/img/4.png?raw=true "Figure 4 - App activated in Browser OWA")


##Running this in your Tenant##
If you desire, you can add this to your Outlook client by adding the app.
1.	Navigate to https://rtmailapp.azurewebsites.net/ 
This is a demo site that provides the backing HTML based application utilized by the Office App. For this demo it does very little and just shows the Outlook integration. There is no updates performed and only entity recognition of the words “project | opportunity” within the email item Subject or Body.
2.	Copy the Link to Manifest
Once on that page, copy the shortcut shown on the page; it should be https://rtmailapp.azurewebsites.net/AppManifest/ProjectUniteMailAppManifest.xml 
If you deploy to your own Site a different host name will be used. Note that this MUST be HTTPS. Using Azure Web Apps ensures that HTTPS is supported using the wildcard certificate “*.azurewebsites.net”.
3.	Open “Manage Apps” from OWA
***Figure 5 - Mange Apps in OWA***
![Figure 5 - Mange Apps in OWA](https://github.com/cicorias/ProjectUnite/blob/master/img/5.png?raw=true "Figure 5 - Mange Apps in OWA")
4.	Click on the ‘+’ 
***Figure 6 - Adding an App with a URL***
![Figure 6 - Adding an App with a URL](https://github.com/cicorias/ProjectUnite/blob/master/img/6.png?raw=true "Figure 6 - Adding an App with a URL")
5.	Choose ‘Add from URL’
When Presented with the Entry form, paste in the URL from above; if using the sample here: https://rtmailapp.azurewebsites.net/AppManifest/ProjectUniteMailAppManifest.xml
Then click “Next”, then accept the “warning” regarding the app NOT being verified and NOT from the Office Store by clicking “Install”.  When it’s done, click OK.

###List of Mail Apps###
 
***Figure 7 - App shown in the Manage App list***
![Figure 7 - App shown in the Manage App list](https://github.com/cicorias/ProjectUnite/blob/master/img/7.png?raw=true "Figure 7 - App shown in the Manage App list")
Once you’re done adding, the app should show in the list “Manage Apps” as above. Note the information on the right side regarding what is read from the XML manifest provided before. 

###Overview of the Solution###
####High Level Deployment####
 
***Figure 8 - High level deployment***
![Figure 8 - High level deploymen](https://github.com/cicorias/ProjectUnite/blob/master/img/8.png?raw=true "Figure 8 - High level deploymen")
####Application Components####
#####Client#####
The client is a form of Outlook – either the Outlook Client, or the browser or mobile based client that runs cross Browser and Device.
#####Azure Web App#####
The Azure Web App (can be any Web Site or technology such as ASP.NET, PHP, NodeJS) provides the static content and the interactive JavaScript that runs in the context of the Client.

In addition, for any further interactivity, the Web App could also provide update capabilities that any website generally can provide.

The Web App utilized here uses ASP.NET 4.5 for the base site, although no MVC Controllers are utilized. Only static pages are used in this solution; however, you are not restricted.

The page interactivity is basic JavaScript and AngularJS, along with Bootstrap for the presentation tier.
####Deployment Approaches####
#####Development#####
During development, you simply hit F5 – this will deploy the “manifest” to an Office 365 Exchange Tenant – the following dialog box will appear. You will require permissions to deploy this to your Email account.  You can obtain a Trial Tenant from MSDN subscriptions if you wish to isolate (recommended) from your production email.
***Figure 9 - Visual Studio Office Tools Authentication***
![Figure 9 - Visual Studio Office Tools Authentication](https://github.com/cicorias/ProjectUnite/blob/master/img/9.png?raw=true "Figure 9 - Visual Studio Office Tools Authentication")
#####Production#####
There are 3 ways to deploy, the first 2 are considered un-trusted as they bypass the Office Store validation process.
1.	Via URL – which this sample uses
2.	Via File – which is generally the same as URL, just using a local file
3.	Via Office Store – this requires a publishing process and will make the application available for other Office 365 Tenants and Users to install.
##Code Artifacts##
The code is published here: https://github.com/cicorias/ProjectUnite
##Required Tooling##
The tools required to run the sample are:
1.	Visual Studio 2013 or Visual Studio 2015
2.	Microsoft Office Developer Tools for Visual Studio 2013 – April 2015 Update
***Not needed if using Visual Studio 2015 RC (not the Previews)***
The following shows installation of the tools using Web Platform Installer which can be obtained from: http://www.microsoft.com/web/downloads/platform.aspx  (or http://go.microsoft.com/fwlink/?LinkId=255386 ). 

***Figure 10 - Web Platform Installer***
![Figure 10 - Web Platform Installer](https://github.com/cicorias/ProjectUnite/blob/master/img/10.png?raw=true "Figure 10 - Web Platform Installer")
##Opportunities for Reuse##
There has been significant interest from various customers related to collaboration tools and applications that surround the Office 365 ecosystem. The base example presented here can be used to bootstrap an effort and initiate conversations around what is possible to facilitate collaboration experiences and productivity enhancements as users spend a significant portion of their day within an email application.
##Follow up##
Rallyteam is continuing to evaluate Office Mail Apps and looking at additionally providing contextual recognition beyond the simple Regular Expressions that are provided in this sample. By increasing the permission levels of the Applications, it is possible to inspect a mail item deeper and use custom back-end services, provided by the Application and not Office 365, to enrich the experience. This capability requires greater trust level and permissions, but is possible through use of the Office 365 services that allow interaction within a user’s email item, their mailbox, or other O365 Services.
##Links and References##
Office Development Center: [http://dev.office.com/](http://dev.office.com/ "Office Development Center")
Apps for Office Overview: [https://msdn.microsoft.com/en-us/library/office/jj220060(v=office.15).aspx](https://msdn.microsoft.com/en-us/library/office/jj220060(v=office.15).aspx "Apps for Office Overview")
Creating a Mail App with Visual Studio: [https://msdn.microsoft.com/en-us/library/](https://msdn.microsoft.com/en-us/library/ "Creating a Mail App with Visual Studio")a1b11750-7476-477d-9243-56ff145a0e3c
Creating a Mail App with Napa (Monaco – what “code.visualstudio.com” was built with): [https://msdn.microsoft.com/EN-US/library/office/jj220072.aspx](https://msdn.microsoft.com/EN-US/library/office/jj220072.aspx "Creating a Mail App with Napa (Monaco)") 
