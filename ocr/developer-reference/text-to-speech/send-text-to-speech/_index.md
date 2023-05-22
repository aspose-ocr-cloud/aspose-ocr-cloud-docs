---
weight: 10
date: "2023-05-12"
author: "Vladimir Lapin"
type: docs
url: /send-text-to-speech/
feedback: OCRCLOUD
title: Sending text for conversion
description: How to send text to Aspose.OCR cloud API to convert it to voice.
keywords:
- aloud
- voice
- TTS
- speech
- sound
- send
---

To read the text aloud, send a **POST** request to the `https://api.aspose.cloud/v5.0/ocr/converttexttospeech` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

The text and conversion parameters are provided in JSON format in the request body.

```json
{
	"text": "Read this text aloud",
	"settings": {
		"language": "English",
		"resultType": "Wav"
	}
}
```

## Providing a text

The string to be read aloud is specified in the value of the `text` property.

{{% alert color="primary" %}} 
At the moment, the Aspose.OCR Cloud API can only read aloud English texts.
{{% /alert %}}

## Conversion settings

Property | Type | Default&nbsp;value | Description
------- | ---- | ------------- | -----------
`language` | string | `English` | Specify the [language](/ocr/supported-languages/) for reading the text aloud. At the moment, `English` is the only supported option.
`resultType` | string | `Wav` | Audio file [format](/ocr/result-format/). At the moment, `Wav` (Waveform Audio) is the only supported option.

## Return value

If successful, this method returns a string with a unique identifier (GUID) of the text-to-speech conversion request in the [queue](/ocr/recognition-workflow/).

Otherwise, it returns a HTTP status code corresponding to the error.

## What's next

The text-to-speech conversion will take a few seconds, depending on the amount of text and the current Aspose.Cloud load. See the article [Fetching audio](/ocr/fetch-voice/) for information on how to fetch a voice from a server.

## cURL example

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --location --request POST 'https://api.aspose.cloud/v5.0/ocr/converttexttospeech' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...DpisWjfwe5RsfNCQ9Uh7Ig' \
--data '{
	"text": "Read this text aloud",
	"settings": {
		"language": "English",
		"resultType": "Wav"
	}
}'
```
{{< /tab >}}
{{< tab tabNum="2" >}}
```
TTS01232-9d40-4f2d-8eda-f1fc0b12bce6
```
{{< /tab >}}
{{< /tabs >}}
