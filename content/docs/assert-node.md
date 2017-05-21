+++
description = "Description of the Assert Node"
title = "Assert Node"
date = "2017-05-20T14:34:08+01:00"
draft = false
weight = 50
bref="The Assert Node evaluate the scope of the graph"
toc = true
+++

### Introduction ###
The Assert node allows to evaluate the scope on a given graph. The node consists of three (3) parameters, which are the following:

* Name, the name of the node
* Error Template, the message to be shown when the assert failed
* Function, is the text area to define an anonymous function which takes the scope as argument and returns the scope. E.g.

		(fn [scope] (assoc scope :happy true))

Below is an example of implementing the node.

{{<figure src="/img/docs/assert-node.png" caption="Assert Node">}} 

When executing the graph and looking at the results, the assert node would evaluate the function, the example below shows the result when the assert failed. 

{{<figure src="/img/docs/assert-fail.png" caption="Executing a fail assert">}}  


### Conditional Execution ###
With the appropriate design, a graph could execute more than one (1) path in parallel. By exploiting the use of the Assert node, you could create a conditional path. For example, creating a two (2) way path, with two arrows pointing to two Assert node, then it means the are two paths on the graph. If on the first node you assign a status code to go from 200 to 299, and the second node you select to go from 300 to 399, meaning that both nodes are excluding paths. When executing the graph it means that it would follow the path depending on the response status, the figure below shows an example of the scenario. 

{{<figure src="/img/docs/conditional-status.png" caption="Conditional execution">}}  