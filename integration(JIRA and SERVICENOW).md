#####  First lets talk about What is Webhook ? 

A webhook is a user-defined callback over HTTP. You can use Jira webhooks to notify your app or web application when certain events occur in Jira. For example, you might want to alert your remote application when an issue is updated or when sprint is started. 

***
#### STEPS TO INTEGRATE JIRA (WEBHOOK) WITH SERVICENOW
    Go to your jira account. URL like :- https://your_username.atlassian.net 

    Then click setting at the bottom left of your page. 

    Now goto System, you will get the webhook at the bottom of your application navigator. 

    Create a Webhook if you have not created before. 

    Name your Webhook , write your URL (API URL for the post) that you want to call. And add the triggers on which your Webhook will run. Like on creation of an issue , edit issue etc. 

    Now save your Webhook. 

#### CREATE SCRIPTED REST SERVICES (SERVICENOW) 

    Goto application navigator and type System Web Services. 

    Now in Scripted Web Services module click on scripted rest APIs. 

    Create a record and save it. 

    Now In your record create a new resources and give HTTP method POST and name your resource . It will give you the resource path. 

    Copy that resource path and insert it on your Webhook URL that we have created before. 

    Write the script for the creation of case and placed the jira body to the related field. 

    Like short_description of case will take description of jira ,etc. 
#### Working of the above methods 

When you create an issue in your jira instance  , then your created Webhook will trigger (according to the trigger events that you have given) and call your API url (Scripted rest API resource path )that you have given. 

Now it will goto ServiceNow instance as your scripted rest API resource path is called by jira and it will run the script that you written in your API script to do. 

***

Before integrate JIRA and Servicenow completely we have to get the API token of our JIRA instance . 

Now to create a API token goto https://id.atlassian.com/manage/api-tokens 

And create a new API token , this will give you the token , now copy it and save it. 
#### CREATE OUTBOUND REST API (SERVICENOW) 

    Goto application navigator and type outboud rest . 

    In System Web Services -> Outbound -> Rest message. 

    Create a new Rest message and give it the required fields. 

    Now in the EndPoint url write the Jira rest API url  

    Like https://your_username.atlassian.net/rest/api/2/issue/ 

    Save it and in Header tab write : 

    Accept : Application/json 

    Authorization : basic your_API_Token_key (that you copied and saved) 

    Content-Type : Application/json 

    Now create HTTP methods , Name it and give http method to it and write the EndPoint url for that http method .Like for PUT give the URL like  https://your_username.atlassian.net/rest/api/3/issue/${issue_key} 

    Give Authentication as inheret from parent. 

    Now save it. And create a new HTTP method for the GET and POST. 
#### JIRA COMMENT IN SERVICENOW 

    Add the insert, update, delete comment trigger events in the Webhook that you have created earlier. 

    Create a Business Rule for the inserting a jira issue comment in your case additional comment in the case table. 

    Write a script in your BR to call the GET http method that you have created in the Outbound Rest API.
####  SERVICENOW COMMENT IN JIRA ISSUE 

    Create a BR in the case table and give it When to run : after update.

    Call the POST http method that you created in the Outbound Rest API. 

    API to POST the comment will be like - https://your_username.atlassian.net/rest/api/2/issue/${issue_key}/comment 

    And insert the servicenow additional comment into the jira coment. 
