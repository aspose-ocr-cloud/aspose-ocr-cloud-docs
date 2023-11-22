---
weight: 20
date: "2023-03-06"
author: "Vladimir Lapin"
type: docs
url: /fetch-regions/
feedback: OCRCLOUD
title: Fetching image regions
description: How to get the image regions from the Aspose.OCR Cloud queue.
keywords:
- detect
- find
- block
- region
- area
- column
- queue
- get
- obtain
- fetch
- result
---

When an image is [submitted](/ocr/send-for-detection/) for region detection, it is [queued](/ocr/recognition-workflow/) to ensure a stable response even under high load. To obtain the found regions, send a **GET** request to the `https://api.aspose.cloud/v5.0/ocr/DetectRegions` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

Provide the [unique identifier](/ocr/send-for-detection/#return-value) of the region detection task in `id` parameter:

```bash
curl --request GET --location 'https://api.aspose.cloud/v5.0/ocr/DetectRegions?id=a371d027-4b0d-4d86-8825-c8d818dd4ed9' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...VhKdGWxrJHdPr-OiTRL6-A' \
```

## Found regions

The regions found on an image are returned in JSON format in the response body.

```json
{
	"id": "a371d027-4b0d-4d86-8825-c8d818dd4ed9",
	"responseStatusCode": "Ok",
	"taskStatus": "Completed",
	"results": [
		{
			"type": "Other",
			"data": "W1swLCA4LCA2OTcsIDQ0MV1d"
		}
	],
	"error": null
}
```

{{% alert color="primary" %}}
Detected regions are stored in the Aspose cloud and can be obtained by the task ID within **24 hours** after the image was sent for OCR.
{{% /alert %}}

Property | Type | Description
--------- | ---- | -----------
`id` | string | Unique identifier of the region detection task. Equals to the value of the `id` request property.
`taskStatus` | string | [Current state](#task-statuses) of the region detection task in the queue.
`responseStatusCode` | string | Region detection response status.
`results` | array | Regions found on an image. An array of rectangles determined by their top-left and bottom-right corners. The type of a result is always _"Other"_.<br />All regions are returned as Base64 encoded strings. You must decode them before use. For example, `W1swLCA4LCA2OTcsIDQ0MV1d` is `[[0, 8, 697, 441]]`.
`error/messages` | string[] | Error messages, if any.<br />Even if the regions are found, you can still get notifications and warnings about non-fatal errors.

## Task statuses

Region detection may take up to several seconds depending on the Aspose.OCR cloud load and image size. The status of the task is indicated in the `taskStatus` property of the region detection result.

Status code | Description | To do
----------- | ----------- | ------
Pending | The image is queued for region detection, but not yet processed. | Try fetching the result in a couple of seconds using the same ID.
Processing | The regions are currently being detected. | Fetch the result again using the same ID.
Completed | Region detection is finished. | Read the regions from `results` property.
Error | An error occurred during region detection. | Check messages in the `error` property for more information.
NotExist | The request with the specified ID does not exist, or the result has already been deleted from the cloud storage. | Check the ID or [send the image](/ocr/send-for-detection/) again with the same parameters.
