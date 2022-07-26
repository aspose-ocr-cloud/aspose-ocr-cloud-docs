---
weight: 10
date: "2022-07-25"
author: "Vladimir Lapin"
type: docs
url: /dsr-mode/
title:  DSR modes
description: List of document structure analysis algorithms that can be used for recognition.
keywords:
- structure
- regions
- areas
- neural network
- algorithm
- DSR
- CRAFT
- mode
---

Aspose.OCR Cloud supports the following [document structure analysis](/ocr/structure-analysis/) algorithms provided in in `dsrMode` request parameter:

Alias             | Parameter value   | Description
----------------- | :---------------: | -----------
`NoDsrNoFilter`   | 3                 | Do no analyze document structure. Can be used when recognizing simple images containing a few lines of text without illustrations or additional formatting.<br />DSR confidence setting is ignored.
`DsrNoFilter`     | 1                 | Use [Document Structure Recognition (DSR)](/ocr/structure-analysis/#document-structure-recognition-dsr) algorithm.<br />Supports [DSR confidence setting](/ocr/dsr-confidence/) for additionally filtering out certain layout blocks.
`DsrAndFilter`    | 2                 | Use [DSR](/ocr/structure-analysis/#document-structure-recognition-dsr) algorithm with a built-in filter that ignores small images. Useful when recognizing images with handwritten marks, inline illustrations, or logos that should not be treated as text.<br />Supports [DSR confidence setting](/ocr/dsr-confidence/) for additionally filtering out certain layout blocks.
`TextDetector`    | 4                 | Use [Character Region Awareness for Text (CRAFT)](/ocr/structure-analysis/#character-region-awareness-for-text-craft) algorithm.<br />DSR confidence setting is ignored.
`DsrPlusDetector` | 5                 | [Combine](/ocr/structure-analysis/#mixed-mode) DSR and CRAFT layout analysis algorithms.<br />Supports [DSR confidence setting](/ocr/dsr-confidence/) for additionally filtering out certain layout blocks.
