---
weight: 20
date: "2023-11-27"
author: "Vladimir Lapin"
type: docs
url: /authorization/
feedback: OCRCLOUD
title: Authorization
description: How to get an access token and use it to authorize Aspose.OCR Cloud API requests.
keywords:
- REST
- header
- auth
- access
- security
---

Aspose.OCR Cloud follows industry standards and best practices to keep your data secure. All communication with OCR REST API is done using JWT authentication, which provides an open-standard, highly secure way to exchange information.

## Getting an access token

Time-limited JWT tokens are generated using _Client ID_ and _Client Secret_ credentials that are specific for each application. To obtain the credentials:

1. Sign in to [Aspose Cloud API Dashboard](https://dashboard.aspose.cloud/).
2. Go to [**Applications**](https://dashboard.aspose.cloud/applications) page.
3. Click **Create New Application** button.
4. Give the application an easily recognizable name so it can be quickly found in a long list, and provide an optional detailed description.
5. Create the cloud storage by clicking the _plus_ icon and following the required steps. You can also reuse existing storage, if available.   
   Aspose.OCR Cloud uses its own internal storage, so you can provide the bare minimum storage options:

    - Type: **Internal storage**
    - Storage name: _Any name you like_
    - Storage mode: **Retain files for 24 hours**

6. Click **Save** button.
7. Click the newly created application and copy the values from **Client Id** and **Client Secret** fields.

{{% alert color="primary" %}} 
Keep your credentials safe! If you feel that they might be compromised, regenerate them immediately.
{{% /alert %}}

Now request an access token by sending the **POST** request to `https://api.aspose.cloud/connect/token` with the following parameters in the request body (x-www-form-urlencoded):

- `grant_type` - must be `client_credentials`
- `client_id` - the value from **Client Id** field.
- `client_secret` - the value from **Client Secret** field.

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --request POST --location 'https://api.aspose.cloud/connect/token' \
     --header 'Content-Type: application/x-www-form-urlencoded' \
     --data-urlencode 'grant_type=client_credentials' \
     --data-urlencode 'client_id=CLIENT-ID-VALUE' \
     --data-urlencode 'client_secret=CLIENT-SECRET-VALUE'
```
{{< /tab >}}
{{< tab tabNum="2" >}}
```json
{
	"access_token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA",
	"expires_in": 3600,
	"token_type": "Bearer"
}
```
{{< /tab >}}
{{< /tabs >}}

The access token is returned in `access_token` property of the response JSON and will be valid for the number of seconds specified in the `expires_in` property of the response JSON. If it has expired, request a new one using the same API call.

## Authorizing REST API requests

To authorize your requests to Aspose.OCR Cloud API, pass the access token in **Authorization** header of each request (_Bearer authentication_):

```bash
curl --request POST --location 'https://api.aspose.cloud/v3.0/ocr/recognize' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...l8v7jUV-mLjEdQ'
```

## Authorizing SDK requests

The SDKs greatly simplify all operations for obtaining an access token and authorizing requests. Just pass in the values from the **Client ID** and **Client Secret** fields when initializing the recognition API and it will do the rest for you.

{{< tabs tabID="3" tabTotal="5" tabName1=".NET" tabName2="Java" tabName3="Python" tabName4="Node.js" tabName5="Android" >}}

{{< tab tabNum="1" >}}
```csharp
Configuration conf = new Configuration();
conf.AppSid = "CLIENT-ID-VALUE";
conf.AppKey = "CLIENT-SECRET-VALUE";
OcrApi api = new OcrApi(conf);
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-dotnet
{{< /tab >}}

{{< tab tabNum="2" >}}
```java
Configuration.setAPP_SID("CLIENT-ID-VALUE");
Configuration.setAPI_KEY("CLIENT-SECRET-VALUE");
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-java
{{< /tab >}}

{{< tab tabNum="3" >}}
```python
configuration = Configuration(apiKey="CLIENT-SECRET-VALUE",
                              appSid="CLIENT-ID-VALUE")
api = OcrApi(configuration)
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-python
{{< /tab >}}

{{< tab tabNum="4" >}}
```js
var conf = {
    "apiKey":"CLIENT-SECRET-VALUE",
    "appSID":"CLIENT-ID-VALUE",
};
var instance = new Asposeocrcloud.OcrApi(conf);
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-nodejs
{{< /tab >}}

{{< tab tabNum="5" >}}
```java
Configuration.setAPP_SID("CLIENT-ID-VALUE");
Configuration.setAPI_KEY("CLIENT-SECRET-VALUE");
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-android
{{< /tab >}}

{{< /tabs >}}
