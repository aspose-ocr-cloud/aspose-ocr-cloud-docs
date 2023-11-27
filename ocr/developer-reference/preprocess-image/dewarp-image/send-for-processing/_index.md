---
weight: 10
date: "2023-11-27"
author: "Vladimir Lapin"
type: docs
url: /send-image-for-dewarp/
feedback: OCRCLOUD
title: Sending image for dewarping
description: How to submit an image for dewarping with Aspose.OCR Cloud API.
keywords:
- correct
- distort
- curve
- photo
- book
- fisheye
- queue
- send
---

Posting an image to the Aspose.OCR Cloud endpoint `https://api.aspose.cloud/v5.0/ocr/dewarpimage` allows you to [fetch](/ocr/fetch-dewarp-result/) a dewarped image that can be handled by other processing filters or recognized. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

The image is provided in a value of `image` property as a Base64 encoded string.

{{% alert color="caution" %}}
Base64 encoded image can be very long, especially when recognizing scans and high resolution photos. As a result, you may encounter an error when calling recognition via cURL in a shell command. Use the `getconf ARG_MAX` command to check the maximum length of the command arguments (in bytes).
{{% /alert %}}

## Return value

If successful, the endpoint returns a string with a unique identifier (GUID) of the dewarping request in the [queue](/ocr/recognition-workflow/).

Otherwise, it returns a HTTP status code corresponding to the error.

## What's next

Dewarping will take a few seconds, depending on the image size and the current Aspose.Cloud load. See the article [Fetching dewarped image](/ocr/fetch-dewarp-result/) for information on how to get back the dewarped image.

## cURL example

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --request POST --location 'https://api.aspose.cloud/v5.0/ocr/dewarpimage' \
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
