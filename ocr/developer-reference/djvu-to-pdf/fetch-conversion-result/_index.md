---
weight: 20
date: "2023-05-12"
author: "Vladimir Lapin"
type: docs
url: /fetch-djvu-conversion-result/
feedback: OCRCLOUD
title: Fetching PDF converted from DjVu
description: How to get the PDF document converted from DjVu file from the Aspose.OCR Cloud queue.
keywords:
- OCR
- DjVu
- PDF
- queue
- get
- obtain
- fetch
- result
---

When a DjVu file is [submitted](/ocr/send-djvu-for-conversion/) for conversion, it is [queued](/ocr/recognition-workflow/) to ensure a stable response even under high load. To obtain the result, send a **GET** request to the `https://api.aspose.cloud/v5.0/ocr/djvu2pdf` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

Provide the [unique identifier](/ocr/send-djvu-for-conversion/#return-value) of the conversion task in `id` parameter:

```bash
curl --location --request GET 'https://api.aspose.cloud/v5.0/ocr/djvu2pdf?id=c4b60313-4f78-45f8-b708-069eb98dc22e' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA' \
```

## Conversion results

The resulting PDF document is returned in JSON format in the response body.

```json
{
	"id": "c4b60313-4f78-45f8-b708-069eb98dc22e",
	"taskStatus": "Completed",
	"responseStatusCode": "Ok",
	"results": [
		{
			"type": "Pdf",
			"data": "QWxsIG1lbiBsaXZlIGVudm...Vsb3BlZCBpbiB3aGFsZS1saW5lcy4="
		}
	],
	"error": null
}
```

{{% alert color="primary" %}}
Converted PDF documents are stored in the Aspose cloud and can be obtained by the task ID within **24 hours** after the DjVu file was sent for conversion.
{{% /alert %}}

Property | Type | Description
--------- | ---- | -----------
`id` | string | Unique identifier of the conversion task. Equals to the value of the `id` request property.
`taskStatus` | string | [Current state](#task-statuses) of the conversion task in the queue.
`responseStatusCode` | string | Conversion response status.
`results` | array | PDF document with original images in the background. The file is returned as Base64 encoded string. You must decode it to display or save to a file.
`error/messages` | string[] | Conversion error messages, if any.<br />Even if the DjVu is converted, you can still get notifications and warnings about non-fatal conversion errors.

## Task statuses

Conversion may take up to several seconds depending on the Aspose.OCR cloud load and DjVu file size. The status of the conversion task is indicated in the `taskStatus` property of the conversion result.

Status code | Description | To do
----------- | ----------- | ------
Pending | The DjVu is queued for conversion, but not yet processed. | Try fetching the result in a couple of seconds using the same ID.
Processing | The DjVu is currently being converted. | Fetch the result again using the same ID.
Completed | The DjVu is converted. | Read the PDF from `results` property.
Error | An error occurred during conversion. | Check messages in the `error` property for more information.
NotExist | The request with the specified ID does not exist, or the result has already been deleted from the cloud storage. | Check the ID or [send the DjVu for conversion](/ocr/send-djvu-for-conversion/) again with the same parameters.
