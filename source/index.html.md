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

Upload text data to AssemblyAI to create custom models that will be up to 50% more accurate than generic speech APIs. This text data can be historical transcripts, or keywords/phrases.

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

Don’t have historical transcripts? You can still transcribe without a custom model. Your transcriptions will be made using our default models. Accuracy will be pretty good, but less accurate than a custom model. You can also upload a small amount of example transcripts to bootstrap a custom model.

See examples in the Guides section.

# Guides

## Creating a custom model for better accuracy
## Creating a custom model to recognize custom words
## Boostrapping a custom model for better accuracy
## Getting a transcript in real-time
## Getting a transcript of an audio file asynchronously

# Authentication

> Setting the Authorization header with curl

```shell
# With shell, you can just pass the correct header with each request
curl "https://api.assemblyai.com/v1/model"
  -H "Authorization: your-secret-api-token"
```

Authentication with the API is accomplished with with header argument, "Authorization". This is required for all API endpoints.

> Make sure to replace `your-secret-api-token` with your API key.

<aside class="notice">
You must replace <code>your-secret-api-token</code> with your personal API key.
</aside>

# /model

## POST /model

> Create a custom model to be more accurate at detecting two keywords "foo" and "bar"

```shell
curl --request POST \
    --url 'https://api.assemblyai.com/v1/model' \
    --header 'authorization: your-secret-api-token' \
    --data '
    {
      "name": "foobar",
      "phrases": ["foo", "bar"]
    }'
```

> The above command returns JSON structured like this:

```json
{
  "model": {
    "status": "training",
    "updated": "2017-12-11T23:14:48.539760Z",
    "name": "foobar",
    "warning": "Phrase count low, adding phrases will improve accuracy",
    "id": 76089,
    "closed_domain": false
  }
}
```

Create a custom speech recognition model. To learn more about custom models, read <a href="#custom-models">here.</a>

### HTTP Request

`POST https://api.assemblyai.com/v1/model`

### Query Parameters

Parameter | Example | Required | Description
--------- | ------- | ----------- | -----------
phrases | ["foo", "bar"] | Yes | Upload text data to AssemblyAI to create custom models. This text data can be historical transcripts, or keywords/phrases.
name | acme | No | The name of the model you are creating.
closed_domain | True | No | Default is False. Set to True to restrict recognition to only words found in the phrases array. This improves accuracy for simple use cases where you only need to recognize a few commands/words.

<aside class="notice">
The <code>status</code> key in the response will change from <code>training</code> to <code>trained</code> in about 10-20 minutes. Once the status is <code>trained</code> you can begin using the custom model to create transcripts.
</aside>