---
weight: 10
date: "2022-07-19"
author: "Vladimir Lapin"
type: docs
url: /recognize-image-from-content/
title: Recognizing an image from request body
description: Extracting the text from an image passed to the Aspose.OCR Cloud API in the request body.
keywords:
- OCR
- recognize
- image
- picture
- binary
---

Send a **POST** request with the binary content of an image to the [`https://api.aspose.cloud/v3.0/ocr/recognize`](https://apireference.aspose.cloud/ocr/#/Ocr/PostOcrFromUrlOrContent) Aspose.OCR Cloud REST API endpoint and get back the recognized text in JSON format.

{{< tabs tabID="1" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --location --request POST 'https://api.aspose.cloud/v3.0/ocr/recognize' \
--header 'Authorization: Bearer {ACCESS TOKEN}' \
--header 'Content-Type: image/jpeg' \
--data-binary '@/C:/Samples/image.jpg'
```
{{< /tab >}}
{{< tab tabNum="2" >}}
```json
{
	"text": "Ah broken is the golden bowl! the spirit flown forever!\n.let the bell toll!--a saintly soul floats on the Stygian river;",
	"pdf": null,
	"hocr": null,
	"status": "200",
	"statusMessage": "success",
	"code": 200
}
```
{{< /tab >}}
{{< /tabs >}}

## Additional request parameters

The OCR request can be further refined by adding the following optional parameters to the query string:

- **language**  
  [Recognition language](/ocr/recognition-languages-list/), _integer_. If this parameter is omitted, the recognition engine will treat the text as English.
- **resultType**  
  [Recognition results](/ocr/recognition-results-list/) format, _integer_. You can request multiple result types at the same time by providing the corresponding numbers separated by commas. If this parameter is omitted, the recognized text will be returned as plain text broken into lines.
- **spellCheck**  
  Automatically replace misspelled words with the built-in spell checker; _boolean_ (`true` / `false`). Disabled by default.
- **skewCorrect**  
  Automatically straighten a skewed image to improve recognition accuracy; _boolean_ (`true` / `false`). It is recommended to turn this parameter on when recognizing smartphone photos. Disabled by default.
- **makeContrastCorrection**  
  Automatically adjust image contrast to improve recognition accuracy; _boolean_ (`true` / `false`). Disabled by default.
- **makeImageUpscaling**  
  Try to upscale low resolution images to improve recognition accuracy; _boolean_ (`true` / `false`). Disabled by default.
- **dsrMode**  
  Manually specify the [document structure analysis method](/ocr/dsr-mode/) that works best for your content.
- **dsrConfidence**  
  Manually specify how to [deal with]((/ocr/dsr-mode/)) low quality areas of the image.

### Example

{{< tabs tabID="2" tabTotal="2" tabName1="Request" tabName2="Response" >}}
{{< tab tabNum="1" >}}
```bash
curl --location --request POST 'https://api.aspose.cloud/v3.0/ocr/recognize?resultType=2&spellCheck=true' \
--header 'Authorization: Bearer {ACCESS TOKEN}' \
--header 'Content-Type: image/jpeg' \
--data-binary '@/C:/Samples/image.jpg'
```
{{< /tab >}}
{{< tab tabNum="2" >}}
```json
{
	"text": null,
	"pdf": "JVBERi0xLjMKJcKTwozCi8KeIFJlcG9 <...> +CnN0YXJ0eHJlZgoyMTkzNTgKJSVFT0YK",
	"hocr": null,
	"status": "200",
	"statusMessage": "success",
	"code": 200
}
```
{{< /tab >}}
{{< /tabs >}}

## SDKs

While you can directly call the Aspose.OCR Cloud REST API, we provide software development kits (SDKs) for all popular programming languages. They wrap up all routine operations such as establishing connections, sending API requests, and parsing responses into a few simple methods. It makes interaction with Aspose.OCR Cloud services much easier, allowing you to focus on business logic rather than technical details.

{{< tabs tabID="3" tabTotal="5" tabName1=".NET" tabName2="Java" tabName3="Python" tabName4="Node.js" tabName5="Android" >}}

{{< tab tabNum="1" >}}
```csharp
string name = "source.png";
using (FileStream fs = File.OpenRead(name))
{
	OcrApi api = new OcrApi(conf);
	var request = new PostOcrFromUrlOrContentRequest(fs);
	OCRResponse response = api.PostOcrFromUrlOrContent(request);
	return response.Text;
}
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-dotnet
{{< /tab >}}

{{< tab tabNum="2" >}}
```java
api = new ApiClient().createService(OcrApiInvoker.class);
File f = new File("source.png");
OCRResponse ocrResponse = api.RecognizeFromContent(f, Language.English);
return ocrResponse.text;
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-java
{{< /tab >}}

{{< tab tabNum="3" >}}
```python
api = OcrApi(configuration)
params = Parameters(LanguageGroup.ENGLISH, ResultType.Text, False, False, DSRPipeline.DsrNoFilter,
                    DSRConfidence.Mid, False)
res = api.post_recognize_from_content(r"source.png", params)
print(res.text)
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-python
{{< /tab >}}

{{< tab tabNum="4" >}}
```js
var filePath = path.normalize(local_src_folder + "/" + "source.png");
var buffer = Buffer.alloc(1024 * 50);
var fileData = fs.readFileSync(filePath, buffer);

instance.RecognizeFromContentAuto(fileData, function (err, data, res) {
	if (err) throw err;
	expect(200).to.be(res.status);
	console.log("OK\n-----------------------------------------------------------------------------------");
	console.log(data);
});
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-nodejs
{{< /tab >}}

{{< tab tabNum="5" >}}
```java
api = new ApiClient().createService(OCRAPI.class);
InputStream inputStream = getContentResolver().openInputStream(data.getData());
byte[] targetArray = new byte[inputStream.available()];
inputStream.read(targetArray);
RequestBody requestBody = RequestBody.create(MediaType.parse("application/octet-stream"), targetArray);
OCRResponse ocrResponse = api.RecognizeFromContent(requestBody, Language.English);
String text = ocrResponse.text;
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-android
{{< /tab >}}

{{< /tabs >}}
