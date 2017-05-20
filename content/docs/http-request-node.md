+++
description = "Description of the HTTP Request Node"
title = "HTTP Request Node"
date = "2017-05-18T17:08:08+01:00"
draft = false
weight = 40
bref="The HTTP Request Node helps do the HTTP Request protocol"
toc = true
+++

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