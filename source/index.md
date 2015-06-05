---
title: API Reference

language_tabs:
  - python
  - java

toc_footers:
   - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the PremFina API ! You can use our API to access information in our systems.

The API is REST based and "language agnostic" supporting consumers using a variety of programming languages.

Examples in  Java and Python are shown to the right, you can switch the programming language of the examples with the tabs in the top right.

# Version

To find the latest version of the API

## Ping the system 

> To ping, use this code:

```python

import requests

headers = {'Content-type': 'application/json'}

response = requests.post("https://api.premfina.com/ping", headers = headers)

print response.text

```

```java

Coming soon

```

A sample version is given below

`v1.0`

<aside class="notice">
The API call returns the version of the API
</aside>


# Authentication

After you are set up on our systems, you can login via a user name and password.

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

response = requests.post("https://api.premfina.com/login", data=json.dumps(payload), headers = headers)

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

`POST https://api.premfina.com/logout/{token}`

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

requests.post("https://api.premfina.com/logout/25892e17-80f6-415f-9c65-7395632f0223", headers = headers)

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

requests.get("https://api.premfina.com/schemes/25892e17-80f6-415f-9c65-7395632f0223", headers = headers)

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

`GET https://api.premfina.com/schemes/{token}`

### Path Variable

Parameter | Description
--------- | -----------
Token | The Authentication token received after login


## Get a scheme

```python
import requests

headers = {'Content-type': 'application/json'}

requests.get("https://api.premfina.com/schemes/{schemeCode}/25892e17-80f6-415f-9c65-7395632f0223", headers = headers)

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


This endpoint retrieves a scheme based on the scheme code.

<aside class="warning">The scheme must already exist on our systems</aside>

### HTTP Request

`GET https://api.premfina.com/schemes/{schemeCode}/{token}

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

payload = { schemeCode="scheme1", premium = "", deposit ="" , renewal="N"}

requests.post("https://api.premfina.com/quote/25892e17-80f6-415f-9c65-7395632f0223", data=json.dumps(payload), headers = headers)

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


This endpoint retrieves a quote, the renewal flag is used for existing agreements


### HTTP Request

`POST https://api.premfina.com/quote/{token}

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

requests.post("https://api.premfina.com/quote/persist/25892e17-80f6-415f-9c65-7395632f0223", data=json.dumps(payload), headers = headers)

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


This endpoint retrieves a persistent quote. The persistent quote is stored on the system for activation at a later date.


### HTTP Request

`POST https://api.premfina.com/quote/persist/{token}

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

requests.post("https://api.premfina.com/agreement/persist/persistentQuoteId-213/25892e17-80f6-415f-9c65-7395632f0223",  headers = headers)

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

`POST https://api.premfina.com/agreement/persist/{persistentQuoteId}/{token}

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


requests.post("https://api.premfina.com/agreement/create/25892e17-80f6-415f-9c65-7395632f0223",  data=json.dumps(payload), headers = headers)

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

`POST https://api.premfina.com/agreement/create/{token}

### Path Variable

Parameter | Description
--------- | -----------
token | The Authentication token received after login

<aside class="info">The agreement is created</aside>

## Renew an agreement

```python
import requests

headers = {'Content-type': 'application/json'}

requests.post("https://api.premfina.com/agreement/renew/25892e17-80f6-415f-9c65-7395632f0223", headers = headers)

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

This endpoint renews an existing agreement

### HTTP Request

`POST https://api.premfina.com/agreement/renew/{token}

### Path Variable

Parameter | Description
--------- | -----------
token | The Authentication token received after login

<aside class="info">The agreement is renewed</aside>

## Cancel an agreement

```python
import requests

headers = {'Content-type': 'application/json'}

payload = { "agreementNo": "", "cancellationReason": "", cancellationTypes : ""}

requests.post("https://api.premfina.com/agreement/cancel/25892e17-80f6-415f-9c65-7395632f0223", data=json.dumps(payload), headers = headers)

```

```java

Coming soon
```

This endpoint cancels an existing agreement

### HTTP Request

`POST https://api.premfina.com/agreement/cancel/{token}

### Path Variable

Parameter | Description
--------- | -----------
token | The Authentication token received after login

<aside class="info">The agreement is cancelled</aside>

## Get an agreement

```python
import requests

headers = {'Content-type': 'application/json'}

requests.get("https://api.premfina.com/agreement/get/agreement-123/25892e17-80f6-415f-9c65-7395632f0223",  headers = headers)

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


This endpoint retrieves an agreement


### HTTP Request

`GET https://api.premfina.com/agreement/{agreementId}/{token}

### Path Variable

Parameter | Description
--------- | -----------
agreementId | The agreement id to return
token | The Authentication token received after login

<aside class="info">The details of the agreement</aside>

#Financials

## Payment schedule for an agreement

```python
import requests

headers = {'Content-type': 'application/json'}

requests.get("https://api.premfina.com/agreement/getschedule/agreement-123/25892e17-80f6-415f-9c65-7395632f0223",  headers = headers)

```

```java

Coming soon
```

> The above command returns JSON structured like this:

```json
[ {"date":"2015-06-03","amount":0.0,"description": "schedule1"},
  {"date":"2015-06-04","amount":0.0,"description": "schedule2"},
  {"date":"2015-06-05","amount":0.0,"description": "schedule3"}
]

```


This endpoint lists the payment schedule for an agreement


### HTTP Request

`GET https://api.premfina.com/agreement/getschedule/{agreementId}/{token}

### Path Variable

Parameter | Description
--------- | -----------
agreementId | The agreement id to return
token | The Authentication token received after login

<aside class="info">The details of the payment schedule for an agreement</aside>

# Midterm adjustment

Mid term adjustments to an agreement

## MTA - Address change

```python
import requests

headers = {'Content-type': 'application/json'}

payload = { 
           requestDate: "2015-06-03 10:00:00",
          "customer":{ 
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
					  "fax": ""}]}
			}


requests.post("https://api.premfina.com/agreement/modify/address/25892e17-80f6-415f-9c65-7395632f0223",  data=json.dumps(payload), headers = headers)

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


This endpoint modifies an agreement


### HTTP Request

`POST https://api.premfina.com/agreement/modify/address/{token}

### Path Variable

Parameter | Description
--------- | -----------
token | The Authentication token received after login

<aside class="info">The customers address is changed</aside>

## MTA - Bank account change

```python
import requests

headers = {'Content-type': 'application/json'}

payload = { 
           requestDate: "2015-06-03 10:00:00",
          "customer":{ 
			 "bankAccounts":[
				{"sortCode":"",
				 "accountNumber":"",
				 "accountType":"",
				 "accountName":""}]}
			}


requests.post("https://api.premfina.com/agreement/modify/bankaccount/25892e17-80f6-415f-9c65-7395632f0223",  data=json.dumps(payload), headers = headers)

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


This endpoint modifies an agreement


### HTTP Request

`POST https://api.premfina.com/agreement/modify/bankaccount/{token}

### Path Variable

Parameter | Description
--------- | -----------
token | The Authentication token received after login

<aside class="info">The customers bank account is changed</aside>

## MTA - Premium change - Quote

```python
import requests

headers = {'Content-type': 'application/json'}

payload = { 
           "requestDate": "2015-06-03 10:00:00",
           "agreementNumber": "123",
		   "premium" : ""		   
			}


requests.post("https://api.premfina.com/agreement/get/premium/quote/25892e17-80f6-415f-9c65-7395632f0223",  data=json.dumps(payload), headers = headers)

```

```java

Coming soon
```

> The above command returns JSON structured like this:

```json
{
  "agreementNumber":"123",
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


This endpoint retrieves the quote for a change in premium


### HTTP Request

`POST https://api.premfina.com/agreement/get/premium/quote/{token}'  

### Path Variable

Parameter | Description
--------- | -----------
token | The Authentication token received after login

<aside class="info">Get the quote for a change in premium for an existing agreement</aside>

## MTA - Premium change

```python
import requests

headers = {'Content-type': 'application/json'}

payload = { 
           "requestDate": "2015-06-03 10:00:00",
           "agreementNumber": "123",
		   "premium" : ""		   
			}


requests.post("https://api.premfina.com/agreement/modify/premium/quote/25892e17-80f6-415f-9c65-7395632f0223",  data=json.dumps(payload), headers = headers)

```

```java

Coming soon
```

> The above command returns JSON structured like this:

```json
{
  "agreementNumber":"123",
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


This endpoint modifies the agreement for a change in premium and returns the quote for the change.


### HTTP Request

`POST https://api.premfina.com/agreement/modify/premium/quote/{token}'  

### Path Variable

Parameter | Description
--------- | -----------
token | The Authentication token received after login

<aside class="info">Modify the agreement with the details of the change in premium</aside>

# Payer

The payer template is used to send the details of the customer to third parties.

## Payer details

```python
import requests

headers = {'Content-type': 'application/json'}

response = requests.get("https://api.premfina.com/payer/000003461/25892e17-80f6-415f-9c65-7395632f0223",  headers = headers)

```

```java

Coming soon
```

> The above command returns JSON structured like this:

```json

  { "payerReference":"000003461",
    "title":"MS",
	"firstName":"MIR",
	"initials":"",
	"lastName":"BLANKSON",
	"address1":"120",
	"address2":"AR DRIVE",
	"town":"HARROW",
	"address3":"MIDDLESEX",
	"address4":"",
	"postCode":"HA2 8PP",
	"telephoneNumber":null,
	"emailAddress":null,
	"sortCode":"110356",
	"accountNumber":"00035470",
	"accountHoldersName":"MISS M BLANKSON"
	}

```


This endpoint returns the payer details associated with the agreement


### HTTP Request

`GET https://api.premfina.com/payer/{agreementNo}/{token}'  

### Path Variable

Parameter | Description
--------- | -----------
agreementNo | An unique agreement number
token | The Authentication token received after login

<aside class="info">Get the DD payer details in a concise format</aside>


## Multiple Payers' details

```python
import requests

headers = {'Content-type': 'application/json'}

payload = ['000003461', '000003242', '000003231']

url = "https://localhost:8082/payers/%s" % token

response = requests.get(url, data=json.dumps(payload), headers = headers)

print response.status_code

print response.text

```

```java

Coming soon
```

> The above command returns JSON structured like this:

```json

  [ { "payerReference":"000003461",
      "title":"MS",
	  "firstName":"MIRI",
	  "initials":"",
	  "lastName":"BLANKSON",
	  "address1":"120",
	  "address2":"AR DRIVE",
	  "town":"HARROW",
	  "address3":"MIDDLESEX",
	  "address4":"",
	  "postCode":"HA 8PP",
	  "telephoneNumber":null,
	  "emailAddress":null,
	  "sortCode":"111111",
	  "accountNumber":"000355555",
	  "accountHoldersName":"MISS M BLANKSON"},
	{ "payerReference":"000003242",
	  "title":"MR",
	  "firstName":"MIKE",
	  "initials":"",
	  "lastName":"ROBINSON",
	  "address1":"41",
	  "address2":"GO ROAD",
	  "town":"SWANSEA",
	  "address3":"WEST GLAMOR",
	  "address4":"",
	  "postCode":"SA 7DZ",
	  "telephoneNumber":"0000 00000",
	  "emailAddress":"MIKEROB@PREMFINA.COM",
	  "sortCode":"403333",
	  "accountNumber":"121212121",
	  "accountHoldersName":"M ROBINSON"},
   {  "payerReference":"000003231",
      "title":"MR",
	  "firstName":"GA",
	  "initials":"",
	  "lastName":"DAVIES",
	  "address1":"19",
	  "address2":"EL ROAD",
	  "town":"FOXTROT",
	  "address3":"CAMBRIDGESHIRE",
	  "address4":"",
	  "postCode":"PE8 4AU",
	  "telephoneNumber":"01234 455775",
	  "emailAddress":"GADAVIES@PREMINA.COM",
	  "sortCode":"111100",
	  "accountNumber":"00777777",
	  "accountHoldersName":"G  DAVIES"}
	]

```


This endpoint returns the  list of payers associated with the agreements 


### HTTP Request

`GET https://api.premfina.com/payers/{token}'  

### Path Variable

Parameter | Description
--------- | -----------
token | The Authentication token received after login

<aside class="info">Get the DD details of multiple payers in a concise format</aside>


## Payers changed since.


```python

url = "https://localhost:8082/payers/changedSince/3/%s" % token

print url

response = requests.get(url, data=json.dumps(payload), headers = headers)

print response.status_code

print response.text

```

```java

Coming soon
```

> The above command returns JSON structured like this:

```json

 [ { "payerReference":"000003461",
      "title":"MS",
	  "firstName":"MIRI",
	  "initials":"",
	  "lastName":"BLANKSON",
	  "address1":"120",
	  "address2":"AR DRIVE",
	  "town":"HARROW",
	  "address3":"MIDDLESEX",
	  "address4":"",
	  "postCode":"HA 8PP",
	  "telephoneNumber":null,
	  "emailAddress":null,
	  "sortCode":"111111",
	  "accountNumber":"000355555",
	  "accountHoldersName":"MISS M BLANKSON"},
	{ "payerReference":"000003242",
	  "title":"MR",
	  "firstName":"MIKE",
	  "initials":"",
	  "lastName":"ROBINSON",
	  "address1":"41",
	  "address2":"GO ROAD",
	  "town":"SWANSEA",
	  "address3":"WEST GLAMOR",
	  "address4":"",
	  "postCode":"SA 7DZ",
	  "telephoneNumber":"0000 00000",
	  "emailAddress":"MIKEROB@PREMFINA.COM",
	  "sortCode":"403333",
	  "accountNumber":"121212121",
	  "accountHoldersName":"M ROBINSON"},
   {  "payerReference":"000003231",
      "title":"MR",
	  "firstName":"GA",
	  "initials":"",
	  "lastName":"DAVIES",
	  "address1":"19",
	  "address2":"EL ROAD",
	  "town":"FOXTROT",
	  "address3":"CAMBRIDGESHIRE",
	  "address4":"",
	  "postCode":"PE8 4AU",
	  "telephoneNumber":"01234 455775",
	  "emailAddress":"GADAVIES@PREMINA.COM",
	  "sortCode":"111100",
	  "accountNumber":"00777777",
	  "accountHoldersName":"G  DAVIES"}
	]

```


This endpoint returns the  list of payers whose details have changed since the last "n days".


### HTTP Request

`GET https://api.premfina.com/payers/changedSince/{days}/{token}/csv'  

### Path Variable

Parameter | Description
--------- | -----------
days  | The number of days to look back, for any changes
token | The Authentication token received after login

<aside class="info">The agreements that have changed in the past time window are returned</aside>


## Payers changed since (in csv).


```python

url = "https://localhost:8082/payers/changedSince/3/%s/csv" % token

print url

response = requests.get(url, headers = headers)

print response.status_code

print response.text

```

```java

Coming soon
```

> The above command returns csv structured like this:

```csv

000003461,MS,MIR,,BLANKSON,1,A DRIVE,HARROW,MIDDLESEX,,HA 8PP,,,111111,0001111,MISS M BLANKSON
000003242,MR,M,,ROB,4,GO ROAD,SWANSEA,WEST G,,SA 7DZ,0111 552168,MROBINSON@PREMFINA.COM,111111,0001111,M A ROBINSON
000003231,MR,G,,DAVIES,1,E ROAD,HUNTINGDON,C,,PE2 4AU,0111 455775,GDAVIES@PREMFINA.COM,111111,0001111,G L DAVIE
000003237,MRS,S,,OXLEY,2,SELM PARK,LIVING,WEST LOTHIAN,,EH5 5NU,0111 435774,WOXLEY@PREMFINA.COM,111111,0001111,MRS S OXLEY
000003243,MR,D,,ROGERS,9,ALEXANDRA WAY,CRAMLINGTON,NORTH,,NE2 6EB,0111 713930,D.ROGERS924@PREMFINA.COM,111111,0001111,MR D ROGERS
000003247,MR,H,,WILL,21,GREEN LANES,LONDON,,,N 2HA,0208 809 0303,,111111,0001111,MR H WILLIAMS

```


This endpoint returns the  list of payers whose details have changed since the last "n days" as a csv.


### HTTP Request

`GET https://api.premfina.com/payers/changedSince/{days}/{token}/csv'  

### Path Variable

Parameter | Description
--------- | -----------
days  | The number of days to look back, for any changes
token | The Authentication token received after login

<aside class="info">The agreements that have changed in the past time window are returned in csv</aside>

## Payers changed since( csv file ).


```python

url = "https://localhost:8082/payers/changedSince/3/%s/csvfile" % token

print url

response = requests.get(url, headers = headers)

print response.status_code

print response.text

```

```java

Coming soon
```

> The above command returns csv file like this:

```csv

000003461,MS,MIR,,BLANKSON,1,A DRIVE,HARROW,MIDDLESEX,,HA 8PP,,,111111,0001111,MISS M BLANKSON
000003242,MR,M,,ROB,4,GO ROAD,SWANSEA,WEST G,,SA 7DZ,0111 552168,MROBINSON@PREMFINA.COM,111111,0001111,M A ROBINSON
000003231,MR,G,,DAVIES,1,E ROAD,HUNTINGDON,C,,PE2 4AU,0111 455775,GDAVIES@PREMFINA.COM,111111,0001111,G L DAVIE
000003237,MRS,S,,OXLEY,2,SELM PARK,LIVING,WEST LOTHIAN,,EH5 5NU,0111 435774,WOXLEY@PREMFINA.COM,111111,0001111,MRS S OXLEY
000003243,MR,D,,ROGERS,9,ALEXANDRA WAY,CRAMLINGTON,NORTH,,NE2 6EB,0111 713930,D.ROGERS924@PREMFINA.COM,111111,0001111,MR D ROGERS
000003247,MR,H,,WILL,21,GREEN LANES,LONDON,,,N 2HA,0208 809 0303,,111111,0001111,MR H WILLIAMS

```


This endpoint returns the  list of payers whose details have changed since the last "n days" as a csv file.


### HTTP Request

`GET https://api.premfina.com/payers/changedSince/{days}/{token}/csvfile'  

### Path Variable

Parameter | Description
--------- | -----------
days  | The number of days to look back, for any changes
token | The Authentication token received after login

<aside class="info">The agreements that have changed in the past time window are returned in csv file</aside>

# Success

The PremFina API uses the following success codes:

Error Code | Meaning
---------- | -------
200 | Op was successful
204 | Op was successful (without content)