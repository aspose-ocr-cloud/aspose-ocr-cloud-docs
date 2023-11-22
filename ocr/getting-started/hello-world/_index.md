---
weight: 40
date: "2023-01-31"
author: "Vladimir Lapin"
type: docs
url: /hello-world/
feedback: OCRCLOUD
aliases:
- /quickstart/
- /how-to-run-the-examples/
title: Hello, world!
description: Get familiar with Aspose.OCR Cloud by running the simplest example on any system.
keywords:
- hello world
- evaluation
- example
- sample
- dummies
- code
---

In this article, you will learn how to extract text from an image file using Aspose.OCR Cloud REST API.

{{% alert color="primary" %}} 
We assume that you have already [signed up](/ocr/sign-up/) to the service and have not yet exceeded your [free subscription plan](/ocr/subscription/) limits.
{{% /alert %}} 

## You will need

- [Any system](/ocr/system-requirements/) with Internet connection.
- Some image with English text. You can take the one from this article.
- A web browser.
- Any tool that allows you to make REST API calls, such as [cURL](https://curl.se/) or [Postman](https://www.postman.com/). This article provides cURL examples.
- **15 minutes** of spare time.

## Get an access token

The Aspose.OCR Cloud API is fully compliant with industry security standards and best practices. Data transfer is carried out using JWT authentication, which eliminates all possibilities of data theft or disclosure.

To obtain a JWT token, get the _Client ID_ and _Client Secret_ credentials:

1. Sign in to [GroupDocs Cloud API Dashboard](https://dashboard.aspose.cloud/).
2. Go to [**Applications**](https://dashboard.aspose.cloud/applications) page.
3. Create the storage. Click the _plus_ icon and follow the required steps.  
   _Internal storage_ with _24-hour_ retention will suffice.
4. Provide the application name, for example, _HelloWorld_.
5. Click **Save** button.
6. Click the newly created **HelloWorld** application and copy the values from **Client Id** and **Client Secret** fields.

Now request an access token with the following API call:

```bash
curl --request POST --location 'https://api.aspose.cloud/connect/token' \
     --header 'Content-Type: application/x-www-form-urlencoded' \
     --data-urlencode 'grant_type=client_credentials' \
     --data-urlencode 'client_id=CLIENT-ID-VALUE' \
     --data-urlencode 'client_secret=CLIENT-SECRET-VALUE'
```

You should get a response that looks like this:

```json
{
	"access_token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA",
	"expires_in": 3600,
	"token_type": "Bearer"
}
```

The string in `access_token` property will be used to authorize further calls to Aspose.OCR Cloud API.

{{% alert color="primary" %}} 
The access token will be valid for the number of seconds specified in the `expires_in` property. If it has expired, request a new one using the same credentials.
{{% /alert %}}

## Encode the image to Base64

An image sent to the Aspose.OCR Cloud REST API must be Base64 encoded. You can use any online tool, for example, [Aspose Base64 online converter](https://products.aspose.app/ocr/img-to-base64):

1. Download the sample image  
   <img src="/ocr/hello-world/source.png" alt="Image to recognize" style="margin-top: 10px; box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);" />
2. Drag the image inside the box and click **Convert to Base64** button.
3. Copy Base64 string to the clipboard.

## Convert the image to text

Make the following API call:

```bash
curl --request POST --location 'https://api.aspose.cloud/v5.0/ocr/RecognizeImage' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA' \
--data-raw '{
  "image": "iVBORw0KGgoAAAANSUh...d1iEAAAAASUVORK5CYII=",
  "settings": {
    "language": "English"
  }
}'
```

- The authorization header must contain the access token obtained [earlier](#getting-an-access-token).
- The `image` property in the request body (the value of the `--data-raw` command-line parameter) must contain a [Base64 encoded image](#encoding-the-image-to-base64).

{{% alert color="primary" %}} 
Read the description of `PostRecognizeImage` API method in [Aspose.Ocr Cloud API Reference](https://api.aspose.cloud/v5.1/ocr/swagger/index.html) for more information on the request parameters.
{{% /alert %}}

Wait a moment. The request will be placed in the queue and you will get its unique identifier. For example:

```
48d50d5b-8ec3-4a8b-8403-e8cfa976f3ad
```

## Fetch the recognition result

Recognition will take a second or two, depending on the size of the image and the current Aspose.Cloud load. After the recognition is completed, the result can be obtained using the following API call:

```bash
curl --request GET --location 'https://api.aspose.cloud/v5.0/ocr/RecognizeImage?id=48d50d5b-8ec3-4a8b-8403-e8cfa976f3ad' \
--header 'Accept: text/plain' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...HaRYOxBcCRCPLnrFCVXpw7UA' \
```

- The authorization header must contain the access token obtained [earlier](#getting-an-access-token).
- The `id` query string parameter must contain the unique identifier of the recognition request returned in the [previous step](#converting-an-image-to-text).

When the image is recognized, you will get the following response:

```json
{
	"id": "a197aade-bba9-4c7a-92c7-46851b3dceaa",
	"responseStatusCode": "Ok",
	"taskStatus": "Completed",
	"results": [
		{
			"type": "Text",
			"data": "QWxsIG1lbiBsaXZlIGVudmVsb3BlZCBpbiB3aGFsZS1saW5lcy4="
		}
	],
	"error": null
}
```

The `data` property contains Base64 encoded text from the image. You can decode it with any online or on-premise decoder, such as [Aspose Base64 online converter](https://products.aspose.app/pdf/conversion/base64). The above code returns the following string:

```
All men live enveloped in whale-lines.
```

{{% alert color="primary" %}} 
Aspose.OCR Cloud will keep the recognition result in its internal storage for **24 hours**.
{{% /alert %}}

## Live sample

{{< blocks/feature >}}
<!-- BEGIN LCS -->
<div class="ocr-lcs">
	<style>
		.col-lg-4 {
			text-align: left !important;
			max-width: 100% !important;
			padding: 0 !important;
		}

		.ocr-lcs {
			width: 100%;
			box-sizing: border-box;
		}

		.ocr-lcs-controls {
			display: flex;
			flex-wrap: wrap;
		}

		.ocr-lcs-drop {
			cursor: pointer;
			display: flex;
			flex-direction: column;
			align-items: center;
			min-width: 350px;
			box-sizing: border-box;
			margin: 0 15px 15px 0;
			padding: 15px 15px 10px 15px;
			border: dashed 3px #73b5fb;
			border-radius: 10px;
			background-color: #ffffff;
		}

		.ocr-lcs-drop input {
			display: none;
		}

		.ocr-lcs-drop-preload {
			display: none;
		}

		.ocr-lcs-drop svg {
			width: 48px;
			margin-bottom: 5px;
			filter: invert(70%) sepia(12%) saturate(3506%) hue-rotate(183deg) brightness(101%) contrast(97%);
		}

		.ocr-lcs-drop span {
			font-size: 18px;
			text-align: center;
		}

		.ocr-lcs-filename {
			display: none;
		}

		.ocr-lcs-filename span {
			font-style: italic;
		}

		.ocr-lcs-recognizing {
			display: none;
		}

		.ocr-lcs-recognizing span {
			font-style: italic;
		}

		.ocr-lcs-mods {
			display: flex;
			flex-direction: column;
		}

		.ocr-lcs-mods > * {
			width: 150px;
			box-sizing: border-box;
		}

		.ocr-lcs-mods select {
			margin-bottom: 7px;
			padding: .6em 1.4em .5em .8em;
			border:  solid 2px #73b5fb;
			border-radius: .5em;
			line-height: 1.3;
			font-family: arial,sans-serif,-apple-system,BlinkMacSystemFont,segoe ui,Roboto,helvetica neue,apple color emoji,segoe ui emoji,segoe ui symbol;
			font-size: 16px;
			font-weight: 700;
			color: #73b5fb;
			-moz-appearance: none;
			-webkit-appearance: none;
			appearance: none;
			background-color: #ffffff;
			background-image: url('data:image/svg+xml;charset=US-ASCII,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22292.4%22%20height%3D%22292.4%22%3E%3Cpath%20fill%3D%22%2373b5fb%22%20d%3D%22M287%2069.4a17.6%2017.6%200%200%200-13-5.4H18.4c-5%200-9.3%201.8-12.9%205.4A17.6%2017.6%200%200%200%200%2082.2c0%205%201.8%209.3%205.4%2012.9l128%20127.9c3.6%203.6%207.8%205.4%2012.8%205.4s9.2-1.8%2012.8-5.4L287%2095c3.5-3.5%205.4-7.8%205.4-12.8%200-5-1.9-9.2-5.5-12.8z%22%2F%3E%3C%2Fsvg%3E');
			background-repeat: no-repeat, repeat;
			background-position: right .7em top 50%, 0 0;
			background-size: .65em auto, 100%;
		}

		.ocr-lcs-mods select::-ms-expand {
			display: none;
		}

		.ocr-lcs-mods select:hover, .ocr-lcs-mods select:focus {
			border-color: #1a89d0;
			color: #1a89d0;
			background-image: url('data:image/svg+xml;charset=US-ASCII,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22292.4%22%20height%3D%22292.4%22%3E%3Cpath%20fill%3D%22%231a89d0%22%20d%3D%22M287%2069.4a17.6%2017.6%200%200%200-13-5.4H18.4c-5%200-9.3%201.8-12.9%205.4A17.6%2017.6%200%200%200%200%2082.2c0%205%201.8%209.3%205.4%2012.9l128%20127.9c3.6%203.6%207.8%205.4%2012.8%205.4s9.2-1.8%2012.8-5.4L287%2095c3.5-3.5%205.4-7.8%205.4-12.8%200-5-1.9-9.2-5.5-12.8z%22%2F%3E%3C%2Fsvg%3E');
		}

		.ocr-lcs-mods select:focus {
			outline: none;
		}

		*[dir="rtl"] .ocr-lcs-mods select, :root:lang(ar) .ocr-lcs-mods select, :root:lang(iw) .ocr-lcs-mods select {
			background-position: left .7em top 50%, 0 0;
			padding: .6em .8em .5em 1.4em;
		}

		.ocr-lcs-mods select option {
			font-weight: normal;
			color: #4c4c4c;
		}

		.ocr-lcs-mods input {
			padding: 0.6em .6em;
			border: none;
			border-radius: .5em;
			box-shadow: inset 0 1px rgb(255 255 255 / 15%), 0 1px 1px rgb(0 0 0 / 8%);
			font-family: arial,sans-serif,-apple-system,BlinkMacSystemFont,segoe ui,Roboto,helvetica neue,apple color emoji,segoe ui emoji,segoe ui symbol;
			font-size: 16px;
			font-weight: 700;
			color: #ffffff;
			background-color: #1a89d0;
		}

		.ocr-lcs-mods input:hover {
			background-color: #3071a9;
			transition: all .3s ease;
			transition-property: all;
			transition-duration: 0.3s;
			transition-timing-function: ease;
			transition-delay: 0s;
		}

		.ocr-lcs-disabled {
			background-color: silver !important;
		}

		.ocr-lcs-disclaimer {
			font-size: 12px !important;
		}

		.ocr-lcs-result {
			position: fixed;
			top: 0px;
			right: 0px;
			bottom: 0px;
			left: 0px;
			background: rgba(0,0,0,0.8);
			z-index: 9998;
			-webkit-transition: opacity 400ms ease-in;
			-moz-transition: opacity 400ms ease-in;
			transition: opacity 400ms ease-in;
			display: none;
		}

		.ocr-lcs-result > div {
			width: 90vw;
			position: relative;
			margin: 10% auto;
			padding: 5px 20px 13px 20px;
			border-radius: 10px;
			background: #ffffff;
			pointer-events: auto;
		}

		.ocr-lcs-result header {
			position: relative;
			display: flex;
			justify-content: space-between;
			align-items: center;
			padding:  5px 0 10px 0;
			border-bottom: dotted 1px #1a89d0;
		}

		.ocr-lcs-result header span {
			font-size: 18px;
			font-weight: 700;
		}

		.ocr-lcs-result header i {
			cursor: pointer;
			color: #1a89d0;
			font-size: 24px !important;
		}

		.ocr-lcs-result header i:hover {
			color: #3071a9;
		}

		.ocr-lcs-result article {
			max-height: 500px;
			overflow: auto;
			margin: 25px 0 15px 0;
		}
	</style>
	<div class="ocr-lcs-controls">
		<div class="ocr-lcs-drop" onclick="OcrLcsUpload(this);" ondragover="event.preventDefault();" ondrop="OcrLcsDropped(event,this);">
			<input type="file" accept=".jpg,.jpeg,.png,.bmp,.tif,.tiff,.gif" onchange="OcrLcsFileSelected(this);" />
			<svg class="ocr-lcs-drop-preload" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 100 100"><g transform="translate(89,50)"><g transform="rotate(0)"><circle cx="0" cy="0" r="5" fill="#29c26a" fill-opacity="1"><animateTransform attributeName="transform" type="scale" begin="-0.8888888888888888s" values="2 2;1 1" keyTimes="0;1" dur="1s" repeatCount="indefinite"></animateTransform><animate attributeName="fill-opacity" keyTimes="0;1" dur="1s" repeatCount="indefinite" values="1;0" begin="-0.8888888888888888s"></animate></circle></g></g><g transform="translate(79.87573328164014,75.06871677777502)"><g transform="rotate(40)"><circle cx="0" cy="0" r="5" fill="#29c26a" fill-opacity="0.8888888888888888"><animateTransform attributeName="transform" type="scale" begin="-0.7777777777777778s" values="2 2;1 1" keyTimes="0;1" dur="1s" repeatCount="indefinite"></animateTransform><animate attributeName="fill-opacity" keyTimes="0;1" dur="1s" repeatCount="indefinite" values="1;0" begin="-0.7777777777777778s"></animate></circle></g></g><g transform="translate(56.772278929010284,88.40750236747611)"><g transform="rotate(80)"><circle cx="0" cy="0" r="5" fill="#29c26a" fill-opacity="0.7777777777777778"><animateTransform attributeName="transform" type="scale" begin="-0.6666666666666666s" values="2 2;1 1" keyTimes="0;1" dur="1s" repeatCount="indefinite"></animateTransform><animate attributeName="fill-opacity" keyTimes="0;1" dur="1s" repeatCount="indefinite" values="1;0" begin="-0.6666666666666666s"></animate></circle></g></g><g transform="translate(30.500000000000007,83.77499074759311)"><g transform="rotate(119.99999999999999)"><circle cx="0" cy="0" r="5" fill="#29c26a" fill-opacity="0.6666666666666666"><animateTransform attributeName="transform" type="scale" begin="-0.5555555555555556s" values="2 2;1 1" keyTimes="0;1" dur="1s" repeatCount="indefinite"></animateTransform><animate attributeName="fill-opacity" keyTimes="0;1" dur="1s" repeatCount="indefinite" values="1;0" begin="-0.5555555555555556s"></animate></circle></g></g><g transform="translate(13.351987789349579,63.33878558970109)"><g transform="rotate(160)"><circle cx="0" cy="0" r="5" fill="#29c26a" fill-opacity="0.5555555555555556"><animateTransform attributeName="transform" type="scale" begin="-0.4444444444444444s" values="2 2;1 1" keyTimes="0;1" dur="1s" repeatCount="indefinite"></animateTransform><animate attributeName="fill-opacity" keyTimes="0;1" dur="1s" repeatCount="indefinite" values="1;0" begin="-0.4444444444444444s"></animate></circle></g></g><g transform="translate(13.351987789349572,36.661214410298925)"><g transform="rotate(200)"><circle cx="0" cy="0" r="5" fill="#29c26a" fill-opacity="0.4444444444444444"><animateTransform attributeName="transform" type="scale" begin="-0.3333333333333333s" values="2 2;1 1" keyTimes="0;1" dur="1s" repeatCount="indefinite"></animateTransform><animate attributeName="fill-opacity" keyTimes="0;1" dur="1s" repeatCount="indefinite" values="1;0" begin="-0.3333333333333333s"></animate></circle></g></g><g transform="translate(30.499999999999982,16.2250092524069)"><g transform="rotate(239.99999999999997)"><circle cx="0" cy="0" r="5" fill="#29c26a" fill-opacity="0.3333333333333333"><animateTransform attributeName="transform" type="scale" begin="-0.2222222222222222s" values="2 2;1 1" keyTimes="0;1" dur="1s" repeatCount="indefinite"></animateTransform><animate attributeName="fill-opacity" keyTimes="0;1" dur="1s" repeatCount="indefinite" values="1;0" begin="-0.2222222222222222s"></animate></circle></g></g><g transform="translate(56.77227892901027,11.59249763252388)"><g transform="rotate(280)"><circle cx="0" cy="0" r="5" fill="#29c26a" fill-opacity="0.2222222222222222"><animateTransform attributeName="transform" type="scale" begin="-0.1111111111111111s" values="2 2;1 1" keyTimes="0;1" dur="1s" repeatCount="indefinite"></animateTransform><animate attributeName="fill-opacity" keyTimes="0;1" dur="1s" repeatCount="indefinite" values="1;0" begin="-0.1111111111111111s"></animate></circle></g></g><g transform="translate(79.87573328164014,24.931283222224955)"><g transform="rotate(320)"><circle cx="0" cy="0" r="5" fill="#29c26a" fill-opacity="0.1111111111111111"><animateTransform attributeName="transform" type="scale" begin="0s" values="2 2;1 1" keyTimes="0;1" dur="1s" repeatCount="indefinite"></animateTransform><animate attributeName="fill-opacity" keyTimes="0;1" dur="1s" repeatCount="indefinite" values="1;0" begin="0s"></animate></circle></g></g><!-- [ldio] generated by https://loading.io/ --></svg>
			<svg class="ocr-lcs-drop-icon" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 128 128"><path d="M80,0v32h32L80,0z M72,32V0H28c-6.63,0-12,5.37-12,12v104c0,6.62,5.37,12,12,12h72c6.63,0,12-5.37,12-12V40H80.22	C75.57,40,72,36.42,72,32z M88.03,86.03C87.07,87.43,85.55,88,84,88s-3.07-0.59-4.24-1.76L70,76.47V102c0,3.31-2.69,6-6,6	s-6-2.69-6-6V76.47l-9.76,9.76c-2.34,2.34-6.14,2.34-8.49,0s-2.34-6.14,0-8.49l20-20c2.34-2.34,6.14-2.34,8.49,0l20,20	C90.57,80.1,90.57,83.9,88.03,86.03z"/></svg>
			<span class="ocr-lcs-filename">Ready to recognize <span></span></span>
			<span class="ocr-lcs-recognizing">Recognizing <span></span></span>
			<span class="ocr-lcs-hint">Drop a file here or click to browse *</span>
		</div>
		<div class="ocr-lcs-mods">
			<select name="language">
				<option value="39">Albanian</option>
				<option value="24">Arabic</option>
				<option value="45">Azerbaijani </option>
				<option value="27">Bengali</option>
				<option value="44">Bulgarian</option>
				<option value="22">Chinese</option>
				<option value="17">Croatian</option>
				<option value="18">Czech</option>
				<option value="13">Danish</option>
				<option value="10">Dutch</option>
				<option value="1" selected="selected">English</option>
				<option value="20">Estonian</option>
				<option value="15">Finnish</option>
				<option value="3">French</option>
				<option value="43">Georgian</option>
				<option value="2">German</option>
				<option value="36">Greek</option>
				<option value="34">Hebrew</option>
				<option value="25">Hindi</option>
				<option value="33">Indonesian</option>
				<option value="4">Italian</option>
				<option value="37">Japanese</option>
				<option value="40">Latin</option>
				<option value="35">Javanese</option>
				<option value="32">Korean</option>
				<option value="12">Latvian</option>
				<option value="11">Lithuanian</option>
				<option value="14">Norwegian</option>
				<option value="38">Persian</option>
				<option value="7">Polish</option>
				<option value="6">Portuguese</option>
				<option value="21">Romanian</option>
				<option value="23">Russian</option>
				<option value="16">Serbian</option>
				<option value="9">Slovak</option>
				<option value="8">Slovenian</option>
				<option value="5">Spanish</option>
				<option value="19">Swedish</option>
				<option value="28">Tibetan</option>
				<option value="29">Thai</option>
				<option value="31">Turkish</option>
				<option value="26">Ukrainian</option>
				<option value="30">Urdu</option>
				<option value="42">Uzbek</option>
				<option value="41">Vietnamese</option>
			</select>
			<input type="button" value="Run code" class="ocr-lcs-recognize ocr-lcs-disabled" onclick="OcrLcsRecognize(this)" />
		</div>
	</div>
	<p class="ocr-lcs-disclaimer">* By uploading your files or using the service you agree with our <a href="https://about.aspose.com/legal/terms-of-use" rel="nofollow noreferrer" target="_blank">Terms of use</a> and <a href="https://about.aspose.com/legal/privacy-policy" rel="nofollow noreferrer" target="_blank">Privacy Policy</a>.</p>
	<div class="ocr-lcs-result" onclick="OcrLcsCurtainClick(this)">
		<div>
			<header>
				<span>Recognition result</span>
				<i class="fa fa-times" onclick="OcrLcsCloseResult(this);"></i>
			</header>
			<article>&nbsp;</article>
		</div>
	</div>
	<script>
		function OcrLcsUpload(obj)
		{
			let fileInput = $(obj).children("input[type='file']")[0];
			fileInput.click();
		}

		function OcrLcsDropped(event, obj)
		{
			let fileInput = $(obj).children("input[type='file']")[0];
			fileInput.files = event.dataTransfer.files;
			OcrLcsFileSelected(fileInput);
			event.preventDefault();
			return false;
		}

		function OcrLcsFileSelected(obj)
		{
			if(obj.files.length > 0)
			{
				let fileName = obj.value.replace(/.*[\/\\]/, "");
				$(obj).closest(".ocr-lcs-controls").find(".ocr-lcs-recognize").removeClass("ocr-lcs-disabled");
				$(obj).siblings(".ocr-lcs-filename").show().children("span").text(fileName);
				$(obj).siblings(".ocr-lcs-recognizing").children("span").text(fileName);
			}
		}

		function OcrLcsRecognize(obj)
		{
			let button = $(obj);
			if(button.hasClass("ocr-lcs-disabled")) return false;
			let icon = button.closest(".ocr-lcs-controls").find(".ocr-lcs-drop-icon");
			let preloader = button.closest(".ocr-lcs-controls").find(".ocr-lcs-drop-preload");
			let recognizingField = button.closest(".ocr-lcs-controls").find(".ocr-lcs-recognizing");
			let filenameField = button.closest(".ocr-lcs-controls").find(".ocr-lcs-filename");
			let hint = button.closest(".ocr-lcs-controls").find(".ocr-lcs-hint");
			preloader.show();
			recognizingField.show();
			icon.hide();
			filenameField.hide();
			hint.hide();
			button.addClass("ocr-lcs-disabled");
			let lang = button.siblings("select").val();
			let file = button.closest(".ocr-lcs-controls").find("input[type='file']")[0].files[0];
			let payload = new FormData();
			payload.append("language", lang);
			payload.append("attachfile", file);
			$.ajax({
				url: "https://api.products.aspose.app/ocr/conversion/RecognizeImageFromVidget",
				type: "POST",
				data: payload,
				processData: false,
				contentType: false
			}).done(function(data){
				let resultDialog = button.closest(".ocr-lcs").find(".ocr-lcs-result");
				let output = data.replace(/(?:\r\n|\r|\n)/g, "<br />");
				resultDialog.find("article").html(output);
				resultDialog.slideDown(200);
			}).fail(function(jqxhr,textStatus,error){
				console.log(`[${textStatus}] ${error}`);
			}).always(function(){
				preloader.hide();
				recognizingField.hide();
				icon.show();
				hint.show();
				button.closest(".ocr-lcs-controls").find("input[type='file']")[0].value = null;
			});
		}

		function OcrLcsCurtainClick(obj)
		{
			if($(event.target).is(".ocr-lcs-result")) $(obj).hide();
		}

		function OcrLcsCloseResult(obj)
		{
			$(obj).closest(".ocr-lcs-result").slideUp(200);
		}
	</script>
</div>
<!-- END LCS -->
{{< /blocks/feature >}}

## What’s next?

Congratulations! You have successfully recognized the text in the image. Read the [Developer's reference](/ocr/developer-reference/) and [API Reference](https://api.aspose.cloud/v5.1/ocr/swagger/index.html?urls.primaryName=V5.1) for details on creating advanced optical character recognition solutions with Aspose.OCR Cloud.

You can also check [Aspose.OCR Cloud GitHub repositories](https://github.com/aspose-ocr-cloud) for code examples in various programming languages, demonstrating advanced OCR API capabilities. If you like to add or improve an example, we encourage you to contribute to the project. Fork the repository, edit the source code and create a pull request. We will review the changes and include it in the repository if found helpful.
