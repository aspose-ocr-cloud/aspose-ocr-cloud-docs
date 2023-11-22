---
weight: 10
date: "2023-06-27"
author: "Vladimir Lapin"
type: docs
url: /send-label-for-recognition/
feedback: OCRCLOUD
title: Sending label for recognition
description: How to send a photographed label or sign for recognition to the Aspose.OCR Cloud API.
keywords:
- OCR
- recognize
- queue
- send
- label
- sign
- tag
- picture
- photo
---

To extract a text from a photographed label, send a **POST** request to the `https://api.aspose.cloud/v5.0/ocr/RecognizeLabel` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

The photo and recognition parameters are provided in JSON format in the request body.

```json
{
  "image": "Base64 string",
  "settings": {
    "language": "English",
    "makeSkewCorrect": true,
    "makeUpsampling": false,
    "resultType": "Text"
  }
}
```

## Providing an image

The photographed label is provided in a value of `image` property as a Base64 encoded string.

{{% alert color="caution" %}}
Base64 string encoded from a modern smartphone photo can be very long (millions of characters). As a result, you may encounter an error when calling recognition via cURL in a shell command. Use the `getconf ARG_MAX` command to check the maximum length of the command arguments (in bytes).
{{% /alert %}}

## Recognition settings

Property | Type | Default&nbsp;value | Description
------- | ---- | ------------- | -----------
`language` | string | `English` | Specify a [language](/ocr/supported-languages/) for recognition. At the moment, `English` is the only supported option.
`makeSkewCorrect` | boolean | `true` | Automatically [correct image tilt (deskew)](/ocr/deskew-image/) before proceeding to recognition.
`makeUpsampling` | boolean | `false` | Intellectually [upscale](/ocr/upsample-image/) image to improve small font recognition and detection of dense lines.
`resultType` | string | `Text` | Recognition result [format](/ocr/result-format/).

## Image preprocessing order

If image preprocessing filters are enabled, they are applied one after the other in the following order:

1. [Skew correction](/ocr/deskew-image/#using-the-recognition-setting) (`"makeSkewCorrect": true`)
2. [Upsampling](/ocr/upsample-image/#using-the-recognition-setting) (`"makeUpsampling": true`)

If you want to apply preprocessing filters in another order, disable the corresponding recognition settings and use [self-managed preprocessing](/ocr/preprocess-image/).

## Return value

If successful, this method returns a string with a unique identifier (GUID) of the label recognition request in the [queue](/ocr/recognition-workflow/).

Otherwise, it returns a HTTP status code corresponding to the error.

## What's next

Recognition will take a few seconds, depending on the size of the photo and the current Aspose.Cloud load. See the article [Fetching label recognition result](/ocr/fetch-label-recognition-result/) for information on how to get a label recognition result from the server.

## cURL example

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --request POST --location 'https://api.aspose.cloud/v5.0/ocr/RecognizeLabel' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA' \
--data-raw '{
  "image": "iVBORw0KGgoAAAANSUh...d1iEAAAAASUVORK5CYII=",
  "settings": {
    "language": "English",
    "makeSkewCorrect": true,
    "resultType": "Text"
  }
}'
```
{{< /tab >}}
{{< tab tabNum="2" >}}
```
a197aade-bba9-4c7a-92c7-46851b3dceaa
```
{{< /tab >}}
{{< /tabs >}}
