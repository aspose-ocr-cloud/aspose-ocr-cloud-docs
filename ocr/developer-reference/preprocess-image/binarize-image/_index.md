---
weight: 40
date: "2023-05-11"
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

## Usage scenarios

- Increase the contrast of photographed texts.
- Significantly reduce the size of color images.
