---
title: AssemblyAI Docs

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

search: true
---

# AssemblyAI

Integrate the AssemblyAI API to recognize speech in your application in real-time or asynchronously.

Create custom models to more accurately recognize speech, and expand vocabulary with custom words like product/person names.

# Custom Models

Upload text data to AssemblyAI to create custom models that will be up to 50% more accurate than generic speech APIs. This text data can be historical transcripts, keywords/phrases.

Create as many custom models as you want: one per customer, one per dialogue state in an IVR system, or one per user of your application.

## How it Works

AssemblyAI's algorithms learn from the text that you upload to the API. We do this to fine tune our neural networks and create a custom speech recognition model for your application. This process takes about 10-20 minutes.

Then, when you make API calls to transcribe audio, your custom model will be used and you'll get more accurate transcripts as a result.

Here are the steps to create a custom model:

1. `POST` text data (historical transcripts or keywords/phrases) to `/model/`
1. `GET` `/model/` to get the status of your custom model
1. `POST` audio to `/transcript/` and include the `id` of your custom model as an API parameter

## Examples

**Improving recognition accuracy for recordings**

*Call Analytics Inc.* transcribes sales call recordings for 10 different customers. *Call Analytics Inc.* creates 10 custom models, one per customer, using the historical transcripts they've created for each customer. Now, when sending recordings to the API for transcription, *Call Analytics Inc.* tells the API which custom model to use with an API parameter. Creating a custom model for each of *Call Analytics Inc.'s* customers allows them to improve accuracy for each customer.

**Improving recognition accuracy for keywords/phrases**

*Johnny1.com* transcribes podcasts and looks for certain keywords/phrases to do topic tagging. *Johnny1.com* uploads the keywords and phrases they want to detect to the API to create a custom model. Then, *Johnny1.com*  uses this custom model to transcribe podcasts and the API is more accurate at detecting those keywords/phrases when they appear in the audio.

## Bootstrapping custom models

Don’t have historical transcripts? You can use our default models, or you can upload a small amount of example transcripts to bootstrap a custom model.

See examples in the Guides section.

# Guides

## Creating a custom model for better accuracy
## Creating a custom model to recognize custom words
## Boostrapping a custom model for better accuracy
## Getting a transcript in real-time
## Getting a transcript of an audio file asynchronously

# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
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

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
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

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

