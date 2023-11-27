---
weight: 30
date: "2023-11-27"
author: "Vladimir Lapin"
type: docs
url: /region-detection-sdk/
feedback: OCRCLOUD
title: Region detection with Aspose.OCR Cloud SDK
description: How to use Aspose.OCR Cloud SDK for detecting image regions.
keywords:
- detect
- find
- block
- region
- area
- column
- programming
- development
- SDK
- image
- picture
- bitmap
---

Although you can directly call the Aspose.OCR Cloud REST API to [detect](/ocr/send-for-detection/) and [fetch](/ocr/fetch-regions/) regions, there is a much easier way to implement image region detection functionality in your applications. We provide software development kits (SDKs) for all popular programming languages. They wrap up all routine operations such as establishing connections, sending API requests, and parsing responses into a few simple methods. It makes interaction with Aspose.OCR Cloud services much easier, allowing you to focus on business logic rather than technical details.

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
			DetectRegionsApi api = new DetectRegionsApi("<Client Id>", "<Client Secret>");
			/** Read source image to array of bytes */
			byte[] image = File.ReadAllBytes("source.png");
			/** Specify region detection settings */
			OCRSettingsDetectRegions settings = new OCRSettingsDetectRegions {
				Language = Language.English,
				DsrMode = DsrMode.Regions
			};
			/** Send image for regions detection */
			OCRDetectRegionsBody source = new OCRDetectRegionsBody(image, settings);
			string taskID = api.PostDetectRegions(source);
			/** Fetch regions */
			OCRResponse result = api.GetDetectRegions(taskID);
			foreach(var region in result.Results)
			{
				Console.WriteLine(Encoding.UTF8.GetString(region.Data));
			}
		}
	}
}
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-dotnet
{{< /tab >}}

{{< /tabs >}}
