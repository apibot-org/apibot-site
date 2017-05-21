+++
description = "Description of the Assert Header Node"
title = "Assert Header Node"
date = "2017-05-20T14:42:08+01:00"
draft = false
weight = 70
bref="The Assert Header Node evaluate the header of a HTTP Request"
toc = true
+++

### Introduction ###
The Assert Header node allows to evaluate the header of a HTTP Request. The node consists of three (3) parameters, which are the following:

* Name, the name of the node
* Error Template, the message to be shown when the assert failed
* Function, is the text area to define a function in the global namespace, with two parameters, *header*, the HTTP request's header, and *scope*, of the graph. E.g.:

    	f = function(headers, scope) {
    		return headers.auth_token != null;
    	}

Below is an example of implementing the node.

{{<figure src="/img/docs/assert-header-node.png" caption="Assert Header Node">}} 

When executing the graph and looking at the results, the assert node would evaluate the function.


### Conditional Execution ###
With the appropriate design, a graph could execute more than one (1) path in parallel. By exploiting the use of the Assert Header node, you could create a conditional path. For example, creating a two (2) way path, with two arrows pointing to two Assert Header node, then it means the are two paths on the graph. If on the first node you evaluate there is an authentication token, and on the second node there is not, meaning that both nodes are excluding paths. When executing the graph it means that it would follow the path depending on the request header, the figure below shows an example of the scenario. 

{{<figure src="/img/docs/assert-header-conditional.png" caption="Conditional header execution">}}  