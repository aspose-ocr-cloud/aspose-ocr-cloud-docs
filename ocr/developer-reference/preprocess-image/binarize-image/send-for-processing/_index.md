---
weight: 10
date: "2023-11-27"
author: "Vladimir Lapin"
type: docs
url: /send-image-for-binarization/
feedback: OCRCLOUD
title: Sending image for binarization
description: How to submit an image for binarization with Aspose.OCR Cloud API.
keywords:
- black
- white
- pixel
- binary
- monochrome
- queue
- send
---

## Using the recognition setting

The `makeBinarization` recognition setting is available for all image recognition methods. To automatically binarize the image during the recognition, simply set this option to `true`.

While this greatly simplifies the code, you have no control over the intermediate results or the order in which the preprocessing filters are applied to the image.

## Using the dedicated endpoint

Posting an image to the Aspose.OCR Cloud endpoint `https://api.aspose.cloud/v5.0/ocr/binarizeimage` allows you to [fetch](/ocr/fetch-binarization-result/) a black-and-white image that can be handled by other processing filters or recognized. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

The image is provided in a value of `image` property as a Base64 encoded string.

{{% alert color="caution" %}}
Base64 encoded image can be very long, especially when recognizing scans and high resolution photos. As a result, you may encounter an error when calling recognition via cURL in a shell command. Use the `getconf ARG_MAX` command to check the maximum length of the command arguments (in bytes).
{{% /alert %}}

### Return value

If successful, the endpoint returns a string with a unique identifier (GUID) of the binarization request in the [queue](/ocr/recognition-workflow/).

Otherwise, it returns a HTTP status code corresponding to the error.

### What's next

Binarization will take a few seconds, depending on the image size and the current Aspose.Cloud load. See the article [Fetching binarized image](/ocr/fetch-binarization-result/) for information on how to get back the black-and-white image.

### cURL example

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --request POST --location 'https://api.aspose.cloud/v5.0/ocr/binarizeimage' \
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
5abe66e1-d823-48c1-bcb7-5c05c1719976
```
{{< /tab >}}
{{< /tabs >}}
