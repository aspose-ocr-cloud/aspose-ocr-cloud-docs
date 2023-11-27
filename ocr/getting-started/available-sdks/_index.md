---
weight: 50
date: "2023-11-27"
author: "Vladimir Lapin"
type: docs
url: /available-sdks/
feedback: OCRCLOUD
title: Available SDKs
description: Find the latest software development kits (SDKs) that help you easily integrate Aspose.OCR Cloud into your applications.
keywords:
- .NET
- Java
- Python
- Android
- programming
- SDK
---

Aspose offers software development kits (SDKs) for popular programming languages that make interaction with Aspose.OCR cloud services much easier. It allows you to focus on business logic rather than the technical details.

SDKs handle all the routine operations such as establishing connections, sending API requests, and parsing responses, wrapping all these tasks into a few simple methods. The following programming languages are supported:

- [Aspose.OCR Cloud for .NET](https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-dotnet)  
  Use optical character recognition in any on-premise and web-based .NET application.
- [Aspose.OCR Cloud for Java](https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-java)  
  Call Aspose.OCR Cloud API from cross-platform Java apps.
- [Aspose.OCR Cloud for Python](https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-python)  
  Natively integrate OCR features into Python applications.
- [Aspose.OCR Cloud for Node.js](https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-nodejs)  
  Add OCR functionality to AWS Lambda, Azure Functions, services, and applications written in Node.js by querying our REST API.
- [Aspose.OCR Cloud for Android](https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-android)  
  Turn a smartphone into a full featured OCR scanner. Aspose.OCR service runs in the cloud and supports even entry-level and legacy smartphones.
- [Aspose.OCR Cloud for Go](https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-go)  
  Allow your Go applications to extract text from images, read street photos, and many more.

All SDKs are open-source distributed under [MIT License](https://opensource.org/licenses/MIT). You can freely use them for any projects, including commercial and proprietary applications, as well as modify any part of the code.

The provided code is fully tested and ready to run out of the box.

## SDK usage examples

See the examples below for a quick overview of how SDKs can make your development easier.

{{< tabs tabTotal="5" tabID="4" tabName1="C#" tabName2="Java" tabName3="Python" tabName4="Android" tabName5="Go" >}}

{{< tab tabNum="1" >}}

{{< gist "aspose-cloud" "0f9e9de5290f0fcdfd93517225f2b66a" "Example-RecognizeFromStorage.cs" >}}

{{< /tab >}}

{{< tab tabNum="2" >}}

{{< gist "aspose-cloud" "723802ba0a961dac4b73a96f1932469c" "Example-RecognizeFromStorage.java" >}}

{{< /tab >}}

{{< tab tabNum="3" >}}

{{< gist "aspose-cloud" "806422f52a90ff15bbfcd268b91184a9" "RecognizeFromStorage.py" >}}

{{< /tab >}}

{{< tab tabNum="4" >}}

{{< gist "aspose-cloud" "7a771d5fa2f6ac367708ab42b9740d71" "Example-RecognizeFromStorage.java" >}}

{{< /tab >}}

{{< tab tabNum="5" >}}

```go
package main

import (
	"context"
	"encoding/base64"
	"fmt"
	"io/ioutil"

	asposeocrcloud "github.com/aspose-ocr-cloud/aspose-ocr-cloud-go"
)

func main() {

	clientId := "YOUR_CLIENT_ID"
	clientSecret := "YOUR_CLIENT_SECRET"
	configuration := asposeocrcloud.NewConfiguration(clientId, clientSecret)
	apiClient := asposeocrcloud.NewAPIClient(configuration)

	filePath := "../samples/latin.png" // Path to your file

	// Read your file data and convert it into base64 string
	fileBytes, err := ioutil.ReadFile(filePath)
	if err != nil || fileBytes == nil {
		fmt.Println("Read file error:", err)
		return
	}
	fileb64Encoded := base64.StdEncoding.EncodeToString(fileBytes)

	// Step 1: create request body and sent it to OCR Cloud to receive task ID
	recognitionSettings := *asposeocrcloud.NewOCRSettingsRecognizeImage()
	recognitionSettings.Language = asposeocrcloud.LANGUAGE_ENGLISH.Ptr()
	recognitionSettings.DsrMode = asposeocrcloud.DSRMODE_NO_DSR_NO_FILTER.Ptr()
	recognitionSettings.DsrConfidence = asposeocrcloud.DSRCONFIDENCE_DEFAULT.Ptr()
	*recognitionSettings.MakeBinarization = false
	*recognitionSettings.MakeSkewCorrect = false
	*recognitionSettings.MakeUpsampling = false
	*recognitionSettings.MakeSpellCheck = false
	*recognitionSettings.MakeContrastCorrection = false
	recognitionSettings.ResultType = asposeocrcloud.RESULTTYPE_TEXT.Ptr()
	recognitionSettings.ResultTypeTable = asposeocrcloud.RESULTTYPETABLE_TEXT.Ptr()

	requestBody := *asposeocrcloud.NewOCRRecognizeImageBody(
		fileb64Encoded,
		recognitionSettings,
	)

	taskId, httpRes, err := apiClient.RecognizeImageApi.PostRecognizeImage(context.Background()).OCRRecognizeImageBody(requestBody).Execute()
	if err != nil || httpRes.StatusCode != 200 {
		fmt.Println("API error:", err)
		return
	}

	fmt.Printf("File successfully sent. Your TaskID is %s \n", taskId)

	// Step 2: request task results using task ID
	ocrResp, httpRes, err := apiClient.RecognizeImageApi.GetRecognizeImage(context.Background()).Id(taskId).Execute()
	if err != nil || httpRes.StatusCode != 200 || ocrResp == nil {
		fmt.Println("API error:", err)
		return
	}

	if *ocrResp.TaskStatus == asposeocrcloud.OCRTASKSTATUS_COMPLETED {
		if !ocrResp.Results[0].Data.IsSet() {
			fmt.Println("Response is empty")
			return
		}

		// Decode results and write to file
		decodedBytes, err := base64.StdEncoding.DecodeString(*ocrResp.Results[0].Data.Get())
		if err != nil {
			fmt.Println("Decode error:", err)
			return
		}

		resultFilePath := "../results/" + taskId + ".txt"
		err = ioutil.WriteFile(resultFilePath, decodedBytes, 0644)
		if err != nil {
			fmt.Println("Write file error:", err)
			return
		}

		fmt.Printf("Task result successfully saved at %s \n", resultFilePath)
	} else {
		fmt.Printf("Sorry, task %s is not completed yet. You can request results later. Task status: %s\n", taskId, *ocrResp.TaskStatus)
	}
}
```

{{< /tab >}}

{{< /tabs >}}

