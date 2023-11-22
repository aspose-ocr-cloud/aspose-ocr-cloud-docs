---
weight: 10
date: "2023-02-20"
author: "Vladimir Lapin"
type: docs
url: /send-receipt-for-recognition/
feedback: OCRCLOUD
title: Sending receipt for recognition
description: How to send a photo or scan of the receipt for recognition to the Aspose.OCR Cloud API.
keywords:
- OCR
- recognize
- queue
- send
- slip
- check
- statement
---

To extract a text from a scanned or photographed receipt, send a **POST** request to the `https://api.aspose.cloud/v5.0/ocr/RecognizeReceipt` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

The receipt and recognition parameters are provided in JSON format in the request body.

```json
{
  "image": "Base64 string",
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

## Providing a scanned receipt

Photo or scan of the receipt is provided in a value of `image` property as a Base64 encoded string.

{{% alert color="caution" %}}
Base64 encoded file can be very long, especially when recognizing scans and high resolution photos. As a result, you may encounter an error when calling recognition via cURL in a shell command. Use the `getconf ARG_MAX` command to check the maximum length of the command arguments (in bytes).
{{% /alert %}}

## Recognition settings

Property | Type | Default&nbsp;value | Description
------- | ---- | ------------- | -----------
`language` | string | `English` | Specify a [language](/ocr/supported-languages/) for recognition.
`makeSkewCorrect` | boolean | `true` | Automatically correct receipt image tilt (deskew) before proceeding to recognition.<br />Automatic deskew works for images rotated 15 degrees or less. If the scan or photo is rotated by a larger degree or upside down, you must manually specify the rotation angle.
`rotate` | integer | `0` | Rotate a receipt image by the specified degree.<br />Should be used when the image is rotated by a significant angle or turned upside down.
`makeBinarization` | boolean | `false` | Automatically convert a receipt to black and white before proceeding to recognition.
`makeContrastCorrection` | boolean | `true` | Automatically [increase the contrast](/ocr/correct-image-contrast/) of a receipt image before proceeding to recognition.
`makeUpsampling` | boolean | `false` | Intellectually upscale receipt image to improve small font recognition and detection of dense lines.
`makeSpellCheck` | boolean | `false` | Automatically replace commonly misspelled words in recognition results with the correct ones. The dictionary is based on the [selected recognition language](/ocr/supported-languages/).
`dsrMode` | string | `Regions` | [Document structure analysis](/ocr/structure-analysis/) algorithm.
`dsrConfidence` | string | `Default` | [Threshold](/ocr/dsr-confidence/) for filtering content blocks detected by the selected structure analysis algorithm.
`resultType` | string | `Text` | Recognition result [format](/ocr/result-format/).

## Image preprocessing order

If image preprocessing filters are enabled, they are applied one after the other in the following order:

1. [Contrast correction](/ocr/correct-image-contrast/) (`"makeContrastCorrection": true`)
2. [Upsampling](/ocr/upsample-image/#using-the-recognition-setting) (`"makeUpsampling": true`)
3. [Skew correction](/ocr/deskew-image/#using-the-recognition-setting) (`"makeSkewCorrect": true`)

If you want to apply preprocessing filters in another order, disable the corresponding recognition settings and use [self-managed preprocessing](/ocr/preprocess-image/).

## Return value

If successful, this method returns a string with a unique identifier (GUID) of the receipt recognition request in the [queue](/ocr/recognition-workflow/).

Otherwise, it returns a HTTP status code corresponding to the error.

## What's next

Recognition will take a few seconds, depending on the size of the source file and the current Aspose.Cloud load. See the article [Fetching receipt recognition result](/ocr/fetch-receipt-recognition-result/) for information on how to get a receipt recognition result from the server.

## cURL example

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --request POST --location 'https://api.aspose.cloud/v5.0/ocr/RecognizeReceipt' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA' \
--data-raw '{
  "image": "/9j/4AAQSkZJRgABAgAAZABkAAD...8AkTf/2Q==",
  "settings": {
    "language": "English",
    "makeSpellCheck": true,
    "resultType": "Text"
  }
}'
```
{{< /tab >}}
{{< tab tabNum="2" >}}
```
3f030db3-de56-4acb-8469-d696be9dc9a2
```
{{< /tab >}}
{{< /tabs >}}
