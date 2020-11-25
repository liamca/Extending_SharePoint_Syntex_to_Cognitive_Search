# CREATING & APPLYING A DOCUMENT UNDERSTANDING MODEL

Project Cortex provides us the ability to leverage AI tech to automate the classification of files and the extraction of specified metadata for files hosted in SharePoint libraries. For unstructured documents where the text entities you want to extract reside in sentences or specific regions of the document (i.e., letters or contracts), Project Cortex allows you to build a model using a machine learning-based service (LUIS) that can designate both the type of file it is (its classification) and specify the contents of the document you wish to extract (its extractors). This set of models is preserved as a special content type in SharePoint – and can be subsequently published to other libraries in one’s tenant. Like the AI Builder form processing model, the service will write out the extracted file values to library fields at runtime. 
Objective: the purpose of this guided exercise is to understand how to build and apply a document understanding model (including the classifier and one extractor), how to create the three types of explanations, how to test your model on similar unlabeled documents to evaluate model fitness, and how to apply the model to one or more libraries so it can process files at runtime.

## CREATE A CONTENT CENTER & PREPARE A TRAINING SET
- You are going to need a content center and a document library to publish the completed model to. This library can reside in the content center or elsewhere in the same tenant.
- The content center is a new site template in Project Cortex – initially serving as a location for the creation and management of these AI apps, but it will eventually include additional features and capabilities. This site template is not available in self-service and must be created by a SharePoint or Project Cortex admin in the admin center. You can find the template in the Other options template menu. Create a content center, with any name you prefer. Remember to grant access to the users who will be creating the models.
- Creating a model requires a set of example files to train (and test) on. You will need about 5-25 DOCX or PDF files of similar type and layout, but with different values for the information you wish to extract. This set also needs to include 1-3 negative examples (files of what the trained file is not; the model uses these negative examples to improve its accuracy). You can apply these exercises to your own files, but for illustrating the concepts and steps in this lab, we will use the Contoso Electronics benefits contracts example set. These 14 files (twelve examples and two negative examples) are available in the Product Support > Contoso Electronics HOL Files > Document Understanding Example Files folder. Upload your example set either directly to the training files library or to a folder (in case you want to reuse with a different model).

## BUILD YOUR CLASSIFIER MODEL
- Navigate to the model library of your content center and from the ribbon, select + Create a model 
- This will open the “New model” panel where you can associate a model to an existing content type or create a new one. For this exercise we will create a new model named Benefits Change
- The model file will be created in the model library, the content type will be created (currently as a site content type) and you will be redirected to the “model home page”

## ADD FILES
- Notice that all the action tiles are grayed out except one, Add from library. Your first step is to select a set of example files. Note: these same files should be used for both the classifier and extractor training. You always have the option to add more, but typically you can add a full set of example files, label some to train your model, and test the remaining unlabeled ones to evaluate model fitness. 
- Click the Add button, select all your example files and add to your model. They will appear in the Example files for training section.
CREATE INSURANCE PROVIDER ENTITY EXTRACTOR & LABEL EXAMPLES
- Notice that once the example files are added the Create new entity extractor and Label examples tiles are enabled. You can start by either training your classifier (Label examples) or creating and training an extractor (Create a new entity extractor). Extractors are used by the AI as explanations to understand the document classification, and since one explanation is needed for each classifier or extractor you train, it is a helpful strategy to start with an extractor.
- Click the Create new button in the Create new entity extractor tile or select “+ New entity extractor” in the Entity extractor section below. 
- Create a new extractor named Insurance Provider 
- The first document in your sample set will be displayed in the viewer in plain text view; the full list of added example files is displayed in the labeled examples section. NOTE: you can render the formatted view of a document by selecting View original link. If you are displaying “Contract_Change_VanArsdel_1” label the insurance provider name Adatum Corporation by highlighting it. If you select too little or too much text, just select the highlighted selection to clear it and try again.
- When the string is correctly highlighted select Next file  to submit the labeled file and advance to the next one. You can optionally select Submit label link, but it will stay on the currently displayed document.
- Once you advance or click to the next file, it will be displayed in the viewer and the label you applied to the previous file will be displayed in the “Labeled examples” section.
- Continue labeling 4-6 of your example files. For a negative sample, instead of labeling, toggle the “No label found” option and submit the file. Once you have labeled five files a notification banner will display informing you to move to training. You can label more documents or advance to training.

## TRAIN INSURANCE PROVIDER ENTITY EXTRACTOR
- The training phase is where you add explanations to help the model understand how to classify your document or how to identify the information you want to extract. The first labeled file will be displayed and you will be prompted to add an explanation. At least one is required before the model can be trained. NOTE: only the example files that you label in the previous phase are displayed, with a status of not trained.
- For an entity extractor, explanations can be hints about the label format itself or strings around the label to help identify it. To identify the Insurance Provider we will create two phrase list explanations, one before the label and one after. Select “Add explanation” from the coach mark or +New from the ribbon and create an explanation named “String before”
- Select the type Phrase list and in the text box type or copy the preceding part of the sentence “network participation with your insurance provider” and save. NOTE: case sensitivity should be toggled off.
- Once this first explanation is saved, we will automatically train the model. The training results will be displayed in the “Trained files” section, showing both the predicted label value and the evaluation. A match means the model is correctly predicting your label, a mismatch means that just that; it’s not correctly predicting the label for that file. You can look in the “Prediction” column or load the file into the viewer to see the mismatch. In our case, notice that in the “Contract_Change_VanArsdel_2” example file it is only partially predicting “Best For” for the insurance provider “Best For Your Organics Company”
- To correct, let’s add another explanation. Create another phrase list explanation named “String after” and in the text box type or copy the phrase portion that follows the entity name “(http://www.” and save. NOTE: case sensitivity should be toggled off.
- We will initiate retraining once the new explanation is saved. Notice that now the mismatch is fixed for that file. The additional explanation helped the model to understand the variety of insurance provider names and correctly predicted this longer name. 
- You can further test the fitness of your model by selecting the “Test” tab and seeing how well the model predicts the insurance provider value in the other unlabeled files in your example set.
- OPTIONAL: if there were still issues or for even more accuracy a third explanation could be created using the other two previously created ones. Create a proximity explanation named “Provider name range” and first select the “String before” explanation followed by the “String after” explanation with a token range of 1 to 5. A token is a continuous span of letters and/or numbers with no spaces on punctuation. A space is *not* a token. Since most of our insurance provider’s names are around 1-5 tokens in length this explanation would help the model understand how close the two other explanations should be in relation to each other in a file.
- Now that your Insurance Provider entity extractor is trained and accurately predicting labels you can exit this training and return to the model home page. 

## TRAIN BENEFITS CHANGE CLASSIFIER
- In the “Classifier” section of the model page, notice that your classifier, Benefits Change, has no accuracy score (because it hasn’t been trained yet) and two or three explanations (as it can use the explanations you created for the Insurance Provider entity extractor. Select the classifier to go to the label page.
- Like the entity extractor experience, the first labeled document in your example set will be displayed in the viewer; the list of files and their labels are displayed in the “Labeled examples” section on the left. 
- In this training you are effectively labeling the entire document as either a positive or negative example of the content type. Answer the question in the viewer ribbon “Yes” or “No” for that displayed document. Making a selection will submit the answer, label the document as “Positive” or “Negative” and advance the viewer to the next example file. NOTE: you must submit at least one negative example before you can proceed to the next step.
- Once you have labeled five files a notification banner will display informing you to move to training. You can label more documents or advance to training
- The service will train on the labeled set immediately since you already provided explanations when you trained the Insurance Provider entity extractor. If you had started with training the classifier and had no explanations you’d go through a process like the one above, providing an explanation with a string that can be used to identity the file as that class of documents.
- You will now see that all of you trained and labeled files show a status of Match. You can select any one to see the viewed file highlighted in green. If there was a mismatch, the file would show in red and you could remediate by either labeling more files or adding more explanations.

## OPTIONAL: CREATE & TRAIN INSURANCE CHANGE DATE ENTITY EXTRACTOR
Creating this extractor illustrates using a pattern explanation on a date entity in the example files
- Under Entity extractors section of the model page select +New entity extractor 
- Create a new extractor Insurance Change Date 
- Click on the newly created Insurance Change Date entity extractor
- Label the insurance change date, “10/7/2019” in the second paragraph by highlighting it. If you select too little or too much text, just select the highlighted selection to clear it and try again.
- When the string is correctly highlighted select Next file  to submit the labeled file
- The next file in your sample set will be displayed; the label will show up for the previously viewed file in the right.
- Continue labeling 4-6 of your example files. For a negative sample, instead of labeling, toggle the “No label found” option and submit the file. Once you have labeled five files a notification banner will display informing you to move to training. You can label more documents or advance to training.
- For this extractor we are going to use an explanation that provides a hint about the entity format itself and variations it may have in the example documents. To identify the Insurance Change Date we will create a pattern explanation named “Change Date”.
- For this explanation we need to supply the date variations as they appear in the example files. Since these are largely the same – with a one or two digit day, a one or two digit month, and a four digit year, your pattern set will look something like: 
  - 0/0/0000
  - 0/00/0000
  - 00/0/0000
  - 00/00/0000
  
- Select “Ignore digit identity” (as you are just explaining the pattern) and select save.
- You will notice that this explanation alone is insufficient for the model to find the date. Add a phrase explanation like you did in the previous entity extractor, using the preceding string “As of” or the subsequent string “, our status with the” (yes, including the comma that immediately follows the date!).
- Notice that once one of these phrase list explanations are added the model can successfully predict the change date. You can electively check the unlabeled files in the Test stage or return to the model home page.

## APPLY MODEL TO A LIBRARY
- You are now ready to apply your model to a document library. On the model home page select “Publish model” from the tile or +Add Library link in the “Libraries with this model” section. 
- This will display a panel where you can navigate to or search for a site you have access to. Select a library and select “Add”. The library location of the applied model will now appear in the “Libraries with this model” list. 
- After publishing you can test by navigating to the library and first confirming that the model’s associated content type (and its columns) have been added (and that a content type view has been created). You can then upload documents for processing.
- If a file doesn’t process for some reason – or there are existing files in the library that you would like to process using the model, you can select them and select the “> Run model” action in the library ribbon.
