---
weight: 30
date: "2023-06-30"
author: "Vladimir Lapin"
type: docs
url: /font-identification-sdk/
feedback: OCRCLOUD
title: Font identification with Aspose.OCR Cloud SDK
description: How to use Aspose.OCR Cloud SDK for identifying fonts in images.
keywords:
- OCR
- recognize
- programming
- development
- SDK
- font
- style
- bold
- italic
- typeface
---

Although you can directly call the Aspose.OCR Cloud REST API to [send image for font identification](/ocr/send-image-for-font-identification/) and [fetch font identification result](/ocr/fetch-font-identification-result/), there is a much easier way to implement font identification functionality in your applications. We provide software development kits (SDKs) for all popular programming languages. They wrap up all routine operations such as establishing connections, sending API requests, and parsing responses into a few simple methods. It makes interaction with Aspose.OCR Cloud services much easier, allowing you to focus on business logic rather than technical details.

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
			IdentifyFontApi fontIdentificationApi = new IdentifyFontApi("<Client Id>", "<Client Secret>");
			/** Read the image to array of bytes */
			byte[] image = File.ReadAllBytes("source.png");
			/** Specify recognition settings */
			OCRSettingsRecognizeFont recognitionSettings = new OCRSettingsRecognizeFont {
				ResultType = ResultType.Text
			};
			/** Send image for font detection */
			OCRRecognizeFontBody source = new OCRRecognizeFontBody(image, recognitionSettings);
			string taskID = fontIdentificationApi.PostIdentifyFont(source);
			/** Fetch recognition result */
			OCRResponse result = fontIdentificationApi.GetIdentifyFont(taskID);
			Console.WriteLine(Encoding.UTF8.GetString(result.Results[0].Data));
		}
	}
}
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-dotnet
{{< /tab >}}

{{< /tabs >}}
