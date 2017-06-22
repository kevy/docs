---
title: API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='mailto:support@kevy.co'>Request a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Kevy API! You can use our API to access Kevy API endpoints, which can get information on various campaigns, lists, contacts, and automations in our database.

We have language bindings in Shell! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: kevyapikey"
```

> Make sure to replace `kevyapikey` with your API key.

Kevy uses API keys to allow access to the API. You can request a new Kevy API key at by contacting Support[support@kevy.co].

Kevy expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: kevyapikey`

<aside class="notice">
You must replace <code>kevyapikey</code> with your personal API key.
</aside>

# Lists

## Get All Lists

```shell
curl "http://example.com/api/lists"
  -H "Authorization: kevyapikevy"
```

```javascript
const kevy = require('kevy');

let api = kevy.authorize('kevyapikevy');
let lists = api.lists.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all lists.

### HTTP Request

`GET http://example.com/api/lists`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include lists that have already been adopted.

<aside class="success">
Remember — a happy list is an authenticated list!
</aside>

## Get a Specific List

```ruby
require 'kevy'

api = Kevy::APIClient.authorize!('kevyapikevy')
api.lists.get(2)
```

```python
import kevy

api = kevy.authorize('kevyapikevy')
api.lists.get(2)
```

```shell
curl "http://example.com/api/lists/2"
  -H "Authorization: kevyapikevy"
```

```javascript
const kevy = require('kevy');

let api = kevy.authorize('kevyapikevy');
let max = api.lists.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific list.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/lists/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the list to retrieve

