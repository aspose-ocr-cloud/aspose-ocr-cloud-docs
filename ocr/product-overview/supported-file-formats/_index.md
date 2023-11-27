---
weight: 30
date: "2023-11-27"
author: "Vladimir Lapin"
type: docs
url: /supported-file-formats/
feedback: OCRCLOUD
title: Supported file formats
description: File formats for images and recognition results supported by Aspose.OCR Cloud.
keywords:
- format
- image
- data
- source
- result
- scan
- photo
---

Aspose.OCR Cloud can read literally any image you can get from a scanner, camera, or find on the internet.

## Recognized file formats

File type | Extensions | Details
--------- | ---------- | -------
**Bitmap** | .BMP | Uncompressed raster images.
**JPEG** | .JPG, .JPEG, .JPE | The most popular format for smartphone photos and digital cameras.
**PNG** | .PNG | Portable Network Graphic, popular format for images with transparent background.
**TIFF** | .TIF, .TIFF | Tag Image File Format, commonly used for high-quality scanning.<br />_Only single-page TIFF images are supported._
**GIF** | .GIF | Graphics Interchange Format, limited to 256 colors.
**SVG** | .SVG | Scalable Vector Graphics, one of the most popular vector graphic format on the internet.
**PDF** | .PDF | Portable Document Format, the industry standard for storing multi-page documents.

{{% alert color="primary" %}}
You can recognize the entire image or only a specific area of the image.
{{% /alert %}}

## Recognition results

Recognition results are returned in the most popular document and data exchange formats:

Format | Details
------ | -------
**Plain text** | Unformatted text, optionally broken into lines.
**PDF** | Portable Document Format, the industry standard for storing multi-page documents. The resulting documents are fully searchable and indexable.
**CSV** <sup>1</sup> | A plain text format that contains tabular data separated by commas.
**Excel** <sup>1</sup> | Microsoft Excel spreadsheet (Microsoft Office 2007 or later).
**hOCR** | XML-based open standard of data representation for formatted text obtained from OCR. Commonly used to make searchable PDF files.
**WAV** <sup>2</sup>  | Waveform Audio, the main format used on Microsoft Windows systems for uncompressed audio. 

{{% alert color="primary" %}}
1. CSV and Excel formats are available for tabular data recognition only.
2. Audio is returned from text-to-speech conversion methods only.
{{% /alert %}}
