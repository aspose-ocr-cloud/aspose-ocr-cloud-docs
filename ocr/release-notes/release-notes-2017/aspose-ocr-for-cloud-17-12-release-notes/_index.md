---
title: "Aspose.OCR for Cloud 17.12 Release Notes"
type: docs
url: /aspose-ocr-for-cloud-17-12-release-notes/
weight: 10
---

{{% alert color="primary" %}} 

The page contains release notes for Aspose.OCR for Cloud update 17.12 – [API Reference](https://apireference.aspose.cloud/ocr/)

{{% /alert %}} 
## **Aspose.OCR for Cloud 17.12 (New version V3)**
We provided our new version based on the most advanced algorithms on neural networks, distributed computing.

Advantages of this algorithm:

- It's faster than V2, mean page processing time is less than 3 seconds
- Excellent recognition results. Mean recognition quality is greater than 97% on text-only samples
- It is based on modern, perspective, scalable cloud architecture

This is the latest version but not yet perfect. It is based on the cutting edge neural networks algorithms, distributed computing and scalable cloud architecture. Unfortunately, it can't do the skew correction and document structure recognition tasks now (until the next release), but provides good results on only-text images, up to 97,7% [1 - ([Levenshtein](https://en.wikipedia.org/wiki/Levenshtein_distance) / Text_Length)]. It's a bit faster than V2 and will be much faster in future.
## **Specification for functions to work with new algorithm**
#### **1. Recognize image using Aspose.Cloud storage**
**REST**

```plain

/ocr/ocrv3/{name}/recognize_v3/?appSid={appSid}&amp;storage={storage}&amp;folder={folder}

```

**Definition in C# SDK**

```csharp

/// <summary>

/// Recognize image using Aspose.Cloud storage.

/// </summary>

/// <param name="name">File name in storage to recognize</param>

/// <param name="storage">Storage identifier</param>

/// <param name="folder">Folder path in cloud storage</param>

/// <returns></returns>

public OCRResponse GetRecognizeDocument(string name, string storage, string folder)

```

**C# API Recognize image method usage example**

```csharp

// Instantiate Aspose Storage Cloud API SDK

StorageApi storageApi = new StorageApi(APIKEY, APPSID, BASEPATH);

// Instantiate Aspose OCR for Cloud API SDK Version_3

OcrV2Api target = new OcrV3Api(APIKEY, APPSID, BASEPATH);

// Set the image file name 

string name = "SampleOCR.bmp";



try

{

	// Upload source file to aspose cloud storage

	storageApi.PutCreate(name, "", "", System.IO.File.ReadAllBytes(name));

	// Invoke Aspose.OCR Cloud SDK API to run OCR task and get Response

	Com.Aspose.OCR.Model.OCRResponse response = target.GetRecognizeDocument(name, storage, folder);



	//Print recognized text for the demonstration

	Console.WriteLine("Recognized Text");	

    Console.WriteLine("-------------------------------------------------");

    Console.WriteLine(actual.Text);

    Console.WriteLine("-------------------------------------------------");

}

catch (Exception ex)

{

	Console.WriteLine("error:" + ex.Message + "\n" + ex.StackTrace);

}

```

**Response JSON**

```javascript

{  

   "ServerStat":{  

      "ServerTime":{  

      },

      "ServerTimespans":{  

      }

   },

   "Text":"This text is the result of OCR process of Aspose.OCR for Cloud v3\n",

   "PartsInfo":null,

   "PagesInfo":null,

   "Code":200,

   "Status":"OK"

}

```
#### **2. Recognize image from URL**
**REST**

```java

/ocr/ocrV3/recognizeV3/?appSid={appSid}&amp;url={url}

```

**Definition in C# SDK**

```java

/// <summary>

/// Recognize image text from some URL if provided or from the request body content (byte array).

/// </summary>

/// <param name="url">URL to download file or the processing</param>

/// <param name="file">File as byte array for the processing</param>

/// <returns></returns>

public OCRResponse PostOcrFromUrlOrContent(string url, byte[] file)

```

**C# API Recognize image method usage example**

```java

// Instantiate Aspose OCR for Cloud API SDK Version_3

OcrV2Api target = new OcrV3Api(APIKEY, APPSID, BASEPATH);

// Set the image file name 

string name = "SampleOCR.bmp";

try

{

	// Read file into byte array

	byte[] file = System.IO.File.ReadAllBytes(name);

	// Invoke Aspose.OCR Cloud SDK API to run OCR task and get Response

	Com.Aspose.OCR.Model.OCRResponse response = target.PostOcrFromUrlOrContent(url, file);



	//Print recognized text for the demonstration

	Console.WriteLine("Recognized Text");	

    Console.WriteLine("-------------------------------------------------");

    Console.WriteLine(actual.Text);

    Console.WriteLine("-------------------------------------------------");

}

catch (Exception ex)

{

	Console.WriteLine("error:" + ex.Message + "\n" + ex.StackTrace);

}

```

**Response JSON**

```javascript

{  

   "ServerStat":{  

      "ServerTime":{  

      },

      "ServerTimespans":{  

      }

   },

   "Text":"This text is the result of OCR process of Aspose.OCR for Cloud v3\n",

   "PartsInfo":null,

   "PagesInfo":null,

   "Code":200,

   "Status":"OK"

}

```
