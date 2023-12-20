---
weight: 10
date: "2023-12-20"
author: "Vladimir Lapin"
type: docs
url: /send-image-for-recognition/
feedback: OCRCLOUD
title: Sending image for recognition
description: How to send an image for recognition to the Aspose.OCR Cloud API.
keywords:
- OCR
- recognize
- queue
- send
- image
- picture
- bitmap
---

To extract a text from an [image](/ocr/supported-file-formats/), send a **POST** request to the `https://api.aspose.cloud/v5.0/ocr/RecognizeImage` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

The image and recognition parameters are provided in JSON format in the request body.

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

## Evaluation mode

To use Aspose.OCR Cloud image recognition in [evaluation mode](/ocr/subscription/#evaluation-tier), send a POST request to the endpoint `https://api.aspose.cloud/v5.0/ocr/RecognizeImageTrial`.

This endpoint does not use the **Authorization** header, so there is no need to generate an access token. All settings remain the same as in regular image recognition requests.

## Providing an image

The image is provided in a value of `image` property as a Base64 encoded string.

{{% alert color="caution" %}}
Base64 encoded image can be very long, especially when recognizing scans and high resolution photos. As a result, you may encounter an error when calling recognition via cURL in a shell command. Use the `getconf ARG_MAX` command to check the maximum length of the command arguments (in bytes).
{{% /alert %}}

## Recognition settings

Property | Type | Default&nbsp;value | Description
------- | ---- | ------------- | -----------
`language` | string | `English` | Specify a [language](/ocr/supported-languages/) for recognition.
`makeSkewCorrect` | boolean | `true` | Automatically [correct image tilt (deskew)](/ocr/deskew-image/) before proceeding to recognition.<br />Automatic deskew works for images rotated 15 degrees or less. If the image is rotated by a larger degree or upside down, you must manually specify the rotation angle.
`rotate` | integer | `0` | [Rotate](/ocr/deskew-image/#manual-skew-correction) an image by the specified degree.<br />Should be used when the image is rotated by a significant angle or turned upside down.
`makeBinarization` | boolean | `false` | Automatically [convert an image to black and white](/ocr/binarize-image/) before proceeding to recognition.
`makeContrastCorrection` | boolean | `true` | Automatically [increase the contrast](/ocr/correct-image-contrast/) of an image before proceeding to recognition.
`makeUpsampling` | boolean | `false` | Intellectually [upscale](/ocr/upsample-image/) image to improve small font recognition and detection of dense lines.
`makeSpellCheck` | boolean | `false` | Automatically replace commonly misspelled words in recognition results with the correct ones. The dictionary is based on the [selected recognition language](/ocr/supported-languages/).
`dsrMode` | string | `Regions` | [Document structure analysis](/ocr/structure-analysis/) algorithm.
`dsrConfidence` | string | `Default` | [Threshold](/ocr/dsr-confidence/) for filtering content blocks detected by the selected structure analysis algorithm.
`resultType` | string | `Text` | Recognition result [format](/ocr/result-format/).

## Image preprocessing order

If image preprocessing filters are enabled, they are applied one after the other in the following order:

1. [Contrast correction](/ocr/correct-image-contrast/) (`"makeContrastCorrection": true`)
2. [Binarization](/ocr/binarize-image/#using-the-recognition-setting) (`"makeBinarization": true`)
3. [Skew correction](/ocr/deskew-image/#using-the-recognition-setting) (`"makeSkewCorrect": true`)
4. [Upsampling](/ocr/upsample-image/#using-the-recognition-setting) (`"makeUpsampling": true`)

If you want to apply preprocessing filters in another order, disable the corresponding recognition settings and use [self-managed preprocessing](/ocr/preprocess-image/).

## Return value

If successful, this method returns a string with a unique identifier (GUID) of the image recognition request in the [queue](/ocr/recognition-workflow/).

Otherwise, it returns a HTTP status code corresponding to the error.

## What's next

Recognition will take a few seconds, depending on the size of the image and the current Aspose.Cloud load. See the article [Fetching image recognition result](/ocr/fetch-image-recognition-result/) for information on how to get an image recognition result from the server.

## cURL example

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --request POST --location 'https://api.aspose.cloud/v5.0/ocr/RecognizeImage' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA' \
--data-raw '{
  "image": "iVBORw0KGgoAAAANSUh...d1iEAAAAASUVORK5CYII=",
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
a197aade-bba9-4c7a-92c7-46851b3dceaa
```
{{< /tab >}}
{{< /tabs >}}
