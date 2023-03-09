---
weight: 20
date: "2023-02-20"
author: "Vladimir Lapin"
type: docs
url: /fetch-receipt-recognition-result/
feedback: OCRCLOUD
title: Fetching receipt recognition result
description: How to get the receipt recognition result from the Aspose.OCR Cloud queue.
keywords:
- OCR
- recognize
- queue
- get
- obtain
- fetch
- result
- slip
- check
- statement
---

When a receipt is [submitted](/ocr/send-receipt-for-recognition/) for recognition, it is [queued](/ocr/recognition-workflow/) to ensure a stable response even under high load. To obtain the result, send a **GET** request to the `https://api.aspose.cloud/v5.0/ocr/RecognizeReceipt` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

Provide the [unique identifier](/ocr/send-receipt-for-recognition/#return-value) of the recognition task in `id` parameter:

```bash
curl --location --request GET 'https://api.aspose.cloud/v5.0/ocr/RecognizeReceipt?id=3f030db3-de56-4acb-8469-d696be9dc9a2' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA' \
```

## Recognition results

The recognition result is returned in JSON format in the response body.

```json
{
	"id": "3f030db3-de56-4acb-8469-d696be9dc9a2",
	"taskStatus": "Completed",
	"responseStatusCode": "Ok",
	"results": [
		{
			"type": "Text",
			"data": "QWNtZSBDb3Jwb3JhdGlvbgo...5pcyBiYWxscyAkMw=="
		}
	],
	"error": null
}
```

{{% alert color="primary" %}}
Recognition results are stored in the Aspose cloud and can be obtained by the task ID within **24 hours** after the receipt was set for OCR.
{{% /alert %}}

Property | Type | Description
--------- | ---- | -----------
`id` | string | Unique identifier of the receipt recognition task. Equals to the value of the `id` request property.
`taskStatus` | string | [Current state](#task-statuses) of the receipt recognition task in the queue.
`responseStatusCode` | string | Recognition response status.
`results` | array | [Recognition results](/ocr/result-format/) (depend on the `resultType` property of the recognition task).<br />All results (including plain text) are returned as Base64 encoded strings. You must decode them to display on the screen or save to a file.
`error/messages` | string[] | Recognition error messages, if any.<br />Even if the receipt is recognized, you can still get notifications and warnings about non-fatal recognition errors.

## Task statuses

Recognition may take up to several seconds depending on the Aspose.OCR cloud load and the size of the original scan or photo. The status of the recognition task is indicated in the `taskStatus` property of the recognition result.

Status code | Description | To do
----------- | ----------- | ------
Pending | The receipt is queued for recognition, but not yet processed. | Try fetching the result in a couple of seconds using the same ID.
Processing | The receipt is currently recognized. | Fetch the result again using the same ID.
Completed | The receipt is recognized. | Read the recognition result from `results` property.
Error | An error occurred during recognition. | Check messages in the `error` property for more information.
NotExist | The request with the specified ID does not exist, or the result has already been deleted from the cloud storage. | Check the ID or [send the receipt for recognition](/ocr/send-receipt-for-recognition/) again with the same parameters.
