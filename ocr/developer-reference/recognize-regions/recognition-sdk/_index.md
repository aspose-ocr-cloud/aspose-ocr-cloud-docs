---
weight: 30
date: "2023-03-06"
author: "Vladimir Lapin"
type: docs
url: /region-recognition-sdk/
feedback: OCRCLOUD
title: Regions recognition with Aspose.OCR Cloud SDK
description: How to use Aspose.OCR Cloud SDK for extracting text from image regions.
keywords:
- OCR
- recognize
- programming
- development
- SDK
- region
- area
- block
---

Although you can directly call the Aspose.OCR Cloud REST API to [send image regions for recognition](/ocr/send-image-regions-for-recognition/) and [fetch recognition results](/ocr/fetch-region-recognition-result/), there is a much easier way to implement OCR functionality in your applications. We provide software development kits (SDKs) for all popular programming languages. They wrap up all routine operations such as establishing connections, sending API requests, and parsing responses into a few simple methods. It makes interaction with Aspose.OCR Cloud services much easier, allowing you to focus on business logic rather than technical details.

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
			RecognizeRegionsApi api = new RecognizeRegionsApi("<Client Id>", "<Client Secret>");
			/** Read source image to array of bytes */
			byte[] image = File.ReadAllBytes("source.png");
			/** Define regions */
			OCRRegion r1 = new OCRRegion {
				Rect = new OCRRect(0, 0, 300, 100),
				Order = 0
			};
			OCRRegion r2 = new OCRRegion {
				Rect = new OCRRect(0, 200, 300, 250),
				Order = 1
			};
			/** Specify recognition settings */
			OCRSettingsRecognizeRegions settings = new OCRSettingsRecognizeRegions {
				Language = Language.English,
				ResultType = ResultType.Text
			};
			settings.Regions.Add(r1);
			settings.Regions.Add(r2);
			/** Send image for recognition */
			OCRRecognizeRegionsBody source = new OCRRecognizeRegionsBody(image, settings);
			string taskID = api.PostRecognizeRegions(source);
			/** Fetch recognition result */
			OCRResponse result = api.GetRecognizeRegions(taskID);
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
