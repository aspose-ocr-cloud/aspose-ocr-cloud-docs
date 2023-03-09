---
weight: 10
date: "2023-02-20"
author: "Vladimir Lapin"
type: docs
url: /send-pdf-for-recognition/
feedback: OCRCLOUD
title: Sending PDF for recognition
description: How to send a scanned PDF document for recognition to the Aspose.OCR Cloud API.
keywords:
- OCR
- recognize
- queue
- send
- PDF
- document
---

To extract a text from a scanned PDF, send a **POST** request to the `https://api.aspose.cloud/v5.0/ocr/RecognizePdf` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

The PDF file and recognition parameters are provided in JSON format in the request body.

```json
{
  "image": "PDF as Base64 string",
  "settings": {
    "language": "English",
    "makeSkewCorrect": true,
    "rotate": 0,
    "makeBinarization": false,
    "makeContrastCorrection": true,
    "makeUpsampling": false,
    "makeSpellCheck": false,
    "dsrMode": "Regions",
    "dsrConfidence": "Default",
    "resultType": "Text"
  }
}
```

## Providing an scanned PDF

The PDF file is provided in a value of `image` property as a Base64 encoded string.

{{% alert color="caution" %}}
Base64 encoded PDF can be very long, especially when recognizing scans and high resolution photos. As a result, you may encounter an error when calling recognition via cURL in a shell command. Use the `getconf ARG_MAX` command to check the maximum length of the command arguments (in bytes).
{{% /alert %}}

## Recognition settings

{{% alert color="primary" %}}
Preprocessing filters (such as rotation and upsampling) configured in recognition settings are applied to each page of the source PDF document.
{{% /alert %}}

Property | Type | Default&nbsp;value | Description
------- | ---- | ------------- | -----------
`language` | string | `English` | Specify a [language](/ocr/supported-languages/) for recognition.
`makeSkewCorrect` | boolean | `true` | Automatically correct page tilt (deskew) before proceeding to recognition.<br />Automatic deskew works for pages rotated 15 degrees or less. If the page is rotated by a larger degree or upside down, you must manually specify the rotation angle.
`rotate` | integer | `0` | Rotate a page by the specified degree.<br />Should be used when the page is rotated at a significant angle, such as landscape or upside down.
`makeBinarization` | boolean | `false` | Automatically convert page content to black and white before proceeding to recognition.
`makeContrastCorrection` | boolean | `true` | Automatically [increase the contrast](/ocr/correct-image-contrast/) of images on a page before proceeding to recognition.
`makeUpsampling` | boolean | `false` | Intellectually upscale page content to improve small font recognition and detection of dense lines.
`makeSpellCheck` | boolean | `false` | Automatically replace commonly misspelled words in recognition results with the correct ones. The dictionary is based on the [selected recognition language](/ocr/supported-languages/).
`dsrMode` | string | `Regions` | [Document structure analysis](/ocr/structure-analysis/) algorithm.
`dsrConfidence` | string | `Default` | [Threshold](/ocr/dsr-confidence/) for filtering content blocks detected by the selected structure analysis algorithm.
`resultType` | string | `Text` | Recognition result [format](/ocr/result-format/).

## Return value

If successful, this method returns a string with a unique identifier (GUID) of the PDF recognition request in the [queue](/ocr/recognition-workflow/).

Otherwise, it returns a HTTP status code corresponding to the error.

## What's next

Recognition will take a few seconds, depending on the size of the PDF document and the current Aspose.Cloud load. See the article [Fetching PDF recognition result](/ocr/fetch-pdf-recognition-result/) for information on how to get a recognition result from the server.

## cURL example

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --location --request POST 'https://api.aspose.cloud/v5.0/ocr/RecognizePdf' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA' \
--data-raw '{
  "image": "JVBERi0xLjUNJeLjz9...g0xMTYNJSVFT0YN",
  "settings": {
    "language": "English",
    "makeSpellCheck": true,
    "resultType": "Pdf"
  }
}'
```
{{< /tab >}}
{{< tab tabNum="2" >}}
```
db03b9ea-3eed-4954-a1d4-b2712773bbe
```
{{< /tab >}}
{{< /tabs >}}
