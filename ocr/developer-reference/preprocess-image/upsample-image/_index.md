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

## Usage scenarios

- Increasing text size on medication guides or food labels.
- Improving readability of small images or photos.
