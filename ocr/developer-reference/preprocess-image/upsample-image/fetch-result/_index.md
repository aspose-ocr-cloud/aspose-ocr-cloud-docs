---
weight: 20
date: "2023-05-11"
author: "Vladimir Lapin"
type: docs
url: /fetch-upsampling-result/
feedback: OCRCLOUD
title: Fetching resized image
description: How to fetch a resized image from Aspose.OCR Cloud.
keywords:
- enlarge
- width
- height
- upscale
- scale
- get
- obtain
- fetch
- result
---

When an image is [submitted](/ocr/send-image-for-upsampling/#using-the-dedicated-endpoint) for upsampling, the request is queued similar to the [recognition workflow](/ocr/recognition-workflow/) to ensure a stable response even under heavy load. You can show the enlarged image, send it for recognition, or apply another processing method.

{{% alert color="primary" %}}
The resized image is always returned in PNG format.
{{% /alert %}}

To obtain the resized image, send a **GET** request to the `https://api.aspose.cloud/v5.0/ocr/upscaleimage` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

Provide the [unique identifier](/ocr/send-image-for-upsampling/#return-value) of the upsampling task in `id` parameter:

```bash
curl --location --request GET 'https://api.aspose.cloud/v5.0/ocr/upscaleimage?id=c4b60313-4f78-45f8-b708-069eb98dc22e' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA' \
```

## Processing results

The processing result is returned in JSON format in the response body.

```json
{
	"id": "c4b60313-4f78-45f8-b708-069eb98dc22e",
	"taskStatus": "Completed",
	"responseStatusCode": "Ok",
	"results": [
		{
			"type": "ImagePNG",
			"data": "iVBORw0KGgoAAAANSUhEUgAAAboAAAA...If1ueN7AAAAABJRU5ErkJggg=="
		}
	],
	"error": null
}
```

{{% alert color="primary" %}}
Resized images are stored in the Aspose cloud and can be obtained by the task ID within **24 hours** after the image was sent for processing.
{{% /alert %}}

Property | Type | Description
--------- | ---- | -----------
`id` | string | Unique identifier of the upsampling task. Equals to the value of the `id` request property.
`taskStatus` | string | [Current state](#task-statuses) of the upsampling task in the queue.
`responseStatusCode` | string | Upsampling response status.
`results` | array | Resized image in PNG format, returned as Base64 encoded string. You must decode it to display on the screen or save to a file.
`error/messages` | string[] | Processing error messages, if any.<br />Even if the image is processed, you can still get notifications and warnings about non-fatal errors.

## Task statuses

Upsampling may take up to several seconds depending on the Aspose.OCR cloud load and image size. The status of the processing task is indicated in the `taskStatus` property of the result.

Status code | Description | To do
----------- | ----------- | ------
Pending | The image is queued for processing, but not yet processed. | Try fetching the result in a couple of seconds using the same ID.
Processing | The image is currently being processed. | Fetch the result again using the same ID.
Completed | The image is processed. | Read the processed image from `results` property.
Error | An error occurred during processing. | Check messages in the `error` property for more information.
NotExist | The request with the specified ID does not exist, or the result has already been deleted from the cloud storage. | Check the ID or [send the image for upsampling](/ocr/send-image-for-upsampling/#using-the-dedicated-endpoint) again with the same parameters.