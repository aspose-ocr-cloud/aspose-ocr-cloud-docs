---
weight: 10
date: "2023-11-27"
author: "Vladimir Lapin"
type: docs
url: /send-for-detection/
feedback: OCRCLOUD
title: Detecting image regions
description: How to send an image for region detection to the Aspose.OCR Cloud API.
keywords:
- detect
- find
- block
- region
- area
- column
- queue
- send
- image
- picture
- bitmap
---

To detect regions on an image, send a **POST** request to the `https://api.aspose.cloud/v5.0/ocr/DetectRegions` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

The image and detection parameters are provided in JSON format in the request body.

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
    "dsrMode": "Regions",
    "dsrConfidence": "Default"
  }
}
```

## Providing an image

The image is provided in a value of `image` property as a Base64 encoded string.

{{% alert color="caution" %}}
Base64 encoded image can be very long, especially when working with scans and high resolution photos. As a result, you may encounter an error when calling region detection via cURL in a shell command. Use the `getconf ARG_MAX` command to check the maximum length of the command arguments (in bytes).
{{% /alert %}}

## Region detection settings

Property | Type | Default&nbsp;value | Description
------- | ---- | ------------- | -----------
`language` | string | `English` | Specify a language for image text.
`makeSkewCorrect` | boolean | `true` | Automatically [correct image tilt (deskew)](/ocr/deskew-image/) before proceeding to region detection.<br />Automatic deskew works for images rotated 15 degrees or less. If the image is rotated by a larger degree or upside down, you must manually specify the rotation angle.
`rotate` | integer | `0` | [Rotate](/ocr/deskew-image/#manual-skew-correction) an image by the specified degree.<br />Should be used when the image is rotated by a significant angle or turned upside down.
`makeBinarization` | boolean | `false` | Automatically [convert an image to black and white](/ocr/binarize-image/) before proceeding to region detection.
`makeContrastCorrection` | boolean | `true` | Automatically [increase the contrast](/ocr/correct-image-contrast/) of an image before proceeding to region detection.
`makeUpsampling` | boolean | `false` | Intellectually [upscale](/ocr/upsample-image/) image to improve detection of dense lines.
`dsrMode` | string | `Regions` | [Document structure analysis](/ocr/structure-analysis/) algorithm.
`dsrConfidence` | string | `Default` | [Threshold](/ocr/dsr-confidence/) for filtering content blocks detected by the selected structure analysis algorithm.

## Return value

If successful, this method returns a string with a unique identifier (GUID) of the region detection request in the [queue](/ocr/recognition-workflow/).

Otherwise, it returns a HTTP status code corresponding to the error.

## What's next

Region detection will take a few seconds, depending on the size of the image and the current Aspose.Cloud load. See the article [Fetching image regions](/ocr/fetch-regions/) for information on how to get regions from the server.

## cURL example

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --location 'https://api.aspose.cloud/v5.0/ocr/DetectRegions' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...jrfrddlEE4EDlEg' \
--data '{
	"image": "iVBORw0KGgoAAAANSUhEUgAAArgAAAG3CAIAAADQHLEwAAAAGXRFWHRT...FhY8AAAAASUVORK5CYII=",
	"settings": {
		"language": "English",
		"dsrMode": "Regions"
	}
}'
```
{{< /tab >}}
{{< tab tabNum="2" >}}
```
a371d027-4b0d-4d86-8825-c8d818dd4ed9
```
{{< /tab >}}
{{< /tabs >}}
