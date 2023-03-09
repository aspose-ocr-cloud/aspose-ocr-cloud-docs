---
weight: 30
date: "2023-03-06"
author: "Vladimir Lapin"
type: docs
url: /result-format/
feedback: OCRCLOUD
aliases:
- /recognition-results-list/
title: Processing result formats
description: The list languages supported by recognition, text-to-speech, and other Aspose.OCR Cloud APIs.
keywords:
- locale
- language
- culture
- letter
- character
---

Aspose.OCR Cloud can return results in the most popular document and data exchange [formats](/ocr/supported-file-formats/#recognition-results). The desired format is specified in request settings:

Format | REST API setting | Applies to
------ | ---------------- | ----------
Plain text | `"resultType": "Text"`<br />`"resultTypeTable": "Text"`<br />`"resultType": "TextAndPdf"`<br />`"resultType": "TextAndHocr"`<br />`"resultType": "TextAndPdfAndHocr"` | [Image recognition](/ocr/recognize-image/)<br />[PDF recognition](/ocr/recognize-pdf/)<br />[Receipt recognition](/ocr/recognize-receipt/)<br />[Table recognition](/ocr/recognize-table/)<br />[Regions recognition](/ocr/recognize-regions/)
PDF | `"resultType": "Pdf"`<br />`"resultType": "TextAndPdf"`<br />`"resultType": "PdfAndHocr"`<br />`"resultType": "TextAndPdfAndHocr"` | [Image recognition](/ocr/recognize-image/)<br />[PDF recognition](/ocr/recognize-pdf/)<br />[Receipt recognition](/ocr/recognize-receipt/)<br />[Regions recognition](/ocr/recognize-regions/)
hOCR | `"resultType": "Hocr"`<br />`"resultType": "TextAndHocr"`<br />`"resultType": "PdfAndHocr"`<br />`"resultType": "TextAndPdfAndHocr"` | [Image recognition](/ocr/recognize-image/)<br />[PDF recognition](/ocr/recognize-pdf/)<br />[Receipt recognition](/ocr/recognize-receipt/)<br />[Regions recognition](/ocr/recognize-regions/)
Excel | `"resultType": "Excel"`<br />`"resultTypeTable": "CsvAndExcel"` | [Table recognition](/ocr/recognize-table/)
CSV | `"resultType": "Csv"`<br />`"resultTypeTable": "CsvAndExcel"` | [Table recognition](/ocr/recognize-table/)
WAV | `"resultType": "Wav"` | [Text to speech conversion](/ocr/text-to-speech/)
PNG | `"resultType": "ImagePNG"` | [Image preprocessing](/ocr/preprocess-image/)

## Important considerations

- You can get more than one result type from a single request. Use combined formats, such as `TextAndPdf`, `TextAndHocr`, `PdfAndHocr`, or `TextAndPdfAndHocr`.
- When the recognition result is returned as PDF, the resulting PDF document will contain the [preprocessed](/ocr/preprocess-image/) image in the background and an invisible text layer on top of it. This text layer can be searched, indexed, selected, and copied.
- Almost all results (including plain text) are returned as Base64 encoded strings. You must decode them to display on the screen or save to a file.
