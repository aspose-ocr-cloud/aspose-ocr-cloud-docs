---
weight: 20
date: "2023-11-27"
author: "Vladimir Lapin"
type: docs
url: /fetch-font-identification-result/
feedback: OCRCLOUD
title: Fetching font identification result
description: How to get the font identification result from the Aspose.OCR Cloud queue.
keywords:
- queue
- get
- obtain
- fetch
- result
- font
- style
- bold
- italic
- typeface
---

When an image is [submitted](/ocr/send-image-for-font-identification/) for font detection, it is [queued](/ocr/recognition-workflow/) to ensure a stable response even under high load. To obtain the result, send a **GET** request to the `https://api.aspose.cloud/v5.0/ocr/IdentifyFont` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

Provide the [unique identifier](/ocr/send-image-for-font-identification/#return-value) of the font identification task in `id` parameter:

```bash
curl --request GET --location 'https://api.aspose.cloud/v5.0/ocr/IdentifyFont?id=c11c975d-5124-4555-9561-af40fb95ba07' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA' \
```

## Font identification results

The font identification result is returned in JSON format in the response body.

```json
{
	"id": "c11c975d-5124-4555-9561-af40fb95ba07",
	"responseStatusCode": "Ok",
	"taskStatus": "Completed",
	"results": [
		{
			"type": "Text",
			"data": "eydzdHlsZSc6ICdyZWd1bGFyJywgJ2ZvbnQnOiBbJ3RhaG9tYScsICd0aW1lcycsICd2ZXJkYW5hJ119"
		}
	],
	"error": null
}
```

{{% alert color="primary" %}}
Font identification results are stored in the Aspose cloud and can be obtained by the task ID within **24 hours** after the image was sent for font identification.
{{% /alert %}}

Property | Type | Description
-------- | ---- | -----------
`id` | string | Unique identifier of the font identification task. Equals to the value of the `id` request property.
`taskStatus` | string | [Current state](#task-statuses) of the font identification task in the queue.
`responseStatusCode` | string | Font identification response status.
`results` | array | The list of fonts and styles in JSON format, encoded as Base64 string. You must decode it to display on the screen or save to a file.
`error/messages` | string[] | Font identification error messages, if any.<br />Even if the results are returned, you can still get notifications and warnings about non-fatal font identification errors.

### Detected fonts and styles

The list of fonts and styles is returned in JSON format:

```json
{
	'style': 'regular',
	'font': ['tahoma', 'times', 'verdana']
}
```

Property | Type | Description
-------- | ---- | -----------
`style` | string | The most common style used in text.
`font` | array | The list of fonts used on the image, in order of best matching.

## Task statuses

Font identification may take up to several seconds depending on the Aspose.OCR cloud load and the size of the original scan or photo. The status of the font identification task is indicated in the `taskStatus` property of the font identification result.

Status code | Description | To do
----------- | ----------- | ------
Pending | The image is queued for font identification, but not yet processed. | Try fetching the result in a couple of seconds using the same ID.
Processing | Aspose.OCR Cloud is currently identifying fonts in an image. | Fetch the result again using the same ID.
Completed | The fonts have been identified. | Read the font identification result from `results` property.
Error | An error occurred during font identification. | Check messages in the `error` property for more information.
NotExist | The request with the specified ID does not exist, or the result has already been deleted from the cloud storage. | Check the ID or [send the image for font identification](/ocr/send-image-for-font-identification/) again with the same parameters.
