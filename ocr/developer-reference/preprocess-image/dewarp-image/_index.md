---
weight: 20
date: "2023-05-11"
author: "Vladimir Lapin"
type: docs
url: /dewarp-image/
feedback: OCRCLOUD
title: Dewarping
description: How to straighten curved and distorted images before recognition to improve recognition accuracy with Aspose.OCR Cloud API.
keywords:
- correct
- distort
- curve
- photo
- book
- fisheye
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
		height: 454px;
		margin-bottom: 20px;
	}

	.duo > img {
		position: absolute;
	}
</style>

Geometric distortions is a very common case when dealing with photos of books, magazines, multi-page documents, and similar content. They can be caused by physical page curvature or camera lens distortion (ultra-wide and fisheye lenses, as well as entry-level smartphone lenses).

Warped images are very hard to be processed by most OCR algorithms. Thus, image straightening and distortion removal is critical to the recognition process as it directly affects the reliability and efficiency of segmentation and text extraction. Aspose.OCR Cloud has a preprocessing filter for automated correction of geometric image distortions.

<div class="duo">
	<img src="warped-page.png" alt="Curved page photo" />
	<img src="dewarped-page.png" alt="Dewarped image" style="display: none;" />
</div>
<button onclick="triggerSkew(this)">Dewarp image</button>
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
			$(obj).text("Automatically dewarp image");
		}
	}
</script>

## Usage scenarios

- Straightening lines in curved pages.
- Fixing geometric distortions on ultra-wide or fisheye photos.
