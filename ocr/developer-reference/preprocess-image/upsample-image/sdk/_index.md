---
weight: 30
date: "2023-05-11"
author: "Vladimir Lapin"
type: docs
url: /upsampling-sdk/
feedback: OCRCLOUD
title: Image upsampling with Aspose.OCR Cloud SDK
description: How to use Aspose.OCR Cloud SDK for upsampling an image.
keywords:
- enlarge
- width
- height
- upscale
- scale
- programming
- development
- SDK
---

Although you can directly call the Aspose.OCR Cloud REST API to [submit](/ocr/send-image-for-upsampling/#using-the-dedicated-endpoint) an image for upscaling and [fetch the resized image](/ocr/fetch-upsampling-result/), there is a much easier way to implement OCR functionality in your applications. We provide software development kits (SDKs) for all popular programming languages. They wrap up all routine operations such as establishing connections, sending API requests, and parsing responses into a few simple methods. It makes interaction with Aspose.OCR Cloud services much easier, allowing you to focus on business logic rather than technical details.

{{< tabs tabID="1" tabTotal="1" tabName1=".NET" >}}

{{< tab tabNum="1" >}}
```csharp
using Aspose.OCR.Cloud.SDK.Api;
using Aspose.OCR.Cloud.SDK.Model;
using System.Text;

namespace Example
{
	internal class Program
	{
		static void Main(string[] args)
		{
			/** Authorize your requests to Aspose.OCR Cloud API */
			UpscaleImageApi api = new UpscaleImageApi("<Client Id>", "<Client Secret>");
			/** Read source image to array of bytes */
			byte[] image = File.ReadAllBytes("source.png");
			/** Send image for upsampling */
			OCRUpscaleImageBody source = new OCRUpscaleImageBody(image);
			string taskID = api.PostUpscaleImage(source);
			/** Fetch resized image */
			var result = api.GetUpscaleImage(taskID);
			/** Save preprocessed image to file */
			byte[] imageFileData = result.Results[0].Data;
			File.WriteAllBytes("result.png", imageFileData);
		}
	}
}
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-dotnet
{{< /tab >}}

{{< /tabs >}}
