---
weight: 81
date: "2023-05-11"
author: "Vladimir Lapin"
type: docs
url: /aspose-ocr-cloud-23-5-0-release-notes/
feedback: OCRCLOUD
title: Aspose.OCR Cloud 23.5.0 - Release Notes
description: A summary of recent changes, enhancements and bug fixes in Aspose.OCR Cloud 23.5.0 (May 2022) release.
keywords:
- May
- 2023
- new
- release
- changelog
---

{{% alert color="primary" %}}
This article contains a summary of recent changes, enhancements and bug fixes in **Aspose.OCR Cloud 23.5.0 (May 2022)** release.
{{% /alert %}}

## Deprecation warning

{{% alert color="caution" %}}
In the 23.5.0 release, several endpoints have been [updated](#updated-public-apis) to make the API simpler and more consistent.

To make code updates easier, previous endpoints remain fully functional. All of your existing code will continue to work and you can even make minor updates to it, but be aware that all [deprecated](#deprecated-apis) endpoints are planned to be removed in the next release in favor of the new API.
{{% /alert %}}

## What was changed

Key | Summary | Category
--- | ------- | --------
n/a | Conversion of DjVu files to searchable PDF documents. | New feature
n/a | Updated image processing endpoints:<ul><li>[Skew correction](/ocr/deskew-image/);</li><li>[Dewarping](/ocr/dewarp-image/);</li><li>[Upsampling](/ocr/upsample-image/);</li><li>[Binarization](/ocr/binarize-image/).</li></ul> | Enhancement
n/a | Updated [text-to-speech conversion](/ocr/text-to-speech/) endpoints. | Enhancement

## Public API changes and backwards compatibility

This section lists all public API changes introduced in **Aspose.OCR Cloud 23.5.0** that may affect the code of existing applications.

### Added public APIs:

The following public APIs have been introduced in this release:

#### `https://api.aspose.cloud/v5.0/ocr/djvu2pdf`

Convert DjVu file to a searchable PDF document.

Method | Action
------ | ------
**POST** | Send DjVu file for conversion.
**GET** | Fetch the conversion result (searchable PDF).
**DELETE** | Remove the conversion task from the queue.

### Updated public APIs:

The following public APIs have been updated in this release:

#### `https://api.aspose.cloud/v5.0/ocr/deskewimage`

{{% alert color="warning" %}}
**BACKWARD INCOMPATIBILITY!**

This endpoint replaces the `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/PostSkewCorrectionFile`, `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/GetResultTask` and `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/GetResultFile` endpoints.
{{% /alert %}}

Automatically straighten a skewed image.

Method | Action
------ | ------
**POST** | Submit an image for processing.
**GET** | Fetch the processing result.
**DELETE** | Remove the processing task from the queue.

#### `https://api.aspose.cloud/v5.0/ocr/binarizeimage`

{{% alert color="warning" %}}
**BACKWARD INCOMPATIBILITY!**

This endpoint replaces the `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/PostBinarizationFile`, `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/GetResultTask` and `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/GetResultFile` endpoints.
{{% /alert %}}

Automatically convert an image to black and white.

Method | Action
------ | ------
**POST** | Submit an image for processing.
**GET** | Fetch the processing result.
**DELETE** | Remove the processing task from the queue.

#### `https://api.aspose.cloud/v5.0/ocr/dewarpimage`

{{% alert color="warning" %}}
**BACKWARD INCOMPATIBILITY!**

This endpoint replaces the `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/PostDewarpingFile`, `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/GetResultTask` and `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/GetResultFile` endpoints.
{{% /alert %}}

Automatically straighten curved text and remove geometric distortions from an image.

Method | Action
------ | ------
**POST** | Submit an image for processing.
**GET** | Fetch the processing result.
**DELETE** | Remove the processing task from the queue.

#### `https://api.aspose.cloud/v5.0/ocr/upscaleimage`

{{% alert color="warning" %}}
**BACKWARD INCOMPATIBILITY!**

This endpoint replaces the `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/PostUpsamplingImageFile`, `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/GetResultTask` and `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/GetResultFile` endpoints.
{{% /alert %}}

Increase an image resolution and enhance the contrast of text details.

Method | Action
------ | ------
**POST** | Submit an image for processing.
**GET** | Fetch the processing result.
**DELETE** | Remove the processing task from the queue.

#### `https://api.aspose.cloud/v5.0/ocr/converttexttospeech`

{{% alert color="warning" %}}
**BACKWARD INCOMPATIBILITY!**

This endpoint replaces the `https://api.aspose.cloud/v5.0/ocr/TextToSpeech/PostTextToSpeech`, `https://api.aspose.cloud/v5.0/ocr/TextToSpeech/GetTextToSpeechResult` and `https://api.aspose.cloud/v5.0/ocr/TextToSpeech/GetTextToSpeechResultFile` endpoints.
{{% /alert %}}

Convert the recognition results into a natural human voice.

Method | Action
------ | ------
**POST** | Submit a text for conversion.
**GET** | Fetch the audio.
**DELETE** | Remove the text-to-speech conversion task from the queue.

### Removed public APIs:

_No changes._

### Deprecated APIs

The following public APIs have been marked as deprecated and will be removed in the next release:

#### `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/PostSkewCorrectionFile`

Replaced with _[POST]_ `https://api.aspose.cloud/v5.0/ocr/deskewimage` endpoint.

#### `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/PostBinarizationFile`

Replaced with _[POST]_ `https://api.aspose.cloud/v5.0/ocr/binarizeimage` endpoint.

#### `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/PostDewarpingFile`

Replaced with _[POST]_ `https://api.aspose.cloud/v5.0/ocr/dewarpimage` endpoint.

#### `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/PostUpsamplingImageFile`

Replaced with _[POST]_ `https://api.aspose.cloud/v5.0/ocr/upscaleimage` endpoint.

#### `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/GetResultTask`

Replaced with the following endpoints, depending on the image processing method:

- _[GET]_ `https://api.aspose.cloud/v5.0/ocr/deskewimage`
- _[GET]_ `https://api.aspose.cloud/v5.0/ocr/binarizeimage`
- _[GET]_ `https://api.aspose.cloud/v5.0/ocr/dewarpimage`
- _[GET]_ `https://api.aspose.cloud/v5.0/ocr/upscaleimage`

#### `https://api.aspose.cloud/v5.0/ocr/ImageProcessing/GetResultFile`

Replaced with the following endpoints, depending on the image processing method:

- _[GET]_ `https://api.aspose.cloud/v5.0/ocr/deskewimage`
- _[GET]_ `https://api.aspose.cloud/v5.0/ocr/binarizeimage`
- _[GET]_ `https://api.aspose.cloud/v5.0/ocr/dewarpimage`
- _[GET]_ `https://api.aspose.cloud/v5.0/ocr/upscaleimage`

#### `https://api.aspose.cloud/v5.0/ocr/TextToSpeech/PostTextToSpeech`

Replaced with _[POST]_ `https://api.aspose.cloud/v5.0/ocr/converttexttospeech` endpoint.

#### `https://api.aspose.cloud/v5.0/ocr/TextToSpeech/GetTextToSpeechResult`

Replaced with _[GET]_ `https://api.aspose.cloud/v5.0/ocr/converttexttospeech` endpoint.

#### `https://api.aspose.cloud/v5.0/ocr/TextToSpeech/GetTextToSpeechResultFile`

Replaced with _[GET]_ `https://api.aspose.cloud/v5.0/ocr/converttexttospeech` endpoint.

## Examples

The examples below illustrate the changes introduced in this release:

### Automatically correct geometric image distortions

Send image for dewarping:

```bash
curl --location --request POST 'https://api.aspose.cloud/v5.0/ocr/dewarpimage' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA' \
--data-raw '{
  "image": "iVBORw0KGgoAAAANSUh...d1iEAAAAASUVORK5CYII=",
}'
```

Fetch dewarped image:

```bash
curl --location --request GET 'https://api.aspose.cloud/v5.0/ocr/dewarpimage?id=c4b60313-4f78-45f8-b708-069eb98dc22e' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA' \
```

### Convert text to speech

Send text for conversion:

```bash
curl --location --request POST 'https://api.aspose.cloud/v5.0/ocr/converttexttospeech' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...DpisWjfwe5RsfNCQ9Uh7Ig' \
--data '{
	"text": "Read this text aloud",
	"settings": {
		"language": "English",
		"resultType": "Wav"
	}
}'
```

Fetch audio:

```bash
curl --location --request GET 'https://api.aspose.cloud/v5.0/ocr/converttexttospeech?id=TTS01232-9d40-4f2d-8eda-f1fc0b12bce6' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...DpisWjfwe5RsfNCQ9Uh7Ig' \
```

### Convert DjVu to searchable PDF

Send DjVu file for conversion:

```bash
curl --location --request POST 'https://api.aspose.cloud/v5.0/ocr/djvu2pdf' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA' \
--data-raw '{
  "image": "iVBORw0KGgoAAAANSUh...d1iEAAAAASUVORK5CYII="
}'
```

Fetch PDF converted from DjVu:

```bash
curl --location --request GET 'https://api.aspose.cloud/v5.0/ocr/djvu2pdf?id=c4b60313-4f78-45f8-b708-069eb98dc22e' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA' \
```
