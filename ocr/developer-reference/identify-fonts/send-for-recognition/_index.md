---
weight: 10
date: "2023-06-27"
author: "Vladimir Lapin"
type: docs
url: /send-image-for-font-identification/
feedback: OCRCLOUD
title: Sending image for font identification
description: How to send a photo or scan for font identification to the Aspose.OCR Cloud API.
keywords:
- OCR
- identify
- queue
- send
- font
- style
- bold
- italic
- typeface
- detect
---

To identify a font in a scan or photo, send a **POST** request to the `https://api.aspose.cloud/v5.0/ocr/IdentifyFont` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

The image and font detection parameters are provided in JSON format in the request body.

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
    "resultType": "Text"
  }
}
```

## Providing an image

Photo or scan is provided in a value of `image` property as a Base64 encoded string.

{{% alert color="caution" %}}
Base64 encoded file can be very long, especially when analyzing scans and high resolution photos. As a result, you may encounter an error when calling font identification via cURL in a shell command. Use the `getconf ARG_MAX` command to check the maximum length of the command arguments (in bytes).
{{% /alert %}}

## Font identification settings

Property | Type | Default&nbsp;value | Description
------- | ---- | ------------- | -----------
`language` | string | `English` | Specify a [language](/ocr/supported-languages/) for font identification.
`makeSkewCorrect` | boolean | `true` | Automatically correct image tilt (deskew) before proceeding to font identification.<br />Automatic deskew works for images rotated 15 degrees or less. If the scan or photo is rotated by a larger degree or upside down, you must manually specify the rotation angle.
`rotate` | integer | `0` | Rotate an image by the specified degree.<br />Should be used when the image is rotated by a significant angle or turned upside down.
`makeBinarization` | boolean | `false` | Automatically convert an image to black and white before proceeding to font identification.
`makeContrastCorrection` | boolean | `true` | Automatically [increase the contrast](/ocr/correct-image-contrast/) of an image before proceeding to font identification.
`makeUpsampling` | boolean | `false` | Intellectually upscale an image to improve small font detection, for example in food labels.
`resultType` | string | `Text` | The result of font identification is always returned as a JSON string, so the value of this parameter must be `Text`.

## Image preprocessing order

If image preprocessing filters are enabled, they are applied one after the other in the following order:

1. [Contrast correction](/ocr/correct-image-contrast/) (`"makeContrastCorrection": true`)
2. [Skew correction](/ocr/deskew-image/#using-the-recognition-setting) (`"makeSkewCorrect": true`)
3. [Upsampling](/ocr/upsample-image/#using-the-recognition-setting) (`"makeUpsampling": true`)

If you want to apply preprocessing filters in another order, disable the corresponding font identification settings and use [self-managed preprocessing](/ocr/preprocess-image/).

## Return value

If successful, this method returns a string with a unique identifier (GUID) of the font identification request in the [queue](/ocr/recognition-workflow/).

Otherwise, it returns a HTTP status code corresponding to the error.

## What's next

Font identification will take a few seconds, depending on the size of the image file and the current Aspose.Cloud load. See the article [Fetching font identification result](/ocr/fetch-font-identification-result/) for information on how to get a font identification result from the server.

## cURL example

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --request POST --location 'https://api.aspose.cloud/v5.0/ocr/IdentifyFont' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA' \
--data-raw '{
  "image": "/9j/4AAQSkZJRgABAgAAZABkAAD...8AkTf/2Q==",
  "settings": {
    "makeSkewCorrect": true,
    "resultType": "Text"
  }
}'
```
{{< /tab >}}
{{< tab tabNum="2" >}}
```
c11c975d-5124-4555-9561-af40fb95ba07
```
{{< /tab >}}
{{< /tabs >}}
