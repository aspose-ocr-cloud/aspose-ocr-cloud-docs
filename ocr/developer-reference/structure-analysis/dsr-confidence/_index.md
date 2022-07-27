---
weight: 20
date: "2022-07-25"
author: "Vladimir Lapin"
type: docs
url: /dsr-confidence/
title:  DSR confidence
description: Threshold for filtering content blocks detected by the Document structure recognition (DSR).
keywords:
- structure
- regions
- areas
- blocks
- threshold
- confidence
---

A scanned image, or especially a photograph, may contain areas of varying quality. Some regions may be dim or blurry, some may contain dirt, spots, scratches, glare, unwanted gradients, and other defects. These factors can interfere with recognition and lead to less accurate OCR results or the wrong order of the recognized text.

The [Document Structure Recognition (DSR)](/ocr/structure-analysis/#document-structure-recognition-dsr) algorithm allows for very flexible filtering of areas with low confidence. You can choose whether to skip such areas and achieve highly reliable OCR results at the cost of losing some of the content, or to extract the maximum amount of text from an image with slightly lower accuracy. This filtering threshold is controlled through `dsrConfidence` request parameter.

Alias   | Parameter value | Behavior
--------| :-------------: | --------
Default | 0               | Synonym for `Mid (3)`.
Low     | 1               | Extract most of the text except for very low quality areas.
LowMid  | 2               | Extract most of the text except for low quality areas.
Mid     | 3               | Skip some blurry or dull areas and image defects. Default behavior that balances recognition accuracy and coverage.
MidHigh | 4               | Prefer more accurate recognition at the cost of losing some content from areas of low confidence.
High    | 5               | Skip most of the blurry areas and image defects.
Ultra   | 6               | Process only the highest quality areas, skipping all others.
All     | 7               | Try to extract all the text from the image, regardless of its quality. May lead to less accurate results and artifacts, but can extract text even from illustrations or logos.

Higher values in the range from `1` to `6` mean more aggressive filtering, resulting in more content blocks to be skipped during recognition.

If this parameter is omitted, medium (`3`) filtering is used, providing a good balance between recognition accuracy and volume of extracted text. As a general rule, it is a good idea to tweak `dsrConfidence` only if you are unhappy with the result:

- If you get unwanted artifacts or prefer maximum recognition accuracy, try setting higher values (`4` or higher).
- If some blocks of text do not appear in the recognition results, decrease the value to `1` or `2`.
- To get all the text from the image, regardless of the accuracy, set the value of the parameter to `7`.

{{% alert color="primary" %}} 
`dsrConfidence` parameter only applies to [DSR](/ocr/structure-analysis/#document-structure-recognition-dsr) and [mixed](/ocr/structure-analysis/#mixed-mode) document structure analysis [modes](/ocr/dsr-mode/).
{{% /alert %}}
