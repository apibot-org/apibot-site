+++
description = "Description of the Configuration Node"
title = "Configuration Node"
date = "2017-05-15T22:35:08+01:00"
draft = false
weight = 20
bref="The configuration node is a function that add new variables to the scope"
toc = true
+++

## Definition ##

The configuration node represents a function that given a scope *S* and a list of properties *(n0,v0), (n1,v1), ... ,(nk,vk)* returns the scope *S* with the new properties.
```
f: Scope -> Scope
```

### Parameter ###
The required parameters are the list of properties, to add to your scope, each property has two (2) values, the name of the property and the value.    

Parameter | Description
--- | ---
scope | The scope where the new properties will be assigned to
(n1, v1) | n1: correspond to the name of the first property. <br> v1: correspond to the value assign to n1.

### Example ###
For example, the scope *S = {"user": "Carlos" }* and the configuration node defines *age:=5* and *password := "xyz"*. A function representation is as follow

```
f = (scope) =>{
	scope["age"] = 5;
	scope["password"] = "xyz";
	return scope;
}
```
with the scope changing to

```
s = {
	"user": "Carlos",
	"age": 5,
	"password": "xyz"
}
```


## Tutorial ##

### Introduction ###
The configuration node is useful to create scope variables that could be call later on the scenario or when the config node is called. This node, has 1 visible parameter which is the **name** label to assign a name for the node. It has the option to add new parameters which are the properties, for this you select the node and click on **Add new property** on the right pane, where you will be able to add a new property (scope variables).

On the image below we are adding three properties and we will show you how they are use later. We will be using the example of twitter authentication for applications. The three properties are:

* Key
* Secret
* URL

{{<figure src="/img/docs/configuration-node.png" caption="Configuration node">}} 


### Calling the Property Variables ###
Now we will be calling the variables on a "JS Eval Node", on this node we will be doing a change on the scope. We will create an auth variable, and this variable will concatenate the Key and Secret variable created before, with a ":" in the middle. As shown on the following code:

    (scope)=>{ 
    var auth = btoa(scope.key+":"+scope.secret);
    scope.auth = "Basic" + auth;
    }

As you can see we are calling the variable key, and secret as *scope.key* and *scope.secret*.

{{<figure src="/img/docs/js-eval-node.png" caption="JS Eval node">}} 

The variables can also be called on a parameter input, as it shows on the image below, we will be doing a POST HTTP request. We will be using the property URL, to call the endpoint https://api.twitter.com/oauth2/token, for this we do the following:

* **$(url)**/oauth2/token 

{{<figure src="/img/docs/http-request-twitter oauth2.png" caption="HTTP Request node">}} 