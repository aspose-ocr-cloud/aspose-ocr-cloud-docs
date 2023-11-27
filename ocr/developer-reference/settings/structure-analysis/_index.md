---
weight: 20
date: "2023-11-27"
author: "Vladimir Lapin"
type: docs
url: /structure-analysis/
feedback: OCRCLOUD
aliases:
- /dsr-mode/
title:  Document structure analysis
description: How Aspose.OCR Cloud identifies and analyzes the structure of the image during recognition.
keywords:
- structure
- regions
- areas
- neural network
- algorithm
---

A typical scanned image or photo of a text document may contain a large number of different content blocks - text paragraphs, tables, illustrations, formulas, and the like. Detecting, ordering, and classifying areas of interest on a page is the cornerstone of a successful and accurate OCR. This process is called _document structure and layout analysis (DSR)_.

![Document structure analysis and recognition](structure-analysis.png)

Aspose.OCR Cloud offers several document structure analysis algorithms, allowing you to choose the one that works best for your specific content.

{{% alert color="primary" %}} 
Aspose.OCR Cloud automatically selects the document structure analysis algorithms for you that is suitable for most common use cases. However, you can manually override or tune up the defaults through the API if you are unhappy with the results or get unwanted artifacts.
{{% /alert %}}

You can manually override the default document areas detection method if you are unhappy with the results or get unwanted artifacts. Document structure analysis algorithm is specified in an optional recognition setting `dsrMode`:

Value | Description | Use cases
----- | ----------- | ---------
`NoDsrNoFilter` | Do not analyze document structure. | Simple images containing a few lines of text without illustrations or formatting.<br />Applications requiring maximum recognition speed<br />Web applications
`DsrNoFilter` | Detect large blocks of text, such as paragraphs and columns. Optimal for multi-column documents with illustrations. Can be further tuned up with [DSR confidence](/ocr/dsr-confidence/) recognition setting to filter out dim and blurry areas that can lead to unreliable recognition results.<br />See [Complex structure analysis](/ocr/structure-analysis/complex/) for additional details. | Contracts<br />Books<br />Articles<br />Newspapers<br />High-quality scans
`DsrAndFilter` | Do not analyze document structure for small images to maximize recognition speed; use [complex structure analysis](/ocr/structure-analysis/complex/) for large images only. Use this algorithm to accelerate the batch recognition of a large number of diverse images.<br />Can be further tuned up with [DSR confidence](/ocr/dsr-confidence/) setting to filter out dim and blurry areas that can lead to unreliable recognition results. | Batch recognition
`TextDetector` | Find small text blocks (individual words, phrases, or lines) inside complex images and then position these blocks relative to each other in recognition results. This algorithm works best with sparse irregular text and low-quality photos. <br />See [Text area analysis](/ocr/structure-analysis/text/) for additional details. | Invoices<br />Screenshots<br />Driver’s licenses<br />Identity cards<br />Visas<br />Math formulas
`DsrPlusDetector` | The [combination](/ocr/structure-analysis/combined/) of [complex structure analysis](/ocr/structure-analysis/complex/) and [text area analysis](/ocr/structure-analysis/text/). Can be further tuned up with [DSR confidence](/ocr/dsr-confidence/) recognition setting to filter out dim and blurry areas that can lead to unreliable recognition results. | Posters<br />Billboards<br />Datasheets<br />Random photos<br />Batch recognition
`Regions` | Detect blocks of text, such as paragraphs, columns, annotations, and so on. | [Regions detection](/ocr/detect-regions/)
`CraftPoly` | Automatically straighten curved or distorted lines and find small text blocks (individual words, phrases, or lines) inside the resulting image.<br />See [Curved text detection](/ocr/structure-analysis/curved/) for additional details. | Photos of books, magazine articles, and other curved pages.
