---
weight: 10
date: "2022-07-26"
author: "Vladimir Lapin"
type: docs
url: /dsr-mode/
title:  DSR modes
description: List of document structure analysis methods that can be used for recognition.
keywords:
- structure
- regions
- areas
- neural network
- algorithm
- DSR
- mode
---

Aspose.OCR Cloud supports the following [document structure analysis](/ocr/structure-analysis/) methods provided in in `dsrMode` request parameter:

Alias             | Parameter value   | Description | Use cases
----------------- | :---------------: | ----------- | ---------
`NoDsrNoFilter`   | 3                 | Do not analyze document structure.<br />DSR confidence setting is ignored. | Simple images containing a few lines of text without illustrations or additional formatting. The fastest recognition method, but may not be suitable for large amounts of structured text and photos.
`DsrNoFilter`     | 1                 | Use [Document structure recognition (DSR)](/ocr/structure-analysis/#document-structure-recognition-dsr) algorithm.<br />Can be further tuned up with [DSR confidence setting](/ocr/dsr-confidence/) to filter out dim and blurry areas that can lead to unreliable recognition results. | Contracts<br />Books<br />Articles<br />Newspapers<br />High-quality scans
`DsrAndFilter`    | 2                 | Do not analyze document structure for small images; use [Document structure recognition (DSR)](/ocr/structure-analysis/#document-structure-recognition-dsr) for large images.<br />Can be further tuned up with [DSR confidence setting](/ocr/dsr-confidence/) (large images only) to filter out dim and blurry areas that can lead to unreliable recognition results. | Batch recognition of a large number of different images.
`TextDetector`    | 4                 | Use [Text area analysis](/ocr/structure-analysis/#text-area-analysis) algorithm.<br />DSR confidence setting is ignored. | Invoices<br />Driver’s licenses<br />Social security cards<br />Government and work IDs<br />Visas<br /> Photos<br />Screenshots
`DsrPlusDetector` | 5                 | The [combination](/ocr/structure-analysis/#mixed-mode) of _Document structure recognition_ and _Text area analysis_.<br />Can be further tuned up with [DSR confidence setting](/ocr/dsr-confidence/) to filter out dim and blurry areas that can lead to unreliable recognition results. | Posters<br />Billboards<br />Datasheets<br />Random photos<br />Batch recognition
