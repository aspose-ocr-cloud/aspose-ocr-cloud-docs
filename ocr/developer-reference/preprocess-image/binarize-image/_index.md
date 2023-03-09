---
weight: 40
date: "2023-03-01"
author: "Vladimir Lapin"
type: docs
url: /binarize-image/
feedback: OCRCLOUD
title: Binarization
description: How to convert an image to black and white to improve recognition accuracy with Aspose.OCR Cloud API.
keywords:
- black
- white
- pixel
- binary
- monochrome
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
		width: 600px;
		height: 324px;
		margin-bottom: 20px;
	}

	.duo > img {
		position: absolute;
	}
</style>

Although you can extract text from color scans or photographs, text recognition and area detection gives better results with black and white images. The conversion to black and white is called _binarization_.

Aspose.OCR Cloud can automatically convert images to black and white without losing the details required for recognition. Moreover, it can intellectually remove text background, color noise, and other unnecessary data.

<div class="duo">
	<img src="color-image.png" alt="Colored image" />
	<img src="binarized-image.png" alt="Monochrome image" style="display: none;" />
</div>
<button onclick="triggerSkew(this)">Binarize image</button>
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
			$(obj).text("Binarize image");
		}
	}
</script>

To convert the image to black and white, send a **POST** request with the image file to the `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/PostBinarizationFile` Aspose.OCR Cloud REST API endpoint or enable `makeBinarization` property in recognition settings.

## Using the recognition setting

The `makeBinarization` recognition setting is available for all image recognition methods. To automatically binarize the image during the recognition, simply set this option to `true`.

While this greatly simplifies the code, you have no control over the intermediate results or the order in which the preprocessing filters are applied to the image.

## Using the dedicated endpoint

Posting an image to the Aspose.OCR Cloud endpoint `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/PostBinarizationFile` allows you to [fetch](/ocr/fetch-preprocessed-image/) a preprocessed image that can be handled by other preprocessing filters or recognized. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

The image is provided as a form data.

### Return value

If successful, `PostBinarizationFile` method returns a string with a unique identifier (GUID) of the binarization request in the [queue](/ocr/recognition-workflow/).

Otherwise, it returns a HTTP status code corresponding to the error.

### What's next

Binarization will take a few seconds, depending on the image size and the current Aspose.Cloud load. See the article [Fetching preprocessed image](/ocr/fetch-preprocessed-image/) for information on how to get back the black-and-white image.

### cURL example

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --location --request POST 'https://api.aspose.cloud/v5.0/ocr/ImageProcessing/PostBinarizationFile' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...PITajhQfa-31HNq2A' \
--form 'file=@"/C:/source.png"'
```
{{< /tab >}}
{{< tab tabNum="2" >}}
```
5abe66e1-d823-48c1-bcb7-5c05c1719976
```
{{< /tab >}}
{{< /tabs >}}
