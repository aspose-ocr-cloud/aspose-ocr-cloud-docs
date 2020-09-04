---
title: "Aspose.OCR for Cloud 20.03 Release Notes"
type: docs
url: /aspose-ocr-for-cloud-20-03-release-notes/
weight: 10
---

{{% alert color="primary" %}} 

The page contains release notes for Aspose.OCR Cloud update 20.3 – [API Reference](https://apireference.aspose.cloud/ocr/)

{{% /alert %}} 
## **Important Changes and New Features**
We are glad to introduce French and German languages support.
#### **API Changes:**
Added optional language selection feature:

```csharp

 static string RecognizeFromContent(Configuration conf)

{

    string name = "10.png";

    using (FileStream fs = File.OpenRead(name))

    {

        OcrApi api = new OcrApi(conf);

        var request = new PostOcrFromUrlOrContentRequest(fs, language: LanguageGroup.German);

        OCRResponse response = api.PostOcrFromUrlOrContent(request);

        return response.Text;

    }

}

```

**Available options:** English, German, French


