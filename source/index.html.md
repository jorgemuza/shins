---
title: Glass API v1.0.0
language_tabs:
  - shell: Shell
  - javascript: JavaScript
toc_footers: []
includes:
  - errors
search: true
highlight_theme: darkula
headingLevel: 2


---



# Introduction

Glass retrieves user-authorized account and transactional data from financial institutions and returns it to third-party solutions in an organized, highly usable format.

Glass’s API has an architectural style of a RESTful design pattern. It uses HTTP as its underlying protocol, where standard HTTP verbs and HTTP response codes are used. Communication travels via HTTPS to ensure a secure data exchange. Almost every response body is JSON encoded, unless stated on the endpoint description.  Since RESTful services and JSON are highly popular and most major development languages include a form to interact with these technologies, it's quite easy to integrate with Sync's API.

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.


# Authentication


> Make sure to pass the API Key token on all your requests made to Glass API endpoints:


```shell
# With shell, you can just pass the correct header with each request
curl -X POST \
  https://apidev.paybook.com/v1/glass/[ENDPOINT]?token=[API_KEY_TOKEN] \
  -H 'Content-Type: application/json'
```

```javascript
$.ajax({
  url: 'https://apidev.paybook.com/v1/glass/[ENDPOINT]?token=[API_KEY_TOKEN]',
  method: 'post',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
});

```

Glass uses API keys to allow access to the API, the API key token needs to be included in all API requests made to the server:

`token=[API_KEY_TOKEN]`


In order to obtain an API key token you will need to invoke the authUser endpoint where you will pass your Glass username and password, please see below
for a detailed explanation.


<aside class="warning">
You must replace <code>[API_KEY_TOKEN]</code> with your personal API key.
</aside>



## authUser


<a id="opIdauthUser"></a>


> Code samples


```shell
# You can also use wget
curl -X POST https://apidev.paybook.com/v1/users/login \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```


```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

$.ajax({
  url: 'https://apidev.paybook.com/v1/users/login',
  method: 'post',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})


```


`POST /users/login`


*Logs user into the system*


> Body parameter


```json
{
  "username": "string",
  "password": "string"
}
```


<h3 id="authUser-parameters">Parameters</h3>


|Parameter|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[UserCreds](#schemausercreds)|true|Created user object|


> Example responses


```json
{
  "token": "string",
  "username": "string",
  "timestamp": 0,
  "alias": "string",
  "accounts": "string",
  "apps": [
    "string"
  ],
  "can_createBusiness": true,
  "is_qa": true
}
```


<h3 id="authUser-responses">Responses</h3>


|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|successful operation|[UserToken](#schemausertoken)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Invalid username/password supplied|None|


<aside class="success">
This operation does not require authentication
</aside>


> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.


Glass API documentation reference


Base URLs:


* <a href="https://apidev.paybook.com/v1/glass">https://apidev.paybook.com/v1/glass</a>


<h1 id="Glass-API-transactions">transactions</h1>


## getTransactions


<a id="opIdgetTransactions"></a>


> Code samples


```shell
# You can also use wget
curl -X GET https://apidev.paybook.com/v1/glass/transactions/{id_transaction} \
  -H 'Accept: application/json'


```


```javascript
var headers = {
  'Accept':'application/json'


};


$.ajax({
  url: 'https://apidev.paybook.com/v1/glass/transactions/{id_transaction}',
  method: 'get',


  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})


```


`GET /transactions/{id_transaction}`


*Returns a list of transactions from the system that the user has access to*


<h3 id="getTransactions-parameters">Parameters</h3>


|Parameter|In|Type|Required|Description|
|---|---|---|---|---|
|id_transaction|query|string(guid)|false|Transaction ID|
|id_paybook|query|array[string]|false|List of paybook ID's|
|id_paybook_theme|query|array[string]|false|List of paybook theme ID's|
|id_paybook_theme_type|query|array[string]|false|List of paybook theme type ID's|
|is_auto|query|boolean(int64)|false|Automatic or manual transactions ( Based on transaction source catalog )|
|transaction_type|query|string|false|Transactions type: expense | income|
|has_attachment|query|boolean(int64)|false|Transaction with or without attachments|
|description|query|array[string]|false|List of words to filter transactions using transaction's description or related paybook names|
|id_currency|query|string(guid)|false|Currency ID|
|is_disable|query|boolean(int64)|false|Disabled transactions|
|dt_transaction_from|query|number(date)|false|Transaction creation, start date|
|dt_transaction_to|query|number(date)|false|Transaction creation, end date|
|skip|query|string(date)|false|Query results start index|
|limit|query|integer(int64)|false|Query limit results, default: 500|
|order|query|array[string]|false|Sort order columns|


> Example responses


```json
[
  {
    "id_transaction": "string",
    "id_currency": "string",
    "id_transaction_source": "string",
    "is_disable": true,
    "description": "string",
    "source_description": "string",
    "amount": null,
    "reference": "string",
    "notes": "string",
    "extra": "string",
    "currency": 0,
    "paybooks": [
      "string"
    ],
    "owner": "string",
    "has_attachment": true,
    "attachments": [
      null
    ],
    "dt_transaction": null,
    "dt_disable": null,
    "dt_create": null,
    "dt_modify": null
  }
]
```


<h3 id="getTransactions-responses">Responses</h3>


|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Collection of Transactions|Inline|


<h3 id="getTransactions-responseschema">Response Schema</h3>


Status Code **200**


|Name|Type|Required|Description|
|---|---|---|---|
|*anonymous*|[[Transaction](#schematransaction)]|false|No description|
|» id_transaction|string(guid)|false|Transaction ID|
|» id_currency|string(guid)|false|Currency ID|
|» id_transaction_source|string(guid)|false|Transaction Source ID|
|» is_disable|boolean(int64)|false|Is Disabled?|
|» description|string(string)|false|Description|
|» source_description|string(string)|false|Source Description|
|» amount|float(currency)|false|Amount|
|» reference|string(string)|false|Reference|
|» notes|string(string)|false|Notes|
|» extra|string(string)|false|Extra|
|» currency|number(currency)|false|Currency|
|» paybooks|[string]|false|Paybooks|
|» owner|string(guid)|false|Owner|
|» has_attachment|boolean(int64)|false|Has attachment?|
|» attachments|[file]|false|List of attachments|
|» dt_transaction|date(number)|false|Transaction Date|
|» dt_disable|date(number)|false|Disabled Date|
|» dt_create|date(number)|false|Creation Date|
|» dt_modify|date(number)|false|Modification Date|


<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
api_key
</aside>


# Schemas


<h2 id="tocSapiresponse">APIResponse</h2>


<a id="schemaapiresponse"></a>


```json
{
  "rid": "string",
  "code": 0,
  "errors": [
    "string"
  ],
  "status": "string",
  "message": "string",
  "response": {}
}
```


### Properties


|Name|Type|Required|Description|
|---|---|---|---|
|rid|string(guid)|false|Request Identifier|
|code|integer(int64)|false|Code|
|errors|[string]|false|Errors Collection|
|status|string(string)|false|Response status|
|message|string(string)|false|Response message|
|response|object|false|Endpoint response|


<h2 id="tocSusercreds">UserCreds</h2>


<a id="schemausercreds"></a>


```json
{
  "username": "string",
  "password": "string"
}
```


### Properties


|Name|Type|Required|Description|
|---|---|---|---|
|username|string(string)|false|Username|
|password|string(MD5)|false|MD5 encoded Password|


<h2 id="tocSusertoken">UserToken</h2>


<a id="schemausertoken"></a>


```json
{
  "token": "string",
  "username": "string",
  "timestamp": 0,
  "alias": "string",
  "accounts": "string",
  "apps": [
    "string"
  ],
  "can_createBusiness": true,
  "is_qa": true
}
```


### Properties


|Name|Type|Required|Description|
|---|---|---|---|
|token|string(guid)|false|API Key Token|
|username|string(guid)|false|Username|
|timestamp|number(timestamp)|false|Timestamp|
|alias|string(string)|false|User Alias|
|accounts|string(string)|false|Associated Accounts|
|apps|[string]|false|Associated Apps|
|can_createBusiness|boolean(int64)|false|Can User Create Business?|
|is_qa|boolean(int64)|false|Is QA user?|


<h2 id="tocStransaction">Transaction</h2>


<a id="schematransaction"></a>


```json
{
  "id_transaction": "string",
  "id_currency": "string",
  "id_transaction_source": "string",
  "is_disable": true,
  "description": "string",
  "source_description": "string",
  "amount": null,
  "reference": "string",
  "notes": "string",
  "extra": "string",
  "currency": 0,
  "paybooks": [
    "string"
  ],
  "owner": "string",
  "has_attachment": true,
  "attachments": [
    null
  ],
  "dt_transaction": null,
  "dt_disable": null,
  "dt_create": null,
  "dt_modify": null
}
```


### Properties


|Name|Type|Required|Description|
|---|---|---|---|
|id_transaction|string(guid)|false|Transaction ID|
|id_currency|string(guid)|false|Currency ID|
|id_transaction_source|string(guid)|false|Transaction Source ID|
|is_disable|boolean(int64)|false|Is Disabled?|
|description|string(string)|false|Description|
|source_description|string(string)|false|Source Description|
|amount|float(currency)|false|Amount|
|reference|string(string)|false|Reference|
|notes|string(string)|false|Notes|
|extra|string(string)|false|Extra|
|currency|number(currency)|false|Currency|
|paybooks|[string]|false|Paybooks|
|owner|string(guid)|false|Owner|
|has_attachment|boolean(int64)|false|Has attachment?|
|attachments|[file]|false|List of attachments|
|dt_transaction|date(number)|false|Transaction Date|
|dt_disable|date(number)|false|Disabled Date|
|dt_create|date(number)|false|Creation Date|
|dt_modify|date(number)|false|Modification Date|


