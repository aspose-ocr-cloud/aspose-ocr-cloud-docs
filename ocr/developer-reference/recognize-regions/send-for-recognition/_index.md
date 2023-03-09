---
weight: 10
date: "2023-03-06"
author: "Vladimir Lapin"
type: docs
url: /send-image-regions-for-recognition/
feedback: OCRCLOUD
title: Sending image regions for recognition
description: How to extract text from the predetermined image regions in ASPOSE.OCR Cloud API.
keywords:
- OCR
- recognize
- queue
- send
- region
- area
- block
---

Aspose.OCR Cloud allows you to extract names, dates, numbers, and other blocks from certain areas of uniform images, such as ID cards, visas, driver’s licenses, applications, and so on. Regions can be provided manually or [automatically detected](/ocr/detect-regions/) from an image.

To extract a text from one or more areas of an image, send a **POST** request to the `https://api.aspose.cloud/v5.0/ocr/RecognizeRegions` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

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
    "resultType": "Text",
    "regions": [
      {
        "rect": {
          "topLeftX": 0,
          "topLeftY": 0,
          "bottomRightX": 300,
          "bottomRightY": 100
        },
        "order": 0
      }
    ]
  }
}
```

## Providing an image

The image is provided in a value of `image` property as a Base64 encoded string.

{{% alert color="caution" %}}
Base64 encoded image can be very long, especially when recognizing scans and high resolution photos. As a result, you may encounter an error when calling recognition via cURL in a shell command. Use the `getconf ARG_MAX` command to check the maximum length of the command arguments (in bytes).
{{% /alert %}}

## Specifying regions

Regions are provided as an array of objects in `regions` property. For each region, the following properties must be provided:

- `rect` - image area, defined by the coordinates of its top-left and bottom-right corners (in pixels).
- `order` - relative recognition priority of a region. The higher the number, the further the region's text will be placed in the recognition result.

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
`resultType` | string | `Text` | Recognition results format. All region recognition results will be of the same type.

## Return value

If successful, this method returns a string with a unique identifier (GUID) of the image recognition request in the [queue](/ocr/recognition-workflow/).

Otherwise, it returns a HTTP status code corresponding to the error.

## What's next

Recognition will take a few seconds, depending on the size of the image and the current Aspose.Cloud load. See the article [Fetching region recognition result](/ocr/fetch-region-recognition-result/) for information on how to get an image recognition result from the server.

## cURL example

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --location --request POST 'https://api.aspose.cloud/v5.0/ocr/RecognizeRegions' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...y6HFO2W3iuX5XvtpjVA5FtYA' \
--data '{
	"image": "iVBORw0KGgoAAAANSUhEUgAAAboAAAA/CAIAAAAZ...AgwAK2nACOid1iEAAAAASUVORK5CYII=",
	"settings": {
		"language": "English",
		"resultType": "Text",
		"regions": [
			{
				"order": 0,
				"rect": {
					"topLeftX": 21,
					"topLeftY": 24,
					"bottomRightX": 414,
					"bottomRightY": 43
				}
			}
		]
	}
}'
```
{{< /tab >}}
{{< tab tabNum="2" >}}
```
b7162f77-bf10-407d-86de-ee255e422ca7
```
{{< /tab >}}
{{< /tabs >}}
