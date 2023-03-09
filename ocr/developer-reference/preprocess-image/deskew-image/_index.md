---
weight: 10
date: "2023-03-01"
author: "Vladimir Lapin"
type: docs
url: /deskew-image/
feedback: OCRCLOUD
title: Skew correction
description: How to straighten a rotated image to improve recognition accuracy with Aspose.OCR Cloud API.
keywords:
- deskew
- straighten
- rotate
- tilt
- skew
- align
---

<style>
	button {
		cursor: pointer;
		margin-right: 20px;
		padding: 7px 15px;
		border: none;
		border-radius: 5px;
		background-color: #1a89d0;
		font-weight: 700;
		font-size: 15px;
		color: #ffffff;
	}

	button:hover {
		background-color: #3071a9;
	}

	button:focus {
		outline: none;
	}

	.code-sample {
		display: flex;
	}

	.code-sample > div {
		display: flex;
		align-items: center;
		padding: 5px 10px;
		border-radius: 5px;
		white-space: nowrap;
		background-color: rgba(0,0,0,5%);
		font-size: 16px;
		font-weight: 700;
	}

	.unseen {
		display: none !important;
	}

	.duo {
		position: relative;
		width: 800px;
		height: 474px;
	}

	.duo > img {
		position: absolute;
	}
</style>

When a page is fed to a flatbed scanner (mechanically or manually) or photographed with a smartphone, it is nearly impossible to achieve perfect alignment. As a result, a slight skew (tilt) inevitably occurs in scanned images or photographs.

Skew angle detection and image straightening is critical to the OCR process as it directly affects the reliability and efficiency of segmentation and text extraction. Aspose.OCR Cloud offers automated processing algorithms to correct image tilt (deskew).

## Automatic skew correction

To automatically straighten skewed image, send a **POST** request with the image file to the `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/PostSkewCorrectionFile` Aspose.OCR Cloud REST API endpoint or enable `makeSkewCorrect` property in recognition settings.

{{% alert color="primary" %}} 
Automatic deskew works for images rotated 15 degrees or less. If the image is rotated by a larger degree or upside down, you must [manually specify the rotation angle](#manual-skew-correction).
{{% /alert %}}

<div class="duo">
	<img src="skew-origin.png" alt="Skewed image" />
	<img src="deskew.png" alt="Deskewed image" style="display: none;" />
</div>
<button onclick="triggerSkew(this)">Automatically deskew image</button>
<script>
	function triggerSkew(obj)
	{
		let images = $(".duo > img");
		let skewed = images.eq(0).is(":visible");
		if(skewed)
		{
			images.eq(1).show(200);
			images.eq(0).hide(200);
			$(obj).text("View original image");
		}
		else
		{
			images.eq(0).show(200);
			images.eq(1).hide(200);
			$(obj).text("Automatically deskew image");
		}
	}
</script>

### Using the recognition setting

The `makeSkewCorrect` recognition setting is available for all image recognition methods. To automatically correct the image tilt during the recognition, simply set this option to `true`.

While this greatly simplifies the code, you have no control over the intermediate results or the order in which the preprocessing filters are applied to the image.

### Using the dedicated endpoint

Posting an image to the Aspose.OCR Cloud endpoint `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/PostSkewCorrectionFile` allows you to [fetch](/ocr/fetch-preprocessed-image/) a preprocessed image that can be handled by other preprocessing filters or recognized. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

The image is provided as a form data.

#### Return value

If successful, `PostSkewCorrectionFile` method returns a string with a unique identifier (GUID) of the deskew request in the [queue](/ocr/recognition-workflow/).

Otherwise, it returns a HTTP status code corresponding to the error.

#### What's next

Skew correction will take a few seconds, depending on the image size and the current Aspose.Cloud load. See the article [Fetching preprocessed image](/ocr/fetch-preprocessed-image/) for information on how to get back the straightened image.

#### cURL example

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --location 'https://api.aspose.cloud/v5.0/ocr/ImageProcessing/PostSkewCorrectionFile' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9....HMTd3btfrc91Q' \
--form 'file=@"/C:/source.png"'
```
{{< /tab >}}
{{< tab tabNum="2" >}}
```
713fc26d-86c0-46e8-b7e2-6420ecadb4e9
```
{{< /tab >}}
{{< /tabs >}}

## Manual skew correction

When the image is rotated by a significant angle or upside down, [automatic skew correction](#automatic-skew-correction) may not detect the correct angle.

To deal with such situations, you can manually specify the image rotation angle using the `rotate` recognition setting, which is available for all image recognition methods.

{{% alert color="primary" %}} 
- Manual image rotation can be combined with automatic deskew for best results.
- You cannot get the rotated image as a file.
{{% /alert %}}

### cURL example

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --location --request POST 'https://api.aspose.cloud/v5.0/ocr/RecognizeImage' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA' \
--data-raw '{
  "image": "iVBORw0KGgoAAAANSUh...d1iEAAAAASUVORK5CYII=",
  "settings": {
    "language": "English",
    "rotate": 90,
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
