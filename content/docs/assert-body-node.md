+++
description = "Description of the Assert Body Node"
title = "Assert Body Node"
date = "2017-05-20T14:42:08+01:00"
draft = false
weight = 70
bref="The Assert Body Node evaluate the body of a HTTP Response"
toc = true
+++

### Introduction ###
The Assert Body node allows to evaluate the body of a HTTP Response. The node consists of three (3) parameters, which are the following:

* Name, the name of the node
* Error Template, the message to be shown when the assert failed
* Function, is the text area to define a function in the global namespace, with two parameters, *body*, the HTTP response body, and *scope*, of the graph. E.g.:

    	f = function(body, scope) {
    		return body.user_id != scope.user_id;
    	}

Below is an example of implementing the node.

{{<figure src="/img/docs/assert-body-node.png" caption="Assert Body Node">}} 

When executing the graph and looking at the results, the assert node would evaluate the function.


### Conditional Execution ###
With the appropriate design, a graph could execute more than one (1) path in parallel. By exploiting the use of the Assert Body node, you could create a conditional path. For example, creating a two (2) way path, with two arrows pointing to two Assert node, then it means the are two paths on the graph. If on the first node you assign a status code to go from 200 to 299, and the second node you select to go from 300 to 399, meaning that both nodes are excluding paths. When executing the graph it means that it would follow the path depending on the response status, the figure below shows an example of the scenario. 

{{<figure src="/img/docs/assert-body-conditional.png" caption="Conditional body execution">}}  