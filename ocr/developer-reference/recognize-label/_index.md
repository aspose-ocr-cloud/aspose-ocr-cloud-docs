---
weight: 75
date: "2023-11-27"
author: "Vladimir Lapin"
type: docs
url: /recognize-label/
feedback: OCRCLOUD
title: Label recognition
description: Extracting the text from signboards, price tags, plates, and other labels using the Aspose.OCR Cloud API.
keywords:
- OCR
- recognize
- image
- picture
- bitmap
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
		height: 227px;
		margin-bottom: 20px;
	}

	.duo > div {
		display: flex;
	}

	.rec-result > pre {
		margin-left: 15px;
		min-width: 222px;
	}
</style>

Aspose.OCR Cloud can read text literally from any source: signboards, price tags, plates, food labels and many more. Almost any photo can be converted into text that can be shared, imported into a database, analyzed, sent for automatic translation, and so on.

<div class="duo">
	<div class="rec-source"><img src="label-source.png" alt="Street photo" /></div>
	<div class="rec-result" style="display: none;">
	<img src="label-regions.png" alt="Recognition result" />
	<pre>
p
within
the
lines
only		
	</pre>
	</div>
</div>
<button onclick="triggerSkew(this)">Read label</button>
<script>
	function triggerSkew(obj)
	{
		let isOrigin = $(".rec-source").is(":visible");
		if(isOrigin)
		{
			$(".rec-source").hide();
			$(".rec-result").show();
			$(obj).text("View original photo");
		}
		else
		{
			$(".rec-source").show();
			$(".rec-result").hide();
			$(obj).text("Read label");
		}
	}
</script>

{{% alert color="caution" %}}
Aspose.OCR Cloud API currently supports label recognition in English only.
{{% /alert %}}

Label texts are extracted in 3 API calls:

1. [Get access token](/ocr/authorization/)
2. [Send photo for recognition](/ocr/send-label-for-recognition/)
3. [Fetch recognition results](/ocr/fetch-label-recognition-result/)

Because Aspose.OCR Cloud is provided as a REST API, label recognition can be performed from any platform with Internet access.

Aspose also provides open-source [SDKs](/ocr/label-recognition-sdk/) for all popular programming languages, that wrap all routine label recognition operations into a few native methods. It makes interaction with Aspose.OCR Cloud services much easier, allowing you to focus on the task at hand rather than technical details.

{{% alert color="primary" %}}
Make sure the application has access to the **api.aspose.cloud** domain.
{{% /alert %}}
