---
weight: 10
date: "2023-05-11"
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

{{% alert color="primary" %}} 
Automatic deskew works for images rotated 15 degrees or less. If the image is rotated by a larger degree or upside down, you must manually specify the rotation angle in recognition settings.
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

## Manual skew correction

When the image is rotated by a significant angle or upside down, automatic skew correction may fail to detect the correct angle.

To deal with such situations, you can manually specify the image rotation angle using the `rotate` recognition setting, which is available for all image recognition methods.

{{% alert color="primary" %}} 
- Manual image rotation can be combined with automatic deskew for best results.
- You cannot get the rotated image as a file.
{{% /alert %}}

### cURL example

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

## Usage scenarios

- Straightening skewed images.
- Turning flipped images.
