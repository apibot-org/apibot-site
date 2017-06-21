+++
description = "Description of the HTTP Request Node"
title = "HTTP Request Node"
date = "2017-05-18T17:08:08+01:00"
draft = false
weight = 40
bref="The HTTP Request Node helps do the HTTP Request protocol"
toc = true
+++

## Definition ##
The HTTP Request node define a function in the global namespace that provides the HTTP request protocol implementation. The function requires an endpoint *u*, and a method *m*, other optional parameters such as a body *b* and a list of variables corresponding to the headers *(n0,h0), (n1,h1), ... ,(nk,hk)* can be added. 

```
f: f -> HTTP Request
```
### Parameter ###

#### Required Parameters ####
The required parameter are the endpoint(or URL) where the HTTP request service will be called and the type of method.  
Parameter | Description
--- | ---
endpoint | The URL where the HTTP call is made
method | The HTTP Method when doing the request

#### Optional Parameters ####
Parameter | Description
--- | ---
(n1, h1) | n1: correspond to the name of the first header. <br> h1: correspond to the value assign to the header h1.
body | is the HTTP Message body. The content-type header must be added if the body is added.  


## Tutorial ##
### Introduction ###
You use the HTTP Request node to implement the HTTP Request protocol on your graph. We are assuming that you understand the protocol.  
The HTTP Request node consists of three parameters which are the following:

* Name, the name of the node
* URL, the endpoint to make the request
* Method, the HTTP method, to indicate the desired action to be performed on the identified resource, is usually GET or POST. 

As shown on the figure below, implementing the endpoint to get the user_timeline on twitter.

{{<figure src="/img/docs/get-user-timeline.png" caption="User Timeline">}}   

If the request need a message body, a content-type header must be added, so the body text area shows up.  
To insert headers on the request, you should click on **add new header**, as shown on the image below. 

{{<figure src="/img/docs/http-request-twitter oauth2.png" caption="HTTP Request node">}} 