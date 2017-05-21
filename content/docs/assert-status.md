+++
description = "Description of the Assert Status Node"
title = "Assert Status Node"
date = "2017-05-19T10:39:08+01:00"
draft = false
weight = 60
bref="The Assert Status Node evaluate the status of a HTTP Response"
toc = true
+++

### Introduction ###
The Assert Status node allows to evaluate the status code from a HTTP Response message. The node consists of three (3) parameters, which are the following:

* Name, the name of the node
* Status From, the response status code minimum accepted value
* Status To, the response status code maximum accepted value

Below is an example of implementing the node.

{{<figure src="/img/docs/assert-status-twitter-oauth2.png" caption="Assert Status">}} 

When executing the graph and looking at the results, the assert node would evaluate if the response status code was between does values, the example below shows the result when the assert failed. 

{{<figure src="/img/docs/assert-fail.png" caption="Executing a fail assert">}}  


### Conditional Execution ###
With the appropriate design, a graph could execute more than one (1) path in parallel. By exploiting the use of the Assert Status node, you could create a conditional path. For example, creating a two (2) way path, with two arrows pointing to two Assert Status node, then it means the are two paths on the graph. If on the first node you assign a status code to go from 200 to 299, and the second node you select to go from 300 to 399, meaning that both nodes are excluding paths. When executing the graph it means that it would follow the path depending on the response status, the figure below shows an example of the scenario. 

{{<figure src="/img/docs/conditional-status.png" caption="Conditional execution">}}  