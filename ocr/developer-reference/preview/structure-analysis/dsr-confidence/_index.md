---
weight: 20
date: "2022-07-25"
author: "Vladimir Lapin"
type: docs
url: /dsr-confidence/
title:  DSR confidence
description: Threshold for filtering layout blocks detected by the Document Structure Recognition (DSR).
keywords:
- structure
- regions
- areas
- blocks
- threshold
- confidence
---
 
The [Document Structure Recognition (DSR)](/ocr/structure-analysis/#document-structure-recognition-dsr) algorithm detects several thousand overlapping layout blocks per image. As the block detection is performed by the artificial intelligence, there is always a certain degree of uncertainty. For example, some blocks may contain false positives such as an illustration, logo, or stamp that are misinterpreted as a block of text. This will result in unwanted letters or words appearing in the recognition results, or in the wrong order of the recognized text.

To filter out such blocks, you can manually specify region filtering threshold in `dsrConfidence` request parameter.

Alias   | Parameter value
--------| :-------------:
Default | 0
Low     | 1
LowMid  | 2
Mid     | 3
MidHigh | 4
High    | 5
Ultra   | 6
All     | 7

Higher values mean more aggressive filtering, resulting in more blocks to be ignored during recognition.

If this parameter is omitted, medium (`3`) filtering is used, which is suitable for most situations. It is recommended to adjust this setting only if you are not satisfied with the result:

- If the recognized text is in the wrong order or you get unwanted artifacts, try setting higher values.
- If some blocks of text do not appear in the recognition results, decrease the value.

{{% alert color="primary" %}} 
DSR confidence setting only applies to [Document Structure Recognition (DSR)](/ocr/structure-analysis/#document-structure-recognition-dsr) and [mixed](/ocr/structure-analysis/#mixed-mode) layout analysis [modes](/ocr/dsr-mode/).
{{% /alert %}}
