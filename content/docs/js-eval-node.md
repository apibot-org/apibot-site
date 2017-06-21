+++
description = "Description of the JS Eval Node"
title = "JS Eval Node"
date = "2017-05-18T10:42:08+01:00"
draft = false
weight = 30
bref="The JS Eval node is useful to add logic for the scenario"
toc = true
+++

## Definition ##

The JS Eval node define a function in the global namespace that given a scope *S* returns the scope *S*, after applying logic to it.
```
f: Scope -> Scope
```

### Parameter ###
The scope is the required parameter to which the logic will be applied.    

Parameter | Description
--- | ---
scope | The scope where the logic will be applied to

### Example ###
For example, the scope *S = {"user": "Carlos", "age": 25 }* and the JS eval node defines a property on the scope, telling if the user is an adult or not. A function representation is as follow

```
f = (scope) =>{
	scope["adult"] = scope["age"] >= 18;
	return scope;
}
```
with the scope changing to

```
s = {
	"user": "Carlos",
	"age": 25,
	"adult": "TRUE"
}
```


## Tutorial ##

### Introduction ###
The JS Eval node is helpful to apply Javascript logic to the scenario. This node has two parameters which are:

* name, label to assign a name for the node
* function, where you define a function in the global namespace, which takes a scope as argument and returns a scope.  

In the example below, we will be using the twitter example (presented on the quickstart).  
We will create an auth variable, and this variable will concatenate the Key and Secret variable that were created on the scope, with a ":" in the middle. As shown on the following code:  

    (scope)=>{ 
    var auth = btoa(scope.key+":"+scope.secret);
    scope.auth = "Basic" + auth;
    }

{{<figure src="/img/docs/js-eval-node.png" caption="JS Eval node">}} 

After adding the auth variable, we could use it later on the graph. Following the example, we will use the auth as a header on an HTTP Request node. We will call the variable with this syntax $(auth) on the authorization header

{{<figure src="/img/docs/http-request-twitter oauth2.png" caption="HTTP Request node">}} 
