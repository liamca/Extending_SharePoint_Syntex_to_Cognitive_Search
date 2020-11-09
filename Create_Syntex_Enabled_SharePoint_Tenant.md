# Creating a Demo Microsoft 365 Tenant

NOTE: This step is only required if you do not already have a Syntex enabled SharePoint tenant.

To get started, we will create a SharePoint tenant to host the content that will be enriched using Syntex.  To do this, visit https://cdx.transform.microsoft.com/my-tenants and choose “Create Tenant”.  Choose your tenant location and pick the “Microsoft 365 Enterprise with Users and No Content”.

![Create tenant](https://github.com/liamca/Extending_SharePoint_Syntex_to_Cognitive_Search/raw/main/images/create_tenant_01.png)
Make note of the Admin name and password.
![Create tenant](https://github.com/liamca/Extending_SharePoint_Syntex_to_Cognitive_Search/raw/main/images/create_tenant_02.png)
 
Go back to your tenant list, and copy the link to your “Admin Portal” and make note of your tenant name.  

##Add a Trial for Syntex

Syntex is an add on to SharePoint and needs to be enabled.  To do so, go to this admin link and log in as the admin.  It is recommended that you use a separate browser or “InPrivate” to avoid conflicts with your Microsoft credentials.
Choose “Purchase Services” and locate and click on “Add-Ons” in the bottom of the page.

Choose “Details” for “SharePoint Syntax Trial” and choose “Get Free Trial” and continue with the order of this trial.

![Create tenant](https://github.com/liamca/Extending_SharePoint_Syntex_to_Cognitive_Search/raw/main/images/create_tenant_03.png)
 
Please note, it could take a little time for this option to be enabled.

## Enable Syntex in your Teams Site
Now that we have a content center, we need to define which SharePoint sites can use it.  We will apply this to the Contoso site that came with the installation of the tenant.  To do this, open the Microsoft 365 Admin Center (https://admin.microsoft.com/Adminportal/Home?#/homepage) and choose “Setup”/
Choose “Automate content understanding” and choose “Get Started”
![Create tenant](https://github.com/liamca/Extending_SharePoint_Syntex_to_Cognitive_Search/raw/main/images/create_tenant_04.png)

Choose: “Only libraries in selected sites” and choose existing “Contoso” site
![Create tenant](https://github.com/liamca/Extending_SharePoint_Syntex_to_Cognitive_Search/raw/main/images/create_tenant_05.png)

In the next page enter “Contoso Content Center” as the content center name.
Complete the steps to activate Syntex – AI Builder
At this point you can go to the Contoso SharePoint site and choose the “Documents” folder.  From here you should see the option to leverage the AI Builder under the “Automate” menu item:

## Create an AI Model
At this point you now have a Syntex enabled SharePoint tenant.  In the next steps you will need to choose at least one of the below options to create AI enabled models to extract knowledge from content.  This can be done by:
1)	Applying a Document Understanding Model:  Follow the content found in “GA-HOL-Creating_and_Applying_a_Document_Understanding_Model_to_a_Library.docx”, you can choose to create models that allow you to perform tasks such as classification of content and entity extraction.  You can skip directly to the section “Build Your Classifier Model” using the Content Center created in the previous step.  For the library, you can choose to use the “Contoso” site that has already been created.
2)	Applying a Forms Processing Model:  Follow the content found in “GA-HOL-Creating_and_Applying_a_Forms_Processing_Model_to_a_Library.docx”, you can configure a model to extract information from forms.


