---
title: "Extract Text from Image using Cloud Storage"
type: docs
url: /extract-text-from-image-using-cloud-storage/
weight: 10
---

## **Introduction**
Optical character recognition can be performed either on a whole image or on a specific portion of the image. If the required characters are all over the image then scanning the whole image is a better option. If you want to scan partial image then specify a rectangular area containing the characters. Aspose.OCR Cloud API allows passing X and Y coordinates from where the rectangle is supposed to be started as well as its width and height. Once the character recognition operation is initiated within a specified rectangular area - The cloud OCR API will read the characters and font information from that area and return the response in XML or JSON format.

The characters of different languages have different representations. If we combine the languages with the font types and styles - it makes a large set of characters to be recognized from an image. Aspose.OCR Cloud handles this task very elegantly as it can recognize text in English, French and German languages.

Aspose.OCR Cloud provided an API to recognize and extract OCR text from raster images (JPEG, PNG, GIF, BMP, TIFF) stored in the cloud.
## **API Explorer**
[The API Reference page](https://apireference.aspose.cloud/ocr/#/Ocr/GetRecognizeDocument) is the easiest way to try out our APIs right away in your browser! It allows you to effortlessly interact and try out every single operation our APIs exposes.
### **cURL Example**
{{< tabs tabTotal="2" tabID="1" tabName1="Request" tabName2="Response" >}}

{{< tab tabNum="1" >}}

```java

curl -v "https://api.aspose.cloud/v3.0/ocr/sample_ocr.png/recognize" \
-X GET \
-H "Content-Type: application/json" \
-H "Accept: application/json"\
-H "authorization: Bearer <JWT Token>"

```

{{< /tab >}}

{{< tab tabNum="2" >}}

```java

 {

  "text": "He collapsed right in the middle of a packed courtroom. He was\none of this country's most distinguished trial lawyers. He was also\na man who was as well known for the three-thousand-dollar Italian\nsuits which draped his well-fed frame as for his remarkable string\nof legal victories. I simply stood there, paralyzed by the shock of\nwhat I had just witnessed. The great Julian Mantle had been\nreduced to a victim and was now squirming on the ground like a\nhelnless infant, shaking and shivering and sweating like a maniac\nEverything seemed to move in slow motion from that point on.\n'My God, Julian's in trouble!\" his paralegal screamed, emotionally\noffering us a blinding glimpse of the obvious. The judge looked\npanic-stricken and quickly muttered something into the private\nphone she had had installed in the event of an emergency. As for\nme, I could only stand there, dazed and confused. Please don'tdie,\nyou old fool. Its too early for you to check out. You don't deserve\nto die like this.\nThe bailiff, who earlier had looked as if he had been embalmed\nin his standing position. leapt into action and started to perform\nCPR on the fallen legal hero. The paralegal was at his side, her\nCHAPTER ONE\nThe Wake-Up Call",

  "code": 200

}

```

{{< /tab >}}

{{< /tabs >}}
## **SDKs**
Using an SDK (API client) is the quickest way for a developer to speed up the development. An SDK takes care of a lot of low-level details of making requests and handling responses and lets you focus on writing code specific to your particular project. Check out our [GitHub repository](https://github.com/aspose-ocr-cloud) for a complete list of Aspose.OCR Cloud SDKs along with working examples, to get you started in no time. Please check [Available SDKs](/ocr/available-sdks/) article to learn how to add an SDK to your project.
### **SDK Examples**
**Extract OCR or HOCR Text from Images**

{{< tabs tabTotal="3" tabID="4" tabName1="C#" tabName2="Java" tabName3="Python">}}

{{< tab tabNum="1" >}}

{{< gist "aspose-cloud" "0f9e9de5290f0fcdfd93517225f2b66a" "Example-RecognizeFromStorage.cs" >}}

{{< /tab >}}

{{< tab tabNum="2" >}}

{{< gist "aspose-cloud" "723802ba0a961dac4b73a96f1932469c" "Example-RecognizeFromStorage.java" >}}

{{< /tab >}}

{{< tab tabNum="3" >}}

{{< gist "aspose-cloud" "806422f52a90ff15bbfcd268b91184a9" "RecognizeFromStorage.py" >}}

{{< /tab >}}

{{< /tabs >}}




