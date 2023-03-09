---
weight: 70
date: "2023-03-01"
author: "Vladimir Lapin"
type: docs
url: /preprocessing-sdk/
feedback: OCRCLOUD
title: Image preprocessing with Aspose.OCR Cloud SDK
description: How to use Aspose.OCR Cloud SDK for preprocessing images.
keywords:
- preprocess
- programming
- development
- SDK
---

Although you can directly call the Aspose.OCR Cloud REST API to preprocess images and fetch them as files, there is a much easier way to implement this functionality in your applications. We provide software development kits (SDKs) for all popular programming languages. They wrap up all routine operations such as establishing connections, sending API requests, and parsing responses into a few simple methods. It makes interaction with Aspose.OCR Cloud services much easier, allowing you to focus on business logic rather than technical details.

{{< tabs tabID="1" tabTotal="1" tabName1=".NET" >}}

{{< tab tabNum="1" >}}
```csharp
using Aspose.OCR.Cloud.SDK.Api;

namespace Example
{
	internal class Program
	{
		static void Main(string[] args)
		{
			/** Authorize your requests to Aspose.OCR Cloud API */
			ImageProcessingApi api = new ImageProcessingApi("<Client Id>", "<Client Secret>");
			using(FileStream fileStream = new FileStream("source.png", FileMode.Open, FileAccess.Read))
			{
				/** Send image for preprocessing */
				string taskID = api.PostDewarpingFile(fileStream);
				/** Fetch preprocessed image */
				var result = api.GetResultTask(taskID);
				/** Save preprocessed image to file */
				byte[] imageFileData = result.Results[0].Data;
				File.WriteAllBytes($"result.png", imageFileData);
			}
		}
	}
}
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-dotnet
{{< /tab >}}

{{< /tabs >}}
