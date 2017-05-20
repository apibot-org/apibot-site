+++
description = "Quickstart guide using Twitter API"
title = "Quick start"
date = "2017-05-15T22:35:08+01:00"
draft = false
weight = 10
bref="With Apibot you will save time allowing you to expend it on more valuable activities. We will be showing how Apibot works making you more efficient with your API integration test"
toc = true
+++

For this guide, it is necessary to have a Twitter developer account, for more information, please check Twitter developer documentation. 

### Getting the Bearer Token from Twitter ###
We will be applying Twitter documentation regarding [Application-only Authentication](https://dev.twitter.com/oauth/application-only). 

First, we will create a new scenario (graph) by pressing the button **new graph** on the menu bar top of the screen.  If you would like, add a title and a description of your scenario. We should leave the executable box as uncheck, because the scenario is still incomplete. 

{{<figure src="/img/docs/new-graph.png" caption="Creating an Scenario on Apibot">}} 

Next, we will need to add the scope variables, which are, the global variables on our scenario. The node that we use for this is the **config node**, where we insert these variables. To add the node, go to the left pane and select the **config node** then click **add**. It would add the config node on the scren, then select it on the screen, and press the **Add new property**, where we will enter the global variables, which are:

*   Consumer Key: Given by Twitter for your application
*   Consumer Secret: Given by Twitter for your application
*   URL: https://api.twitter.com

{{<figure src="/img/docs/configuration-node.png" caption="Configuration node">}} 

After having the scope variables, is necessary to encode the consumer key and secret. We will concatenate both variables and assigned it to a new variable call **auth** on the scope. For this we will be using, the **JS Eval node**, useful to apply logic on our scenario. We insert the JS Eval node, as has been done on previous nodes, then we include a name for the node (e.g., "Set Auth"), and insert the following code on the function text area:

    (scope)=>{ 
    var auth = btoa(scope.key+":"+scope.secret);
    scope.auth = "Basic" + auth;
    }

You must connect the configuration node to the JS Eval Node, unsing an arrow. 

{{<figure src="/img/docs/js-eval-node.png" caption="JS Eval node">}} 

The next step is to obtain the bearer token. As explained on Twitter:

>   The value calculated in step 1 must be exchanged for a bearer token by issuing a request to POST oauth2 / token:

>*   The request must be a HTTP POST request.
>*   The request must include an Authorization header with the value of Basic <base64 encoded value from step 1>.
>*   The request must include a Content-Type header with the value of application/x-www-form-urlencoded;charset=UTF-8.
>*   The body of the request must be grant_type=client_credentials.

Therefore, you add a **HTTP Request Node** on the scenario, and connect it to the JS Eval Node, with the following parameters:

*   **Name:** *any name (e.g., /oauth2/token)*. How you would like to call your node
*   **URL:** *$(URL)/oauth2/token*. Endpoint for the HTTP request, we are using the scope variable $(URL) that you created on the config node
*   **Method:** *POST*. HTTP request type, in this case, is POST

To include the grant_type on the body, you should add the header content-type, and then the authorization and accept headers. Click on **add new header**, and add: 

*   **content-type:** *application/x-www-form-urlencoded;charset=UTF-8*
*   **authorization:** *$(auth)*. Using the scope variable that we transform on the JS Eval Node
*   **accept:** *application/json*. The response type

{{<figure src="/img/docs/http-request-twitter oauth2.png" caption="HTTP Request node">}} 

Now we should have the bearer token, to confirm that the process was successful, you could use a **assert status node**. Insert a **assert status node** from the node templates, and fill the fields

*   **Status from:** *200*. The response status minimum accepted value
*   **Status to:** *200*. The response status maximum accepted value

{{<figure src="/img/docs/assert-status-twitter-oauth2.png" caption="Assert Status">}} 

By now we could execute the graph, but before doing that, we are going to extract the bearer token and assign it to a variable for later use.
Therefore, we will add a **Extract Body node**, with the following parameters:

*   **Property Name:** *token*, 
*   **Function**:

        (body) =>{
        return "Bearer" + body.access_token;
        }

{{<figure src="/img/docs/extract-token-twitter-oauth2.png" caption="Extract Token">}} 

Now we could execute the scenario and see the results. The graph must be executable (remember from *new graph* description). You could do this by pressing on the editor and on the right pane check executable. 
{{<figure src="/img/docs/results-bearer-token-oauth2.png" caption="Results Token">}} 

### Authenticate API Requests with the Bearer Token ###
Now we will show you one of the functionalities that make Apibot unique and best in its class.

Create a new graph, go to the left pane and select the previous graph (we called it *Twitter Bearer Token*) click on add, it will show up on our new graph screen 

{{<figure src="/img/docs/previous-graph-twitter-oauth2.png" caption="Previous Graph">}} 

We will be using the endpoint to ask for a user timeline. Consequently, you should add a HTTP Request node, connect it with an arrow from our previous graph, and fill the parameters

*   URL: $(url)/1.1/statuses/user_timeline.json?count=100&screen_name=twitterapi
*   Method: GET

Now you should be able to execute the API Requests

{{<figure src="/img/docs/get-user-timeline.png" caption="User Timeline">}} 