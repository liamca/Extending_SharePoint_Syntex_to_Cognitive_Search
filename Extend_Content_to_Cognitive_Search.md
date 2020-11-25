# Extend Content to Azure Cognitive Search

This section will explain how to extend the knowledge extracted through SharePoint Syntex to Azure Cognitive Search. This service will power a subsequent custom seach application that will allow users to effectively search and explore this content.

## Prerequisites
Before you begin, you must have the following:

- An Azure account with an active subscription. Create an [account for free](https://azure.microsoft.com/free/).
- An Azure Cognitive Search service. [Create a service](https://docs.microsoft.com/en-us/azure/search/search-create-service-portal) or find an [existing service](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices) under your current subscription. You can use a free service for this quickstart.
- Azure Logic Apps instance

## Create the Cognitive Search Index
We first need to create a search index in your Cognitive Search service.  To this, open your search service in the Azure Portal.  From there choose “Add Index” and enter the following settings.  
 
Choose “Create” to add the empty index.
Create a Logic App to Synchronize Data
Next, we will add a logic app to allow the data to be synchronized from SharePoint to Cognitive Search.  To do this open your Azure Logic App from that Azure Portal.  
- From the “Logic App Designer” add a “New Step”
- Choose the SharePoint step “When a file is classified by a content understanding model”
- Enter your Site Address (using your Administrative user / password)
- Enter your Documents Library
- Set the interval to be 3 Minutes
 
Add another “New Step” and choose “HTTP” with the following settings:
- Method: POST
- URL with your search service name: https://[YOUR_SEARCH_SERVICE].search.windows.net/indexes/contoso/docs/index?api-version=2020-06-30
- Headers:
  - api-key: Your Cognitive Search Admin API Key
  - Content-Type: application/json
- Body: 

```json
{
  "value": [
    {
      "@@search.action": "mergeOrUpload",
      "classification": @{triggerBody()?['{ContentType}']?['Name']},
      "createdBy": @{triggerBody()?['Author']?['DisplayName']},
      "fullPath": @{triggerBody()?['{FullPath}']},
      "id": @{string(triggerBody()?['ID'])},
      "insuranceProvider": @{triggerBody()?['Insurance_x0020_Provider']},
      "keyPoints": @{triggerBody()?['MediaServiceKeyPoints']},
      "modifiedBy": @{triggerBody()?['Editor']?['DisplayName']},
      "name": @{triggerBody()?['{Name}']},
      "thumbnail": @{triggerBody()?['{Thumbnail}']?['Medium']}
    }
  ]
}
```


Choose “Save”
Add Content to SharePoint
Now that everything is configured, we can add some content to be classified and enriched by Syntex.  To do this, go to your Contoso site and upload the files located in the “Document Understanding Example Files” folder to your Documents library.
NOTE: If you already had these files in the library you will want to first delete them so that Syntex will apply the model.
It might take some time (10+ min), however, you should be able to go to the Overview blade in your Logic App to monitor the progress.  When completed, you should see successful status in the Run History.
 
At this point open your Cognitive Search service in the Azure Portal and choose “Search Explorer”.  Choose “Search” to ensure the data exists in the search index.
Create a Search Enabled Application
From the “Search Explorer”, choose “Create Demo App”.
- If asked, choose to “Enable CORS”
- Thumbnail: thumbnail
- Title: name
- Description: keyPoints
 
Delete all the “sidebar” items other than modifiedBy, CreatedBy, insuranceProvider and classification.
 
Create and download the Demo App





