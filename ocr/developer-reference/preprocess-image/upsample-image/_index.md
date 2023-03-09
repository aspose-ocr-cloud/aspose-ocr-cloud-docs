---
weight: 30
date: "2023-03-01"
author: "Vladimir Lapin"
type: docs
url: /upsample-image/
feedback: OCRCLOUD
title: Upsampling
description: How to increase the image resolution to improve recognition accuracy with Aspose.OCR Cloud API.
keywords:
- enlarge
- width
- height
- upscale
- scale
---

<style>
	button {
		cursor: pointer;
		margin-right: 20px;
		margin-bottom: 20px;
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

	.duo {
		position: relative;
		width: 500px;
		height: 419px;
		margin-bottom: 20px;
	}

	.duo > img {
		position: absolute;
	}
</style>

The Aspose.OCR Cloud recognition engine can work with images of any size. However, when recognizing very small images, it may ignore some font detail or incorrectly separate dense lines. Straightforward resizing will not help in these situations, as it will mechanically increase the width and height of the image without actually improving the detail.

Aspose.OCR Cloud offers a smart upsampling algorithm that can increase image resolution and enhance the contrast of text details, greatly improving recognition accuracy.

<div class="duo">
	<img src="small-image.png" alt="Small image" />
	<img src="upsampled-image.png" alt="Smart upsampling" style="display: none;" />
</div>
<button onclick="triggerSkew(this)">Upsample image</button>
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
			$(obj).text("Upsample image");
		}
	}
</script>

To intellectually improve the image resolution, send a **POST** request with the image file to the `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/PostUpsamplingImageFile` Aspose.OCR Cloud REST API endpoint or enable `makeUpsampling` property in recognition settings.

## Using the recognition setting

The `makeUpsampling` recognition setting is available for all image recognition methods. To automatically upsample the image during the recognition, simply set this option to `true`.

While this greatly simplifies the code, you have no control over the intermediate results or the order in which the preprocessing filters are applied to the image.

## Using the dedicated endpoint

Posting an image to the Aspose.OCR Cloud endpoint `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/PostUpsamplingImageFile` allows you to [fetch](/ocr/fetch-preprocessed-image/) a preprocessed image that can be handled by other preprocessing filters or recognized. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

The image is provided as a form data.

### Return value

If successful, `PostUpsamplingImageFile` method returns a string with a unique identifier (GUID) of the upsampling request in the [queue](/ocr/recognition-workflow/).

Otherwise, it returns a HTTP status code corresponding to the error.

### What's next

Upsampling will take a few seconds, depending on the image size and the current Aspose.Cloud load. See the article [Fetching preprocessed image](/ocr/fetch-preprocessed-image/) for information on how to get back the image with improved resolution.

### cURL example

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --location --request POST 'https://api.aspose.cloud/v5.0/ocr/ImageProcessing/PostUpsamplingImageFile' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9....X6nACzTQF5OwG5fAuq3u65eyA5vw' \
--form 'file=@"/C:/source.png"'
```
{{< /tab >}}
{{< tab tabNum="2" >}}
```
a69d6a23-f3ae-43b7-9c6a-e30c4d4f8035
```
{{< /tab >}}
{{< /tabs >}}
