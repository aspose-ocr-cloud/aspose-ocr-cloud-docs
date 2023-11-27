---
weight: 50
date: "2023-11-27"
author: "Vladimir Lapin"
type: docs
url: /dsr-confidence/
feedback: OCRCLOUD
title:  Confidence threshold
description: Threshold for filtering content blocks detected by the complex structure analysis.
keywords:
- structure
- regions
- areas
- blocks
- threshold
- confidence
---

A scanned image, or especially a photograph, may contain areas of varying quality. Some regions may be dim or blurry, some may contain dirt, spots, scratches, glare, unwanted gradients, and other defects. These factors can interfere with recognition and lead to less accurate OCR results or the wrong order of the recognized text.

The [complex structure analysis](/ocr/structure-analysis/complex/) algorithm allows for very flexible filtering of areas with low confidence. You can choose whether to skip such areas and achieve highly reliable OCR results at the cost of losing some of the content, or to extract the maximum amount of text from an image with slightly lower accuracy. This filtering threshold is controlled through `dsrConfidence` recognition setting:

Alias   | Behavior
--------| --------
Default | Synonym for `Mid`.
Low     | Extract most of the text except for very low quality areas.
LowMid  | Extract most of the text except for low quality areas.
Mid     | Skip some blurry or dull areas and image defects. Default behavior that balances recognition accuracy and coverage.
MidHigh | Prefer more accurate recognition at the cost of losing some content from areas of low confidence.
High    | Skip most of the blurry areas and image defects.
Ultra   | Process only the highest quality areas, skipping all others.
All     | Try to extract all the text from the image, regardless of its quality. May lead to less accurate results and artifacts, but can extract text even from illustrations or logos.

If this parameter is omitted, medium (`Mid`) filtering is used, providing a good balance between recognition accuracy and volume of extracted text. As a general rule, it is a good idea to tweak `dsrConfidence` only if you are unhappy with the result:

- If you get unwanted artifacts or prefer maximum recognition accuracy, try setting more aggressive filtering (`Ultra`, `High` or `MidHigh`).  
  Keep in mind, that some content blocks will not be recognized.
- If some blocks of text do not appear in the recognition results, set the value to `Low` or `LowMid`.
- To get all the text from the image, regardless of the accuracy, set the value of the parameter to `All`.

{{% alert color="primary" %}} 
`dsrConfidence` parameter only applies to [complex structure analysis](/ocr/structure-analysis/complex/) and [combined structure analysis](/ocr/structure-analysis/combined/) modes.
{{% /alert %}}
