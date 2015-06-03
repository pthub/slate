---
title: API Reference

language_tabs:
  - python
  - java

toc_footers:
   - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the PremFina API ! You can use our API to access information in our systems.

The API is REST based and "language agnostic" supporting consumers using a variety of programming languages.

Examples in  Java and Python are shown to the right, you can switch the programming language of the examples with the tabs in the top right.

# Authentication

Authentication is via a process of login. After you are setup on systems you can login via a user name and password.

On login you will receive a temporary token, the token can be used for further calls to the APIs.

The token expires after a period of inactivity i.e. 5 minutes.

The sequence of operations are 

1. Login API call
2. Further API calls
3. Logout API call

If you do not make the logout API call the token expires in 5 minutes  and the process is to be repeated, i.e login ..

## Login to the system

> To login, use this code:

```python

import requests
import json

payload = {"user": "bennetts", "password": "pa33w0rd-2"}

headers = {'Content-type': 'application/json'}

response = requests.post("http://api.premfina.com/login", data=json.dumps(payload), headers = headers)

token = response.text

```

```java

Coming soon

```


> Replace `user` and password with your details.


A sample token is given below

`Token: 25892e17-80f6-415f-9c65-7395632f0223`

<aside class="notice">
The temporary authenticated token will expire if there is a period of inactivity of 5 minutes.
</aside>


## Logout of the system

This endpoint is used to logout.

### HTTP Request

`POST http://api.premfina.com/logout/{token}`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
token | false | Pass in the temporary token issued after a login request


<aside class="success">
A HTTP status code of 204 denoting a successful logout
</aside>


```python
import requests

headers = {'Content-type': 'application/json'}

requests.post("http://api.premfina.com/logout/25892e17-80f6-415f-9c65-7395632f0223", headers = headers)

```

```java

coming soon

```

#Scheme

A scheme is a configuration containing the details of the product

## Get a list of schemes

```python
import requests

headers = {'Content-type': 'application/json'}

requests.get("http://api.premfina.com/schemes/25892e17-80f6-415f-9c65-7395632f0223", headers = headers)

```

```java

Coming soon
```


> The above command returns JSON structured like this:

```json
[ { "name":"scheme1",
  "description": "A description of the scheme",
  "product":{
      "code":"product1",
	  "collectionParams":{
	      "params":[{"key":"frequency","value":"12"}]}},
  "code":"schemeCode1"},
  { "name":"scheme2",
  "description": "A description of scheme2",
  "product":{
      "code":"product2",
	  "collectionParams":{
	      "params":[{"key":"frequency","value":"12"}]}},
  "code":"schemeCode2"}
  ]
```

This endpoint retrieves a list of schemes on the system.

<aside class="warning">These schemes already exist on our systems</aside>

### HTTP Request

`GET http://api.premfina.com/schemes/{token}`

### Path Variable

Parameter | Description
--------- | -----------
Token | The Authentication token received after login


## Get a scheme

```python
import requests

headers = {'Content-type': 'application/json'}

requests.get("http://api.premfina.com/schemes/{schemeCode}/25892e17-80f6-415f-9c65-7395632f0223", headers = headers)

```

```java

Coming soon
```


> The above command returns JSON structured like this:

```json
{ "name":"scheme1",
  "description": "A description of the scheme",
  "product":{
      "code":"product1",
	  "collectionParams":{
	      "params":[{"key":"frequency","value":"12"}]}},
  "code":"schemeCode1"}
```


This endpoint retrieves a list of schemes on the system.

<aside class="warning">The scheme must already exist on our systems</aside>

### HTTP Request

`GET http://api.premfina.com/schemes/{schemeCode}/{token}

### Path Variable

Parameter | Description
--------- | -----------
schemeCode | A particular scheme code from the list of schemes
token | The Authentication token received after login

#Quote

A quote contains the financial details and is retrieved passing in particulars.

A persistent quote is a quote that remains on the system and is activated later on demand.

## Retrieve a Quote


```python
import requests

headers = {'Content-type': 'application/json'}

payload = { schemeCode="scheme1", premium = "", deposit ="" }

requests.post("http://api.premfina.com/quote/25892e17-80f6-415f-9c65-7395632f0223", data=json.dumps(payload), headers = headers)

```

```java

Coming soon
```

> The above command returns JSON structured like this:

```json
{ "scheme":{
          "name":null,
		  "description":null,
		  "product":{
		       "code": null,
			   "collectionParams":{
			         "params":[
					   {"key":"frequency","value":"12"}]}
					},
			"code":null},
	"premium":0.0,
	"deposit":0.0,
	"noInstallments":0,
	"apr":0.0,
	"flatRate":0.0,
	"installmentAmount":0.0
}

```


This endpoint retrieves a quote


### HTTP Request

`POST http://api.premfina.com/quote/{token}

### Path Variable

Parameter | Description
--------- | -----------
token | The Authentication token received after login

## Retrieve a Persistent Quote


```python
import requests

headers = {'Content-type': 'application/json'}

payload = { schemeCode="scheme1", 
            premium = "", 
			deposit ="",
		   { "fullName":"Joe Bloggs",
		     "firstName": "Joe",
			 "surname": "Bloggs",
			 "addresses":[
			      {"country":"UK",
				   "addressLine1": "",
				   "addressLine2": "",
				   "addressLine3": "",
				   "city": "London",
				   "zipCode": "EC2 NW"}],
				   "contacts":[
				     {"email": "test@mail",
					  "landline": "",
					  "mobile": "",
					  "fax": ""}],
			"bankAccounts":[
				{"sortCode":"",
				 "accountNumber":"",
				 "accountType":"",
				 "accountName":""}]}
}

requests.post("http://api.premfina.com/quote/persist/25892e17-80f6-415f-9c65-7395632f0223", data=json.dumps(payload), headers = headers)

```

```java

Coming soon
```

> The above command returns JSON structured like this:

```json
{ "scheme":{
          "name":null,
		  "description":null,
		  "product":{
		       "code": null,
			   "collectionParams":{
			         "params":[
					   {"key":"frequency","value":"12"}]}
					},
			"code":null},
	"premium":0.0,
	"deposit":0.0,
	"noInstallments":0,
	"apr":0.0,
	"flatRate":0.0,
	"installmentAmount":0.0,
	"persistentQuoteId":"persistentQuoteId-213"
}

```


This endpoint retrieves a persistent quote


### HTTP Request

`POST http://api.premfina.com/quote/persist/{token}

### Path Variable

Parameter | Description
--------- | -----------
token | The Authentication token received after login

<aside class="warning">The persistent quote can be activated later on demand by passing in the persistentQuoteId</aside>


#Agreement

An agreement is a financed insurance policy

An agreement can be activated by passing in the persistentQuoteId retrieved from the persistent quote api.

An agreement can also be created by passing in the details of a retrieved quote and the details of the Customer including the bank details.

## Create an agreement from a persistent quote

```python
import requests

headers = {'Content-type': 'application/json'}

requests.post("http://api.premfina.com/agreement/persist/persistentQuoteId-213/25892e17-80f6-415f-9c65-7395632f0223",  headers = headers)

```

```java

Coming soon
```

> The above command returns JSON structured like this:

```json
{
  "agreementNumber":"123",
  "customer":{ "fullName":"Joe Bloggs",
		     "firstName": "Joe",
			 "surname": "Bloggs",
			 "addresses":[
			      {"country":"UK",
				   "addressLine1": "",
				   "addressLine2": "",
				   "addressLine3": "",
				   "city": "London",
				   "zipCode": "EC2 NW"}],
				   "contacts":[
				     {"email": "test@mail",
					  "landline": "",
					  "mobile": "",
					  "fax": ""}],
			"bankAccounts":[
				{"sortCode":"",
				 "accountNumber":"",
				 "accountType":"",
				 "accountName":""}]},
	  "quote":{ "scheme":{
          "name":null,
		  "description":null,
		  "product":{
		       "code": null,
			   "collectionParams":{
			         "params":[
					   {"key":"frequency","value":"12"}]}
					},
			"code":null},
			"premium":0.0,
			"deposit":0.0,
			"noInstallments":0,
			"apr":0.0,
			"flatRate":0.0,
			"installmentAmount":0.0
		},
      "premium":0.0,
	  "deposit":0.0,
	  "noInstallments":0,
	  "apr":0.0,
	  "flatRate":0.0,"installmentAmount":0.0},
	  "scheduled":[{"date":null,"amount":0.0,"description":null}],
	  "params":[{"key":null,"value":null}],
	  "policyNumber":null,
	  "timeWindowDays":0}

```


This endpoint creates an agreement from a persistent quote


### HTTP Request

`POST http://api.premfina.com/agreement/persist/{persistentQuoteId}/{token}

### Path Variable

Parameter | Description
--------- | -----------
persistentQuoteId | The previously requested persistent quote
token | The Authentication token received after login

<aside class="info">The agreement is activated from a persistent quote within the time window</aside>

## Create an agreement

```python
import requests

headers = {'Content-type': 'application/json'}

payload = { 
           requestDate: "2015-06-03 10:00:00",
          "customer":{ "fullName":"Joe Bloggs",
		     "firstName": "Joe",
			 "surname": "Bloggs",
			 "addresses":[
			      {"country":"UK",
				   "addressLine1": "",
				   "addressLine2": "",
				   "addressLine3": "",
				   "city": "London",
				   "zipCode": "EC2 NW"}],
				   "contacts":[
				     {"email": "test@mail",
					  "landline": "",
					  "mobile": "",
					  "fax": ""}],
			"bankAccounts":[
				{"sortCode":"",
				 "accountNumber":"",
				 "accountType":"",
				 "accountName":""}]},
		  "quote":{ "scheme":{
			  "name":null,
			  "description":null,
			  "product":{
				   "code": null,
				   "collectionParams":{
						 "params":[
						   {"key":"frequency","value":"12"}]}
						},
				"code":null},
				"premium":0.0,
				"deposit":0.0,
				"noInstallments":0,
				"apr":0.0,
				"flatRate":0.0,
				"installmentAmount":0.0
			}}


requests.post("http://api.premfina.com/agreement/create/25892e17-80f6-415f-9c65-7395632f0223",  data=json.dumps(payload), headers = headers)

```

```java

Coming soon
```

> The above command returns JSON structured like this:

```json
{
  "agreementNumber":"123",
  "customer":{ "fullName":"Joe Bloggs",
		     "firstName": "Joe",
			 "surname": "Bloggs",
			 "addresses":[
			      {"country":"UK",
				   "addressLine1": "",
				   "addressLine2": "",
				   "addressLine3": "",
				   "city": "London",
				   "zipCode": "EC2 NW"}],
				   "contacts":[
				     {"email": "test@mail",
					  "landline": "",
					  "mobile": "",
					  "fax": ""}],
			"bankAccounts":[
				{"sortCode":"",
				 "accountNumber":"",
				 "accountType":"",
				 "accountName":""}]},
	  "quote":{ "scheme":{
          "name":null,
		  "description":null,
		  "product":{
		       "code": null,
			   "collectionParams":{
			         "params":[
					   {"key":"frequency","value":"12"}]}
					},
			"code":null},
			"premium":0.0,
			"deposit":0.0,
			"noInstallments":0,
			"apr":0.0,
			"flatRate":0.0,
			"installmentAmount":0.0
		},
      "premium":0.0,
	  "deposit":0.0,
	  "noInstallments":0,
	  "apr":0.0,
	  "flatRate":0.0,"installmentAmount":0.0},
	  "scheduled":[{"date":null,"amount":0.0,"description":null}],
	  "params":[{"key":null,"value":null}],
	  "policyNumber":null,
	  "timeWindowDays":0}

```


This endpoint creates an agreement based on a quote and a Customer


### HTTP Request

`POST http://api.premfina.com/agreement/create/{token}

### Path Variable

Parameter | Description
--------- | -----------
token | The Authentication token received after login

<aside class="info">The agreement is created</aside>

## Get an agreement

```python
import requests

headers = {'Content-type': 'application/json'}

requests.get("http://api.premfina.com/agreement/get/agreement-123/25892e17-80f6-415f-9c65-7395632f0223",  headers = headers)

```

```java

Coming soon
```

> The above command returns JSON structured like this:

```json
{
  "agreementNumber":"123",
  "customer":{ "fullName":"Joe Bloggs",
		     "firstName": "Joe",
			 "surname": "Bloggs",
			 "addresses":[
			      {"country":"UK",
				   "addressLine1": "",
				   "addressLine2": "",
				   "addressLine3": "",
				   "city": "London",
				   "zipCode": "EC2 NW"}],
				   "contacts":[
				     {"email": "test@mail",
					  "landline": "",
					  "mobile": "",
					  "fax": ""}],
			"bankAccounts":[
				{"sortCode":"",
				 "accountNumber":"",
				 "accountType":"",
				 "accountName":""}]},
	  "quote":{ "scheme":{
          "name":null,
		  "description":null,
		  "product":{
		       "code": null,
			   "collectionParams":{
			         "params":[
					   {"key":"frequency","value":"12"}]}
					},
			"code":null},
			"premium":0.0,
			"deposit":0.0,
			"noInstallments":0,
			"apr":0.0,
			"flatRate":0.0,
			"installmentAmount":0.0
		},
      "premium":0.0,
	  "deposit":0.0,
	  "noInstallments":0,
	  "apr":0.0,
	  "flatRate":0.0,"installmentAmount":0.0},
	  "scheduled":[{"date":null,"amount":0.0,"description":null}],
	  "params":[{"key":null,"value":null}],
	  "policyNumber":null,
	  "timeWindowDays":0}

```


This endpoint creates an agreement based on a quote and a Customer


### HTTP Request

`GET http://api.premfina.com/agreement/{agreementId}/{token}

### Path Variable

Parameter | Description
--------- | -----------
agreementId | The agreement id to return
token | The Authentication token received after login

<aside class="info">The details of the agreement</aside>