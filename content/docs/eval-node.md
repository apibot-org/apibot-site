+++
description = "Description of the Eval Node"
title = "Eval Node"
date = "2017-05-18T10:42:08+01:00"
draft = false
weight = 31
bref="The Eval node is useful to add logic for the scenario"
toc = true
+++

### Introduction ###
The Eval node is helpful to apply logic to the scenario. This node has two parameters which are:

* name, label to assign a name for the node
* function, where you define a function in the global namespace, which takes a scope as argument and returns a scope.  

In the example below, we will be using the twitter example (presented on the quickstart).  
We will create an auth variable, and this variable will concatenate the Key and Secret variable that were created on the scope, with a ":" in the middle. As shown on the following code:  

    fn [scope] (assoc scope :happy true)

{{<figure src="/img/docs/js-eval-node.png" caption="JS Eval node">}} 

After adding the auth variable, we could use it later on the graph. Following the example, we will use the auth as a header on an HTTP Request node. We will call the variable with this syntax $(auth) on the authorization header

{{<figure src="/img/docs/http-request-twitter oauth2.png" caption="HTTP Request node">}} 
