---
weight: 30
date: "2023-11-27"
author: "Vladimir Lapin"
type: docs
url: /tts-sdk/
feedback: OCRCLOUD
title: Text-to-speech conversion with Aspose.OCR Cloud SDK
description: How to use Aspose.OCR Cloud SDK for reading the text aloud.
keywords:
- OCR
- read
- aloud
- sound
- voice
- media
- speech
- TTS
- programming
- development
- SDK
---

Although you can directly call the Aspose.OCR Cloud REST API to [convert text to speech](/ocr/send-text-to-speech/) and [fetch voice](/ocr/fetch-voice/), there is a much easier way to implement text-to-speech functionality in your applications. We provide software development kits (SDKs) for all popular programming languages. They wrap up all routine operations such as establishing connections, sending API requests, and parsing responses into a few simple methods. It makes interaction with Aspose.OCR Cloud services much easier, allowing you to focus on business logic rather than technical details.

{{< tabs tabID="1" tabTotal="3" tabName1=".NET" tabName2="Java" tabName3="Android" >}}

{{< tab tabNum="1" >}}
```csharp
using Aspose.OCR.Cloud.SDK.Api;
using Aspose.OCR.Cloud.SDK.Model;

namespace Example
{
	internal class Program
	{
		static void Main(string[] args)
		{
			/** Authorize your requests to Aspose.OCR Cloud API */
			ConvertTextToSpeechApi api = new ConvertTextToSpeechApi("<Client Id>", "<Client Secret>");
			/** Send text to TTS */
			TTSBody source = new TTSBody {
				text: "Read this text aloud",
				settings: new TTSSettings(
					language: LanguageTTS.English,
					resultType: ResultTypeTTS.Wav
					)
			};
			string taskID = api.PostConvertTextToSpeech(source);
			/** Save voice to file */
			TTSResponse result = api.GetConvertTextToSpeech(taskID);
			byte[] voice = result.Results[0].Data;
			File.WriteAllBytes("voice.wav", voice);
		}
	}
}
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-dotnet
{{< /tab >}}

{{< tab tabNum="2" >}}
```java
// Import classes
import Aspose.OCR.Cloud.SDK.TextToSpeechApi;
import Aspose.OCR.Cloud.SDK.model.LanguageTTS;
import Aspose.OCR.Cloud.SDK.model.ResultTypeTTS;
import Aspose.OCR.Cloud.SDK.model.TTSBody;
import Aspose.OCR.Cloud.SDK.model.TTSResponse;

import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.Scanner;

public class Example {
  public static void main(String[] args) {
    /** Authorize your requests to Aspose.OCR Cloud API */
    RecognizeTableApi api = new RecognizeTableApi("<Client Id>", "<Client Secret>");
    /** Send text to TTS */
    TTSBody source = new TTSBody();
    source.setText("Read this text aloud");
    String taskId = api.postTextToSpeech(source);
    /** Save voice to file */
    TTSResponse result = api.getTextToSpeechResult(taskId);
    Files.write(Path.of("voice.wav"), result.getResults().get(0).getData());
  }
}
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-java
{{< /tab >}}

{{< tab tabNum="3" >}}
```java
/** Authorize your requests to Aspose.OCR Cloud API */
RecognizeTableApi api = new RecognizeTableApi("<Client Id>", "<Client Secret>");
/** Send text to TTS */
TTSBody source = new TTSBody();
source.setText("Read this text aloud");
String taskId = api.postTextToSpeech(source);
/** Save voice to file */
TTSResponse result = api.getTextToSpeechResult(taskId);
FileOutputStream fOut = openFileOutput("voice.wav", Context.MODE_PRIVATE);
fOut.write(result.getResults().get(0).getData());
fOut.close();
```

Visit our GitHub repository for a working code and sample files: https://github.com/aspose-ocr-cloud/aspose-ocr-cloud-android
{{< /tab >}}

{{< /tabs >}}
