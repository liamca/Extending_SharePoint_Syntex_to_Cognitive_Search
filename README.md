# Search Enabled LOB Apps using Syntex and Cognitive Search
## Overview
SharePoint Syntex, the first product from Project Cortex, has shown to be an incredibly powerful tool to enable organizations to easily transform content into knowledge.  This has been enabled through machine teaching which accelerates the extraction of valuable information as metadata from content within SharePoint.
Microsoft 365 has long offered the ability to effectively search over enterprise content.  However, there are cases where organizations will require additional customization of their search application that are not targets for SharePoint.  A few examples of this could include:
- A unique user experience that leverages interfaces such as a geospatial search.
- Leveraging knowledge and data relationships extracted from content.
- Integration of content from other data sources into the search experience
- Scale to high query rates

Azure Cognitive Search enables organizations to create these types of rich custom applications through a fully managed platform which makes extending SharePoint Syntex enriched content to Cognitive Search an excellent option for these use cases.

This document explains how to create a customer ready demo that extends SharePoint Syntex enriched content to Cognitive Search.  

## Requirements

- SharePoint Tenant with Syntex enabled (instructions below on how to do this)
- An Azure account with an active subscription. Create an [account for free](https://azure.microsoft.com/free/).
- An Azure Cognitive Search service. [Create a service](https://docs.microsoft.com/en-us/azure/search/search-create-service-portal) or find an [existing service](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices) under your current subscription. You can use a free service for this tutorial.
- Azure Logic Apps instance

## Steps

- [Step 1: Create and Apply Document Understanding](https://github.com/liamca/Extending_SharePoint_Syntex_to_Cognitive_Search/blob/main/Create_and_Apply_Doc_Understanding.md)
- [Step 2: Extend SharePoint Content to Cognitive Search](https://github.com/liamca/Extending_SharePoint_Syntex_to_Cognitive_Search/blob/main/Extend_Content_to_Cognitive_Search.md)

## Optional: 
- [Create and Apply Forms Understanding](https://github.com/liamca/Extending_SharePoint_Syntex_to_Cognitive_Search/blob/main/Create_and_Apply_Forms_Understanding.md)
