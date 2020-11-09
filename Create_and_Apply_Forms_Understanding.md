# CREATING & APPLYING A FORM PROCESSING MODEL

One of the new capabilities Project Cortex provides is the ability to leverage AI tech to automate the classification of files and the extraction of specified metadata for files hosted in SharePoint libraries. For semi-structured files where you have clear key-value pairs or table data (like forms or invoices) – Project Cortex allows you to build a model using the new Power Platform AI Builder service, and then publishing that model to a SharePoint library and write out the extracted file values to library fields at runtime. 
Objective: the purpose of this guided exercise is to understand how to build and apply an AI Builder model to a SharePoint library to automate the extraction of file metadata. It will also illustrate updates to assign a content type to a model and to improve model fitness by training on undetected fields during model creation.

## CONFIRM A TEST LOCATION & TRAINING SET
- Be sure AI Builder is enabled in your environment. This will ensure the PowerApps default environment is configured and a CDS database is created.
- You are going to need a test site collection or library. Optionally, you can build the model and apply to a production library, but please note that the application of a model to an existing library does not currently process any existing files. 
- This model type requires a sample form set to train (and test) on. You’ll need about 5-10 input documents with a similar layout and in JPG, PNG, or PDF format (refer to requirements & limitations for more details). Optionally, you can try it out using our Contoso Electronics purchase orders sample set. These 12 PDF files are available in the Product Support > Contoso Electronics HOL Files folder.
- For a visual walk-through refer to the Content_Understanding-GA_Model_Creation_Experience_Updates_May2020 deck

## BUILD YOUR FORM PROCESSING MODEL
- Navigate to the library where you want to apply the model and from the ribbon select Automate > AI Builder > Create a form processing model 
- This will open a panel directing you to name your model. By default, a new content type is created, and its library view will become the new library default when the model is published. You can change these settings under “Advanced settings”. Select “Create”.
- TBD: You will be redirected to a dialog where you will have to provide model name again. When we release the name you used in creation panel will be passed along and you will be directed to the “add documents” page. 
- Upload at least five (5) example documents from either your local storage or a SharePoint site (we suggest keeping a few in reserve for runtime testing) 
- After the files have been uploaded, select “Analyze” 
- The analysis will show what fields have been identified from the sample set 
	Select the fields you wish to capture in your runtime
	You can rename or resize these fields
	You can also highlight to select fields not detected during analysis
	If you resize any detected fields or create new, undetected fields you will have to specify these modifications in each example document. 
- Select “Done” and on the next screen “Train” 
- Once training is complete you can view details. From this page you can also perform a quick test. 
- Publish your model 
- Select “Use”. The panel will load the PowerAutomate flow template - Start AI Builder form processing when a new file is created – you may need to confirm connections, and select “Create flow” 
- You will be redirected back to the library with the model applied – and if you elected to make the model schema the new default view, you will see form fields you selected as SharePoint columns.

## RUNTIME
- From the updated library either select upload files or drag from your local set one or more of the remaining sample files.
- You will see a notification informing you that additional processing is being performed.
- You will see the library fields populated from data in the files (it should not take more than 30-90s).
- View model details: from same ribbon action you will now see the create model action replaced with a “view form processing model details” action. If you are the owner there will a link to view or edit the model in AI Builder. If you are not an owner you will only see limited model details (including when it was published and who the owner is).
