---
weight: 110
date: "2022-07-21"
author: "Vladimir Lapin"
type: docs
url: /recognition-results-list/
title: Recognition result types
description: The list of values of resultType request parameter.
keywords:
- target
- result
- save
---

`resultType` parameter allows you to specify the [formats](/ocr/supported-file-formats/#recognition-results) in which you want to get recognition results.

Alias    | Parameter value
-------- | :-------------:
Text     | 1
PDF      | 2
hOCR     | 4
Internal | 8

{{% alert color="primary" %}} 
You can request the recognition result in several formats by specifying the appropriate values separated by commas.
{{% /alert %}}
