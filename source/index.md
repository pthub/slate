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

Examples in  Java and Python are shown to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

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
import kittn

api = kittn.authorize('meowmeowmeow')
```


> Replace `user` and password with your details.

Authentication is via a process of login. After your setup on systems you can login via a user name and password.

On login you will receive a temporary token, the token can be used for further calls to the APIs.

The token expires after a period of inactivity i.e. 10 minutes.

The sequence of operations are 

1. Login API call
2. Further API calls
3. Logout API call

If you do not make the logout API call the token expires in 10 minutes  and the process is to be repeated, i.e login ..

A sample token is given below

`Token: 25892e17-80f6-415f-9c65-7395632f0223`

<aside class="notice">
The temporary authenticated token will expire if there is a period of inactivity of 10 minutes.
</aside>

# Login

## Login to the system

```python
import requests
import json

payload = {"user": "bennetts", "password": "pa33w0rd-2"}

headers = {'Content-type': 'application/json'}

response = requests.post("http://api.premfina.com/login", data=json.dumps(payload), headers = headers)

token = response.text
```

```java

coming soon

```



> The above command returns JSON structured like this:

```json
25892e17-80f6-415f-9c65-7395632f0223
```

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

## Get a Specific Kitten

```python
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```java
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```


> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Isis",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">If you're not using an administrator API key, note that some kittens will return 403 Forbidden if they are hidden for admins only.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the cat to retrieve

