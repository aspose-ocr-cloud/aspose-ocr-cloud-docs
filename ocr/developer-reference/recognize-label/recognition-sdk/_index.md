---
weight: 30
date: "2023-06-27"
author: "Vladimir Lapin"
type: docs
url: /label-recognition-sdk/
feedback: OCRCLOUD
title: Label recognition with Aspose.OCR Cloud SDK
description: How to use Aspose.OCR Cloud SDK for extracting text from photographed labels or signs.
keywords:
- OCR
- recognize
- programming
- development
- SDK
- label
- sign
- tag
- picture
- photo
---

Although you can directly call the Aspose.OCR Cloud REST API to [send photographed labels for recognition](/ocr/send-label-for-recognition/) and [fetch label recognition results](/ocr/fetch-label-recognition-result/), there is a much easier way to implement OCR functionality in your applications. We provide software development kits (SDKs) for all popular programming languages. They wrap up all routine operations such as establishing connections, sending API requests, and parsing responses into a few simple methods. It makes interaction with Aspose.OCR Cloud services much easier, allowing you to focus on business logic rather than technical details.

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
			RecognizeLabelApi recognizeLabelApi = new RecognizeLabelApi("<Client Id>", "<Client Secret>");
			/** Read photographed label to array of bytes */
			byte[] image = File.ReadAllBytes("source.png");
			/** Specify recognition settings */
			OCRSettingsRecognizeLabel recognitionSettings = new OCRSettingsRecognizeLabel {
				Language = Language.English,
				ResultType = ResultType.Text
			};
			/** Send photographed label for recognition */
			OCRRecognizeLabelBody source = new OCRRecognizeLabelBody(image, recognitionSettings);
			string taskID = recognizeLabelApi.PostRecognizeLabel(source);
			/** Fetch recognition result */
			OCRResponse result = recognizeLabelApi.GetRecognizeLabel(taskID);
			Console.WriteLine(Encoding.UTF8.GetString(result.Results[0].Data));
		}
	}
}
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-dotnet
{{< /tab >}}

{{< /tabs >}}
