---
weight: 60
date: "2023-03-01"
author: "Vladimir Lapin"
type: docs
url: /fetch-preprocessed-image/
feedback: OCRCLOUD
title: Fetching preprocessed image
description: How to get the preprocessed image from the Aspose.OCR Cloud queue.
keywords:
- preprocess
- temporary
- result
- download
---

[Skew correction](/ocr/deskew-image/#automatic-skew-correction), [dewarping](/ocr/dewarp-image/), [upsampling](/ocr/upsample-image/), and [binarization](/ocr/binarize-image/) preprocessing filters allow you to get back the resulting image so that you can show it, send it for recognition or apply another pre-processing method.

{{% alert color="primary" %}}
The preprocessed image is always returned in PNG format.
{{% /alert %}}

When a image is submitted for preprocessing, the request is queued similar to the [recognition workflow](/ocr/recognition-workflow/) to ensure a stable response even under heavy load. To get the processed image:

## Fetching preprocessing result as JSON

This query can be useful if you want to have full control over the preprocessing result, such as checking for errors or monitoring the status of a task.

Send a **GET** request to the `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/GetResultTask` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

Provide the unique identifier of the preprocessing task in `id` parameter:

```bash
curl --location --request GET 'https://api.aspose.cloud/v5.0/ocr/ImageProcessing/GetResultTask?id=94b25465-48cc-4485-8669-b18f66bef4ae' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...O4DLxGSyOGE0JogvQ' \
```

The result of preprocessing is returned in JSON format in the response body.

```json
{
	"id": "94b25465-48cc-4485-8669-b18f66bef4ae",
	"responseStatusCode": "Ok",
	"taskStatus": "Completed",
	"results": [
		{
			"type": "ImagePNG",
			"data": "iVBORw0KGgoAAAANSUhEUgAAAlgAAAFECAAAAADe8R99AAAgAEl...dBAAAAAElFTkSuQmCC"
		}
	],
	"error": null
}
```

{{% alert color="primary" %}}
Preprocessed images are stored in the Aspose cloud and can be obtained by the task ID within **24 hours** after the image was sent for processing.
{{% /alert %}}

Property | Type | Description
--------- | ---- | -----------
`id` | string | Unique identifier of the preprocessing task. Equals to the value of the `id` request property.
`taskStatus` | string | [Current state](#task-statuses) of the preprocessing task in the queue.
`responseStatusCode` | string | Preprocessing response status.
`results` | array | Preprocessed image in PNG format, returned as a Base64 encoded string. You must decode it in order to show it or save it to a file.
`error/messages` | string[] | Preprocessing error messages, if any. Even if the image war processed, you can still get notifications and warnings about non-fatal errors.

### Task statuses

Image preprocessing may take up to several seconds depending on the selected filter, image size, and Aspose.OCR cloud load. The status of the preprocessing task is indicated in the `taskStatus` property of the result.

Status code | Description | To do
----------- | ----------- | ------
Pending | The image is queued for processing, but not yet processed. | Try fetching the result in a couple of seconds using the same ID.
Processing | The image is currently being preprocessed. | Fetch the result again using the same ID.
Completed | Preprocessing is finished. | Show the image from `results` property or save it to a file.
Error | An error occurred during preprocessing. | Check messages in the `error` property for more information.
NotExist | The request with the specified ID does not exist, or the result has already been deleted from the cloud storage. | Check the ID or preprocess the image again.

## Fetching image file

This query can be useful if you just want to show the processed image on a website or in app without focusing on technical details.

Send a **GET** request to the `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/GetResultFile` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

Provide the unique identifier of the preprocessing task in `id` parameter:

```bash
curl --location --request GET 'https://api.aspose.cloud/v5.0/ocr/ImageProcessing/GetResultFile?id=94b25465-48cc-4485-8669-b18f66bef4ae' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...O4DLxGSyOGE0JogvQ' \
```

The image is returned in PNG format (_image/png_).
