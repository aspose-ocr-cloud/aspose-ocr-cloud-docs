---
weight: 20
date: "2023-02-27"
author: "Vladimir Lapin"
type: docs
url: /fetch-voice/
feedback: OCRCLOUD
title: Fetching audio
description: How to get the text-to-speech conversion result from the Aspose.OCR Cloud queue.
keywords:
- aloud
- voice
- TTS
- speech
- sound
- stream
- get
- fetch
- media
- download
---

When text is [submitted](/ocr/send-text-to-speech/) to be converted to speech, the request is [queued](/ocr/recognition-workflow/) to ensure a stable response even under heavy load. To get the resulting sound:

## Fetching conversion result as JSON

This query can be useful if you want to have full control over the text-to-speech conversion results, such as checking for errors or monitoring the status of a conversion task.

Send a **GET** request to the `https://api.aspose.cloud/v5.0/ocr/TextToSpeech/GetTextToSpeechResult` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

Provide the [unique identifier](/ocr/send-text-to-speech/#return-value) of the conversion task in `id` parameter:

```bash
curl --location --request GET 'https://api.aspose.cloud/v5.0/ocr/TextToSpeech/GetTextToSpeechResult?id=TTS01232-9d40-4f2d-8eda-f1fc0b12bce6' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...DpisWjfwe5RsfNCQ9Uh7Ig' \
```

The conversion result is returned in JSON format in the response body.

```json
{
	"id": "TTS01232-9d40-4f2d-8eda-f1fc0b12bce6",
	"responseStatusCode": "Ok",
	"taskStatus": "Completed",
	"results": [
		{
			"type": "WavFile",
			"data": "UklGRiSJAQBXQVZFZm10IBAAAA...9p6f808/9c/f+a/P/OAgA="
		}
	],
	"error": null
}
```

{{% alert color="primary" %}}
Text-to-speech conversion results are stored in the Aspose cloud and can be obtained by the task ID within **24 hours** after the text was sent for conversion.
{{% /alert %}}

Property | Type | Description
--------- | ---- | -----------
`id` | string | Unique identifier of the conversion task. Equals to the value of the `id` request property.
`taskStatus` | string | [Current state](#task-statuses) of the conversion task in the queue.
`responseStatusCode` | string | Conversion response status.
`results` | array | Audio file. The audio is returned as a Base64 encoded string. You must decode it in order to play it or save it to a file.
`error/messages` | string[] | Conversion error messages, if any. Even if the conversion succeed, you can still get notifications and warnings about non-fatal errors.

### Task statuses

Text-to-speech conversion may take up to several seconds depending on the Aspose.OCR cloud load. The status of the conversion task is indicated in the `taskStatus` property of the conversion result.

Status code | Description | To do
----------- | ----------- | ------
Pending | The text is queued for conversion to speech, but not yet processed. | Try fetching the result in a couple of seconds using the same ID.
Processing | The text is currently being converted to speech. | Fetch the result again using the same ID.
Completed | Text to speech conversion is finished. | Play or save the audio from `results` property.
Error | An error occurred during conversion. | Check messages in the `error` property for more information.
NotExist | The request with the specified ID does not exist, or the result has already been deleted from the cloud storage. | Check the ID or [send the text for conversion](/ocr/send-text-to-speech/) again with the same parameters.

## Fetching audio file

This query can be useful if you just want to read text aloud on a website or in app without focusing on technical details.

Send a **GET** request to the `https://api.aspose.cloud/v5.0/ocr/TextToSpeech/GetTextToSpeechResultFile` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

Provide the [unique identifier](/ocr/send-text-to-speech/#return-value) of the conversion task in `id` parameter:

```bash
curl --location 'https://api.aspose.cloud/v5.0/ocr/TextToSpeech/GetTextToSpeechResultFile?id=TTSdcbdb-c6d5-4299-ba91-e46245a1c8d7' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...DpisWjfwe5RsfNCQ9Uh7Ig' \
```

The voice is returned as an audio file (_audio/wav_).
