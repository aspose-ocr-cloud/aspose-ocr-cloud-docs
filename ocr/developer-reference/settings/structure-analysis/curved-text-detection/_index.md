---
weight: 40
date: "2023-03-06"
author: "Vladimir Lapin"
type: docs
url: /structure-analysis/curved
feedback: OCRCLOUD
title:  Curved text detection
description: How Aspose.OCR Cloud determines the structure of curved or distorted pages.
keywords:
- structure
- region
- area
- photo
- distort
- curve
---

When photographing pages of books and magazine articles, the cylindrical curvature of the page results in distortion of the image, causing the lines of text to curl. It makes regular recognition algorithms unsuitable.

Curved text detection algorithm uses a specialized neural network that automatically tracks and rectifies curved lines of text. This greatly improves recognition accuracy and allows much more text to be recovered and extracted.

![Detecting and rectifying curved lines of text](curved_text.png)

However, this algorithm is less efficient and consumes more resources when dealing with perfectly straight images, such as a single scanned sheet of paper. Try [complex structure analysis](/ocr/structure-analysis/complex/) or [text area analysis](/ocr/structure-analysis/text/) instead.
