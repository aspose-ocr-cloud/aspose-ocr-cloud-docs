---
weight: 100
date: "2023-03-01"
author: "Vladimir Lapin"
type: docs
url: /preprocess-image/
feedback: OCRCLOUD
title: Image preprocessing
description: Automatic or manual actions for improving an image before sending it for recognition.
keywords:
- preprocess
- correct
- fix
- adjust
---

The accuracy and reliability of text recognition is highly dependent on the quality of the original image. Aspose.OCR Cloud offers a large number of fully automated and manual image processing filters that improve the image and adjust it for OCR.

Filter | Action | Usage scenarios
------ | ------ | ---------------
[Skew correction](/ocr/deskew-image/#automatic-skew-correction) | Automatically straighten images aligned at a slight angle (up to 15 degrees) to the horizontal. | Skewed images
[Rotation](/ocr/deskew-image/#manual-skew-correction) | Manually rotate severely skewed or inverted images. | Images rotated by more than 15 degrees.
[Dewarping](/ocr/dewarp-image/) | Straighten page curvature and fix camera lens distortion. | Photos of curved pages<br />Ultra wide-angle and fisheye photos
[Upsampling](/ocr/upsample-image/) | Intellectually increase the image resolution to improve small font recognition and detection of dense lines. | Medication guides<br />Food labels<br />Small images from the internet
[Binarization](/ocr/binarize-image/) | Convert images to black and white automatically or manually adjust the criteria that determines whether a pixel is considered black or white. | Full color low contrast images
[Contrast correction](/ocr/correct-image-contrast/) | Automatically adjust the image contrast to emphasize small details. | Photos, old papers, text on a background
