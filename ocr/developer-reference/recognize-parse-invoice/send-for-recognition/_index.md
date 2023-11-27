---
weight: 10
date: "2023-11-27"
author: "Vladimir Lapin"
type: docs
url: /send-invoice-for-recognition/
feedback: OCRCLOUD
title: Sending invoice for recognition
description: How to send a photo or scan of the invoice for processing to the Aspose.OCR Cloud API.
keywords:
- OCR
- recognize
- queue
- send
- invoice
---

To extract information from a scanned or photographed invoice, send a **POST** request to the `https://api.aspose.cloud/v5.0/ocr/RecognizeAndParseInvoice` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

The invoice and recognition parameters are provided in JSON format in the request body.

```json
{
  "image": "Base64 string",
  "settings": {
    "language": "English",
    "makeSkewCorrect": true,
    "rotate": 0,
    "makeBinarization": false,
    "makeUpsampling": false,
    "makeSpellCheck": false,
  }
}
```

## Providing invoice image

Photo or scan of the invoice is provided in a value of `image` property as a Base64 encoded string.

{{% alert color="caution" %}}
Base64 encoded file can be very long, especially when recognizing scans and high resolution photos. As a result, you may encounter an error when calling recognition via cURL in a shell command. Use the `getconf ARG_MAX` command to check the maximum length of the command arguments (in bytes).
{{% /alert %}}

## Recognition settings

Property | Type | Default&nbsp;value | Description
------- | ---- | ------------- | -----------
`language` | string | `English` | Specify a [language](/ocr/supported-languages/) for recognition.
`makeSkewCorrect` | boolean | `true` | Automatically correct invoice image tilt (deskew) before proceeding to recognition.<br />Automatic deskew works for images rotated 15 degrees or less. If the scan or photo is rotated by a larger degree or upside down, you must manually specify the rotation angle.
`rotate` | integer | `0` | Rotate an invoice image by the specified degree.<br />Should be used when the image is rotated by a significant angle or turned upside down.
`makeBinarization` | boolean | `false` | Automatically convert an invoice to black and white before proceeding to recognition.
`makeUpsampling` | boolean | `false` | Intellectually upscale an invoice image to improve small font recognition and detection of dense lines.
`makeSpellCheck` | boolean | `false` | Automatically replace commonly misspelled words in recognition results with the correct ones. The dictionary is based on the [selected recognition language](/ocr/supported-languages/).

## Image preprocessing order

If image preprocessing filters are enabled, they are applied one after the other in the following order:

1. [Upsampling](/ocr/upsample-image/#using-the-recognition-setting) (`"makeUpsampling": true`)
2. [Skew correction](/ocr/deskew-image/#using-the-recognition-setting) (`"makeSkewCorrect": true`)

If you want to apply preprocessing filters in another order, disable the corresponding recognition settings and use [self-managed preprocessing](/ocr/preprocess-image/).

## Return value

If successful, this method returns a string with a unique identifier (GUID) of the invoice recognition request in the [queue](/ocr/recognition-workflow/).

Otherwise, it returns a HTTP status code corresponding to the error.

## What's next

Recognition and processing will take a few seconds, depending on the size of the source file and the current Aspose.Cloud load. See the article [Fetching invoice processing result](/ocr/fetch-invoice-recognition-result/) for information on how to get a JSON with parsed invoice data from the server.

## cURL example

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --request POST --location 'https://api.aspose.cloud/v5.0/ocr/RecognizeAndParseInvoice' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA' \
--data-raw '{
  "image": "/9j/4AAQSkZJRgABAQEBLAEsAAD...8AkTf/2Q==",
  "settings": {
    "language": "English",
    "makeSpellCheck": true
  }
}'
```
{{< /tab >}}
{{< tab tabNum="2" >}}
```
39b37b24-86e8-4e91-9a99-6c2574853eb5
```
{{< /tab >}}
{{< /tabs >}}
