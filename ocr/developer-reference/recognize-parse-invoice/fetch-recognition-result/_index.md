---
weight: 20
date: "2023-11-27"
author: "Vladimir Lapin"
type: docs
url: /fetch-invoice-recognition-result/
feedback: OCRCLOUD
title: Fetching invoice processing result
description: How to get the parsed invoice data from the Aspose.OCR Cloud queue.
keywords:
- OCR
- recognize
- queue
- get
- obtain
- fetch
- result
- invoice
---

When an invoice is [submitted](/ocr/send-invoice-for-recognition/) for processing, it is [queued](/ocr/recognition-workflow/) to ensure a stable response even under high load. To obtain the result, send a **GET** request to the `https://api.aspose.cloud/v5.0/ocr/RecognizeAndParseInvoice` Aspose.OCR Cloud REST API endpoint. To authorize the request, pass the [access token](/ocr/authorization/) in **Authorization** header (_Bearer authentication_).

Provide the [unique identifier](/ocr/send-invoice-for-recognition/#return-value) of the invoice processing task in `id` parameter:

```bash
curl --request GET --location 'https://api.aspose.cloud/v5.0/ocr/RecognizeAndParseInvoice?id=39b37b24-86e8-4e91-9a99-6c2574853eb5' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA' \
```

## Processing results

The processing result is returned in JSON format in the response body.

```json
{
	"id": "39b37b24-86e8-4e91-9a99-6c2574853eb5",
	"responseStatusCode": "Ok",
	"taskStatus": "Completed",
	"results": [
		{
			"type": "Text",
			"data": "eyJpc3N1ZV9kYXRlIjogIjIwMTctMTEtMjciL...sICJhY2NvdW50IjogIjJ4eHh4MG9veGsifQ=="
		}
	],
	"error": null
}
```

{{% alert color="primary" %}}
Processing results are stored in the Aspose cloud and can be obtained by the task ID within **24 hours** after the invoice was sent to Aspose.OCR Cloud.
{{% /alert %}}

Property | Type | Description
--------- | ---- | -----------
`id` | string | Unique identifier of the invoice processing task. Equals to the value of the `id` request property.
`taskStatus` | string | [Current state](#task-statuses) of the invoice processing task in the queue.
`responseStatusCode` | string | Processing response status.
`results` | Base64 encoded JSON | [Invoice details](#invoice-details) in JSON format.<br />The data is returned as Base64 encoded string. You must decode it to deserialize into an object, display on the screen or save to a file.
`error/messages` | string[] | Processing error messages, if any.<br />Even if the invoice was processed, you can still get notifications and warnings about non-fatal processing errors.

## Invoice details

The parsed invoice contents are returned in JSON format:

```json
{
	"issue_date": "2017-11-27",
	"due_date": "",
	"supplier_name": "abc exports",
	"supplier_address": "4300 longbeach blvd longbeach california 90807 united states",
	"supplier_email": "",
	"supplier_phone": "15627349957",
	"supplier_tax_id": "",
	"receiver_name": "abc imports",
	"receiver_address": "140 wecker road manstield brisbane queensland 4122 australia",
	"receiver_tax_id": "",
	"currency": "usd",
	"total_amount": 43550.0,
	"vat": -1,
	"net_amount": 43550.0,
	"bank_name": "bank of america",
	"bic": "",
	"account": "2xxxx0ooxk"
}
```

At the moment, Aspose.OCR API recognizes the following invoice data:

Property | Format | Description
-------- | ------ | -----------
"issue_date" | string | Invoice issue date in _YYYY-MM-dd_ format.
"due_date" | string | Invoice due date in _YYYY-MM-dd_ format.
"supplier_name" | string | Supplier or service provider name.
"supplier_address" | string | Supplier or service provider address (as one string).
"supplier_email" | string | Supplier or service provider email address.
"supplier_phone" | string | Supplier or service provider phone number (as provided in the invoice, without conversion to international format).
"supplier_tax_id" | string | Supplier or service provider TIN or similar ID.
"receiver_name" | string | Receiver name.
"receiver_address" | string | Receiver address (as one string).
"receiver_tax_id" | string | Receiver TIN or similar ID.
"currency" | string | Invoice currency.
"total_amount" | number | Total (raw) amount due.
"vat" | number | VAT, percent. `-1` if the value is missing in the invoice.
"net_amount" | number | Net amount due.
"bank_name" | string | Supplier's bank name.
"bic" | string |  Supplier's SWIFT or similar code.
"account" | string | Supplier's account number.

{{% alert color="primary" %}}
The availability of the properties above depends on the invoice text and structure.
{{% /alert %}}

## Task statuses

Processing may take up to several seconds depending on the Aspose.OCR cloud load and the size of the original scan or photo. The status of the processing task is indicated in the `taskStatus` property of the processing result.

Status code | Description | To do
----------- | ----------- | ------
Pending | The invoice is queued for processing, but not yet processed. | Try fetching the result in a couple of seconds using the same ID.
Processing | The invoice is currently being processed. | Fetch the result again using the same ID.
Completed | The invoice is processed. | Read the result from `results` property.
Error | An error occurred during processing. | Check messages in the `error` property for more information.
NotExist | The request with the specified ID does not exist, or the result has already been deleted from the cloud storage. | Check the ID or [send the invoice for processing](/ocr/send-invoice-for-recognition/) again with the same parameters.
