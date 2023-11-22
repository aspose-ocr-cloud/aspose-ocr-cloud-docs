---
weight: 20
date: "2023-03-06"
author: "Vladimir Lapin"
type: docs
url: /fetch-region-recognition-result/
feedback: OCRCLOUD
title: Fetching regions recognition result
description: How to get the region recognition result from the Aspose.OCR Cloud queue.
keywords:
- OCR
- recognize
- queue
- get
- obtain
- fetch
- result
- region
- area
- block
---

When image regions are [submitted](/ocr/send-image-regions-for-recognition/) for recognition, the request is [queued](/ocr/recognition-workflow/) to ensure a stable response even under high load. To obtain the result, send a **GET** request to the `https://api.aspose.cloud/v5.0/ocr/RecognizeRegions` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

Provide the [unique identifier](/ocr/send-image-regions-for-recognition/#return-value) of the region recognition task in `id` parameter:

```bash
curl --request GET --location 'https://api.aspose.cloud/v5.0/ocr/RecognizeRegions?id=2ce30237-86da-41ef-88e9-84f0b7acffc0' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...Ly6HFO2W3iuX5XvtpjVA5FtYA' \
```

## Recognition results

The recognition result is returned in JSON format in the response body.

```json
{
	"id": "2ce30237-86da-41ef-88e9-84f0b7acffc0",
	"taskStatus": "Completed",
	"responseStatusCode": "Ok",
	"results": [
		{
			"type": "Text",
			"data": "QWxsIG1lbiBsaXZlIGVudmVsb3BlZCBpbiB3aGFsZS1saW5lcy4="
		}
	],
	"error": null
}
```

{{% alert color="primary" %}}
Recognition results are stored in the Aspose cloud and can be obtained by the task ID within **24 hours** after the image was sent for OCR.
{{% /alert %}}

Property | Type | Description
--------- | ---- | -----------
`id` | string | Unique identifier of the recognition task. Equals to the value of the `id` request property.
`taskStatus` | string | [Current state](#task-statuses) of the recognition task in the queue.
`responseStatusCode` | string | Recognition response status.
`results` | array | [Recognition results](/ocr/result-format/), separate entry per region. The result type depends on the `resultType` property of the recognition task.<br />All results (including plain text) are returned as Base64 encoded strings. You must decode them to display on the screen or save to a file.
`error/messages` | string[] | Recognition error messages, if any.<br />Even if all regions are recognized, you can still get notifications and warnings about non-fatal recognition errors.

## Task statuses

Recognition may take up to several seconds depending on the Aspose.OCR cloud load and image size. The status of the regions recognition task is indicated in the `taskStatus` property of the recognition result.

Status code | Description | To do
----------- | ----------- | ------
Pending | The image is queued for recognition, but not yet processed. | Try fetching the result in a couple of seconds using the same ID.
Processing | The image is currently recognized. | Fetch the result again using the same ID.
Completed | Image regions are recognized. | Read the recognition result from `results` property.
Error | An error occurred during recognition. | Check messages in the `error` property for more information.
NotExist | The request with the specified ID does not exist, or the result has already been deleted from the cloud storage. | Check the ID or [send image regions for recognition](/ocr/send-image-regions-for-recognition/) again with the same parameters.
