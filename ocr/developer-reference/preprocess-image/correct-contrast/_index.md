---
weight: 50
date: "2023-11-27"
author: "Vladimir Lapin"
type: docs
url: /correct-image-contrast/
feedback: OCRCLOUD
title: Contrast correction
description: How to automatically increase image contrast to improve recognition accuracy with Aspose.OCR Cloud API.
keywords:
- contrast
- brightness
- black
- white
- details
---

Low contrast and blurring are the most typical distortions when text is photographed with a smartphone camera, especially in low light conditions. They make it difficult for the OCR algorithms to operate successfully, significantly reducing the recognition accuracy.

Aspose.OCR Cloud can automatically increase the contrast of images before proceeding to recognition. Set the `makeContrastCorrection` recognition setting to `true` to enable the automatic contrast adjustment. This setting is available for all image recognition methods.

{{% alert color="primary" %}} 
You cannot get the preprocessed image as a file.
{{% /alert %}}

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
    "makeContrastCorrection": true,
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
