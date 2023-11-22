---
weight: 10
date: "2023-05-12"
author: "Vladimir Lapin"
type: docs
url: /send-djvu-for-conversion/
feedback: OCRCLOUD
title: Sending DjVu for conversion
description: How to send a DjVu file for conversion into a PDF document to the Aspose.OCR Cloud API.
keywords:
- OCR
- DjVu
- PDF
- queue
- send
---

To convert DjVu file to a PDF document, send a **POST** request to the `https://api.aspose.cloud/v5.0/ocr/djvu2pdf` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

The DjVu file is provided as a value of `image` property in JSON request body. The file contents must be Base64 encoded.

```json
{
  "image": "DjVu file as Base64 string",
}
```

## Return value

If successful, this method returns a string with a unique identifier (GUID) of the conversion request in the [queue](/ocr/recognition-workflow/).

Otherwise, it returns a HTTP status code corresponding to the error.

## What's next

Conversion will take a few seconds, depending on the size of the image and the current Aspose.Cloud load. See the article [Fetching PDF converted from DjVu](/ocr/fetch-djvu-conversion-result/) for information on how to get a PDF document from the server.

## cURL example

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --request POST --location 'https://api.aspose.cloud/v5.0/ocr/djvu2pdf' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA' \
--data-raw '{
  "image": "iVBORw0KGgoAAAANSUh...d1iEAAAAASUVORK5CYII=",
}'
```
{{< /tab >}}
{{< tab tabNum="2" >}}
```
a197aade-bba9-4c7a-92c7-46851b3dceaa
```
{{< /tab >}}
{{< /tabs >}}
