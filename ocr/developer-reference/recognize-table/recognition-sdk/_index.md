---
weight: 30
date: "2023-11-27"
author: "Vladimir Lapin"
type: docs
url: /table-recognition-sdk/
feedback: OCRCLOUD
title: Table recognition with Aspose.OCR Cloud SDK
description: How to use Aspose.OCR Cloud SDK for extracting text from scanned or photographed tables.
keywords:
- OCR
- recognize
- programming
- development
- SDK
- table
- row
- cell
- Excel
---

Although you can directly call the Aspose.OCR Cloud REST API to [send table images for recognition](/ocr/send-table-for-recognition/) and [fetch recognition results](/ocr/fetch-table-recognition-result/), there is a much easier way to implement OCR functionality in your applications. We provide software development kits (SDKs) for all popular programming languages. They wrap up all routine operations such as establishing connections, sending API requests, and parsing responses into a few simple methods. It makes interaction with Aspose.OCR Cloud services much easier, allowing you to focus on business logic rather than technical details.

{{< tabs tabID="1" tabTotal="4" tabName1=".NET" tabName2="Java" tabName3="Android" tabName4="Node.js" >}}

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
			RecognizeTableApi recognizeTableApi = new RecognizeTableApi("<Client Id>", "<Client Secret>");
			/** Read table image to array of bytes */
			byte[] tableImage = File.ReadAllBytes("table.png");
			/** Specify recognition settings */
			OCRSettingsRecognizeTable recognitionSettings = new OCRSettingsRecognizeTable {
				Language = Language.English,
				ResultTypeTable = ResultTypeTable.Csv
			};
			/** Send table for recognition */
			OCRRecognizeTableBody source = new OCRRecognizeTableBody(tableImage, recognitionSettings);
			string taskID = recognizeTableApi.PostRecognizeTable(source);
			/** Fetch recognition result */
			OCRResponse result = recognizeTableApi.GetRecognizeTable(taskID);
			Console.WriteLine(Encoding.UTF8.GetString(result.Results[0].Data));
		}
	}
}
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-dotnet
{{< /tab >}}

{{< tab tabNum="2" >}}
```java
// Import classes
import Aspose.OCR.Cloud.SDK.RecognizeTableApi;
import Aspose.OCR.Cloud.SDK.model.*;

import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public class Example {
  public static void main(String[] args) {
    /** Authorize your requests to Aspose.OCR Cloud API */
    RecognizeTableApi api = new RecognizeTableApi("<Client Id>", "<Client Secret>");
    /** Read table image to array of bytes */
    byte[] tableImage = Files.readAllBytes(Path.of("table.png"));
    /** Specify recognition settings */
    OCRSettingsRecognizeTable settings = new OCRSettingsRecognizeTable();
    settings.setLanguage(Language.ENGLISH);
    settings.setResultTypeTable(ResultTypeTable.CSV);
    /** Send table for recognition */
    OCRRecognizeTableBody requestBody = new OCRRecognizeTableBody();
    requestBody.setTable(tableImage);
    requestBody.setSettings(settings);
    String taskId = api.postRecognizeTable(requestBody);
    /** Fetch recognition result */
    OCRResponse apiResponse = api.getRecognizeTable(taskId);
    System.out.println(new String(apiResponse.getResults().get(0).getData(), StandardCharsets.UTF_8) + "\n\n");
  }
}
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-java
{{< /tab >}}

{{< tab tabNum="3" >}}
```java
/** Authorize your requests to Aspose.OCR Cloud API */
RecognizeTableApi api = new RecognizeTableApi("<Client Id>", "<Client Secret>");
/** Read table image to array of bytes */
String tableFileName = "table.png";
InputStream inputStream = context.getAssets().open(tableFileName);
int size = inputStream.available();
byte[] tableImage = new byte[size];
inputStream.read(tableImage);
inputStream.close();
/** Specify recognition settings */
OCRSettingsRecognizeTable settings = new OCRSettingsRecognizeTable();
settings.setLanguage(Language.ENGLISH);
settings.setResultTypeTable(ResultTypeTable.CSV);
/** Send table for recognition */
OCRRecognizeTableBody requestBody = new OCRRecognizeTableBody();
requestBody.setTable(tableImage);
requestBody.setSettings(settings);
String taskId = api.postRecognizeTable(requestBody);
/** Fetch recognition result */
OCRResponse apiResponse = api.getRecognizeTable(taskId);
System.out.println(new String(apiResponse.getResults().get(0).getData(), StandardCharsets.UTF_8) + "\n\n");
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-android
{{< /tab >}}

{{< tab tabNum="4" >}}
```js
const AsposeOcrCloud10040Api = require('aspose_ocr_cloud_5_0_api');
const path = require("path");
const fs = require("fs");
const request = require('aspose_ocr_cloud_5_0_api/node_modules/request');

var api;

/** Getting access token */
function connect(){
    return new Promise(function(resolve, reject){
        request.post({
            headers: {"ContentType": "application/x-www-form-urlencoded", "Accept": "application/json;charset=UTF-8"},
            url: "https://api.aspose.cloud/connect/token",
            form: JSON.parse('{"client_id": "<Client Id>", "client_secret": "<Client Secret>", "grant_type": "client_credentials"}')
        }, (err, res, body) => {
            if (err) {
                reject(err);
            }
            resolve(body);
        });
    });
}

/** Sending table image for recognition */
function callPostTableRecognizeFunction (body, img_path){
    return new Promise(function (resolve, reject){
        api = new AsposeOcrCloud10040Api.RecognizeTableApi();
        api.apiClient.basePath = "https://api.aspose.cloud/v5.0/ocr";
        var body_res = JSON.parse(body);
        api.apiClient.authentications = {
            'JWT': {
                type: 'oauth2',
                accessToken: body_res['access_token']
            }
        }
        api.apiClient.defaultHeaders = {
            "User-Agent": "OpenAPI-Generator/1005.0/Javascript"
        }
        /** Read table image to array of bytes */
        var filePath = path.normalize(img_path);
        var buffer = Buffer.alloc(1024 * 50);
        var fileData = fs.readFileSync(filePath, buffer);
        /** Specify recognition settings */
        let settings = new AsposeOcrCloud10040Api.OCRSettingsRecognizeTable();
        settings.Language = "English";
        settings.ResultType = "Text";
        /** Send table for recognition */
        let requestData = new AsposeOcrCloud10040Api.OCRRecognizeTableBody(fileData.toString('base64'), settings);
        api.postRecognizeTable(requestData, (err, res, body) => {
            if (err) {
                reject(err);
            }
            resolve(res);
        });
    });
}

/** Fetching recognition result */
function callGetTableFunction(id){
    return new Promise(function(resolve, reject){
        api.getRecognizeTable(id, (err, res, body) => {
            if (err) {
                reject(err);
            }
            resolve(body);
        })
    })
}

/** Outputting recognition results */
function processResult(body){
    console.log('Processing results...')
    const json_res = JSON.parse(body['text']);
    for (const key in json_res['results']){
        console.log(atob(json_res['results'][key]['data']))
    }
}

/** Recognition flow */
connect().then(
    access_token => callPostTableRecognizeFunction(access_token, "source.png")
).then(
    x => new Promise(resolve => setTimeout(() => resolve(x), 1000))
).then(
    id => callGetTableFunction(id)
).then(
    body => processResult(body)
)
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-nodejs
{{< /tab >}}

{{< /tabs >}}
