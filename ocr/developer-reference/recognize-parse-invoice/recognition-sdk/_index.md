---
weight: 30
date: "2023-11-27"
author: "Vladimir Lapin"
type: docs
url: /invoice-recognition-sdk/
feedback: OCRCLOUD
title: Invoice processing with Aspose.OCR Cloud SDK
description: How to use Aspose.OCR Cloud SDK for parsing scanned or photographed invoices.
keywords:
- OCR
- process
- parse
- programming
- development
- SDK
- invoice
---

Although you can directly call the Aspose.OCR Cloud REST API to [send invoices for processing](/ocr/send-invoice-for-recognition/) and [fetch parsed data](/ocr/fetch-invoice-recognition-result/), there is a much easier way to implement OCR functionality in your applications. We provide software development kits (SDKs) for all popular programming languages. They wrap up all routine operations such as establishing connections, sending API requests, and parsing responses into a few simple methods. It makes interaction with Aspose.OCR Cloud services much easier, allowing you to focus on business logic rather than technical details.

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
			RecognizeAndParseInvoiceApi api = new RecognizeAndParseInvoiceApi("<Client Id>", "<Client Secret>");
			/** Read invoice image to array of bytes */
			byte[] invoice = File.ReadAllBytes("invoice.png");
			/** Specify recognition language */
			OCRSettingsRecognizeAndParseInvoice recognitionSettings = new OCRSettingsRecognizeAndParseInvoice {
				Language = Language.English
			};
			/** Send invoice for processing */
			OCRRecognizeAndParseInvoiceBody source = new OCRRecognizeAndParseInvoiceBody(invoice, recognitionSettings);
			string taskID = api.PostRecognizeReceipt(source);
			/** Fetch recognition result */
			OCRResponse result = api.GetRecognizeAndParseInvoice(taskID);
			Console.WriteLine(Encoding.UTF8.GetString(result.Results[0].Data));
		}
	}
}
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-dotnet
{{< /tab >}}

{{< /tabs >}}
