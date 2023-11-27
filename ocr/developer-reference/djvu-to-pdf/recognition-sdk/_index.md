---
weight: 30
date: "2023-11-27"
author: "Vladimir Lapin"
type: docs
url: /djvu-conversion-sdk/
feedback: OCRCLOUD
title: DjVu to PDF conversion with Aspose.OCR Cloud SDK
description: How to use Aspose.OCR Cloud SDK for converting DjVu file to a PDF document.
keywords:
- OCR
- convert
- programming
- development
- SDK
- DjVu
- PDF
---

Although you can directly call the Aspose.OCR Cloud REST API to [send DjVu for conversion](/ocr/send-djvu-for-conversion/) and [fetch a PDF document](/ocr/fetch-djvu-conversion-result/), there is a much easier way to implement OCR functionality in your applications. We provide software development kits (SDKs) for all popular programming languages. They wrap up all routine operations such as establishing connections, sending API requests, and parsing responses into a few simple methods. It makes interaction with Aspose.OCR Cloud services much easier, allowing you to focus on business logic rather than technical details.

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
			DjVu2PDFApi api = new DjVu2PDFApi("<Client Id>", "<Client Secret>");
			/** Read source DjVu file to array of bytes */
			byte[] image = File.ReadAllBytes("source.djvu");
			/** Specify conversion settings */
			OCRSettingsDjVu2PDF conversionSettings = new OCRSettingsDjVu2PDF();
			/** Send DjVu for conversion */
			OCRDjVu2PDFBody source = new OCRDjVu2PDFBody(image, conversionSettings);
			string taskID = api.PostDjVu2PDF(source);
			/** Save PDF */
			OCRResponse result = api.GetDjVu2PDF(taskID);
			byte[] imageFileData = result.Results[0].Data;
			File.WriteAllBytes("result.pdf", imageFileData);
		}
	}
}
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-dotnet
{{< /tab >}}

{{< /tabs >}}
