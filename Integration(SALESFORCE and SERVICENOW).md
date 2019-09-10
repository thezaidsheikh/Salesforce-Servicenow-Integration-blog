# Integration of SalesForce with ServiceNow

We want to create an Customer Account in ServiceNow when any customer is created in SalesForce. 

So, we required Access Token of our ServiceNow Instance. 

We will also see How to get our SalesForce Access Token ? 

***
#### SERVICENOW ACCESS TOKEN 
    Goto application navigator and type System OAuth. 

    Now goto Application Registry and create a record in it. 

    Name your Application Registry and increase the life span of your Access Token by increasing the number according to your need. 

    Save it and you will get your instance Client_ID and Client_Secret_ID. 
    Now go to Postman and take http method as POST and enter the url :- https://your_id.service-now.com/oauth_token.do 

    And give the body like :- 

    grant_type: password 

    client_id: your_client_ID 

    client_secret: your_client_secret_ID 

    username: admin 

    password: your_servicenow_password 

    Now hit Send and you will get the access_token and refresh_token . 
    Now go to your SalesForce Account and click on your profile and then click on console. 

    Here you will be redirected to the console page where you have to write your code to insert the customer record to the ServiceNow customer account. 
