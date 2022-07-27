---
weight: 120
date: "2022-07-26"
author: "Vladimir Lapin"
type: docs
url: /structure-analysis/
title:  Document structure analysis
description: How Aspose.OCR Cloud identifies and analyzes the structure of the image during recognition.
keywords:
- structure
- regions
- areas
- neural network
- algorithm
---

A typical scanned image or photo of a text document may contain a large number of different content blocks - text paragraphs, tables, illustrations, formulas, and the like. Detecting, ordering, and classifying areas of interest on a page is the cornerstone of a successful and accurate OCR. This process is called _document structure and layout analysis_.

![Document structure analysis and recognition](structure-analysis.png)

Aspose.OCR Cloud offers several document structure analysis algorithms, allowing you to choose the one that works best for your specific content.

{{% alert color="primary" %}} 
Aspose.OCR Cloud automatically selects the document structure analysis algorithms for you that is suitable for most common use cases. However, you can manually override or tune up the defaults through the API if you are unhappy with the results or get unwanted artifacts.
{{% /alert %}}

Document structure analysis algorithm is specified in an optional [`dsrMode` request parameter](/ocr/dsr-mode/).

## Document structure recognition (DSR)

This algorithm works best with large amounts of structured text such as scanned contracts, book pages, articles, newspapers, and the like. It breaks content into larger blocks, such as paragraphs and columns. These blocks are then analyzed, read and combined into recognition results.

![Document Structure Recognition (DSR)](dsr.png)

_* The example article is Copyright &copy; 2016 CLINICS, distributed under the terms of the Creative Commons license._

DSR algorithm is highly customizable. It allows you [choose](/ocr/dsr-confidence/) how to deal with dim, blurry, or low quality areas of the image, as well as illustrations with text data such as logos and stamps, providing the perfect balance between recognition accuracy and coverage.

However, it may not be suitable for analyzing photographs and small amounts of irregular text - try _Text area analysis_ instead.

## Text area analysis

This algorithm works best with sparse irregular text and low-quality photos. It detects smaller text areas in an image, such as individual words, phrases, or lines, and then positions them relative to each other in recognition results.

![Text Area Analysis](taa.png)

It is optimal for invoices, screenshots, driver's licenses, social security cards, government and work IDs, visas, math formulas, code snippets, and more. It can also detect small texts such as handwritten notes, signatures or stamps. In addition, it is well suited for reading smartphone photos and low-quality scans.

However, this algorithm may be less efficient when dealing with large amounts of structured textual data, such as articles and books. Try _Document structure recognition_ instead.

## Mixed mode

The combination of _Document structure recognition_ and _Text area analysis_. Large blocks of text are detected by DSR, while the remaining content is processed by Text area analysis. This allows you to extract as much text from the image as possible while retaining the powerful DSR tuning capabilities.

This allows you to handle even the most complex cases like posters, billboards, or random photos. A universal algorithm that can take a little longer and may be less efficient than the specialized ones. Try _Document structure recognition_ and _Text area analysis_ if you are sure of the content type.
