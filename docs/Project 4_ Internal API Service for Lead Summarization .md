## **Project 4– Internal API Service for Lead Summarization**

### **Last Summer: LeadLens**

* [backend repo](https://github.com/meganfung38/Summary_Extension_Backend/blob/main/README.md) \+ [frontend repo](https://github.com/meganfung38/Summary_Extension_Frontend)

### **Internal Lead Summarizer API** 

* Internal RESTful API service that receives a SFDC Lead ID as input and returns AI generated lead summaries, sales talking points, and contextual data   
* Designed to replicate \+ enhance the functionality of LeadLens (built: Summer 2024\)  
* Output enables internal tools to quickly surface lead insights for sales representatives

### **Problem Statement** 

* Current LeadLens is limited to frontend browser usage (via chrome extension) and specific user contexts  
* Internal tools– internal enablement dashboards, sales intelligence hubs, assistant tools) cannot easily access lead summarization logic   
* There is a need for centralized, reusable API that other internal systems can call using the SFDC Lead ID

### **Solution** 

* Build a backend API service that receives an SFDC Lead ID and returns structured, AI drive sales context   
  * Modular, scalable, and easily consumable by other internal teams   
* Steps:  
1. Chrome Extension Review   
* Audit last summer’s extension logic \+ prompts   
* Identify reusable code and patterns for backend transformation   
2. Design API Interface   
* Define JSON schemas for input/output   
* Decide endpoint granularity   
3. Data Integration Layer   
* Connect to SFDC API   
* Query relevant objects  
4. AI Logic layer   
* Construct prompts and data pipeline to generate:   
  * Product interest inference   
  * Sales hook   
  * Condensed summaries of complex records  
5. Internal Tool Integration   
* Create documentation for usage \+ interaction with API 

### **API Structure** 

* Input  
  * LEAD\_ID (string): unique SFDC Lead ID   
* Output   
  * GENERAL\_INFO: name, company, email, phone, status, title, segment, SM employee size, etc   
  * PRODUCT\_INTEREST: which RC product(s) this lead is most likely interested in   
  * WHERE\_AND\_WHY: where the lead entered the system and why they are a lead   
  * HISTORICAL\_RELATIONSHIP: duplicate history, past campaign involvement, prior opportunities   
  * SALES\_ENABLEMENT\_HOOK: a customized talking point 

\*\*endpoints require: {“lead\_id”: “\<SFDC\_ID\>”} as body

| Endpoint  | Method  | Description  |
| :---- | :---- | :---- |
| /summarize/lead | *POST* | Returns a full summary object for a given SFDC Lead ID  |
| /summarize/general-info | *POST* | Returns just the general lead metadata  |
| /summarize/product-interest | *POST* | Returns inferred product interest |
| /summarize/where-why | *POST* | Explains how and why the lead entered the system  |
| /summarize/history | *POST* | Returns relevant campaign/ opportunity history  |
| /summarize/hook  | *POST* | Returns a sales enablement pitch based on the above |

  