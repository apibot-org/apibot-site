+++
description = "Description of the Extract Body Node"
title = "Extract Body Node"
date = "2017-05-21T12:24:08+01:00"
draft = false
weight = 80
bref="The Extract Body node helps you to apply logic to the body of a HTTP Request/Response"
toc = true
+++

### Introduction ###
The Extract Body node allow us to apply logic to the body of an HTTP Request/Response. This node has three parameters which are:

* Name, label to assign a name for the node
* Property Name, the variable that gets assigned the function return value
* Function, where you define a function in the global namespace which takes the last request's body as argument and returns a value.  

In the example below, we will be using the twitter example (presented on the quickstart).  
We are going to extract the bearer token, by calling the body.access_token and assign it to a variable for later use.
Therefore, we will add a **Extract Body node**, with the following parameters:

* name: any name
* Property Name: token, 
* Function:

        (body) =>{
        return "Bearer" + body.access_token;
        }

{{<figure src="/img/docs/extract-token-twitter-oauth2.png" caption="Extract Token">}} 

Now the token variable could be used later on the scenario. For example we create a new graph, where we will be calling the Twitter Bearer Token, that includes, the token variable. We will be using the endpoint to ask for a user timeline. Consequently, you should add a HTTP Request node, connect it with an arrow from our previous graph, and fill the parameters

*   URL: $(url)/1.1/statuses/user_timeline.json?count=100&screen_name=twitterapi
*   Method: GET

And add a new header:

* authorization: $(token), using the previous variable created on the Extract Body node.

Now you should be able to execute the API Requests

{{<figure src="/img/docs/get-user-timeline.png" caption="User Timeline">}}  
