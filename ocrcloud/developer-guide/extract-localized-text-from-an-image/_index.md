---
title: "Extract Localized Text from an Image"
type: docs
url: /extract-localized-text-from-an-image/
weight: 40
---

## **Introduction**
Aspose.OCR Cloud start facilitating text recognition across multiple languages. Therefore, other than English, the API supports French and German Languages so far.

The language parameter accepts integer value:

- 1 for ***English***
- 2 for ***French*** and ***German***
## **API Explorer**
[The API Reference page](https://apireference.aspose.cloud/ocr/) is the easiest way to try out our APIs right away in your browser! It allows you to effortlessly interact and try out every single operation our APIs exposes.
## **cURL Example**
{{< tabs tabTotal="2" tabID="1" tabName1="Request" tabName2="Response" >}}

{{< tab tabNum="1" >}}

```java

curl -v "https://api.aspose.cloud/v3.0/ocr/de\_1.jpg/recognize?language=2" \

-X GET \

-H "Content-Type: application/json" \

-H "Accept: application/json"\

-H "authorization: Bearer <JWT Token>"

```

{{< /tab >}}

{{< tab tabNum="2" >}}

```java

{

    "text": "Nun ist plötzlich Realität was sie jahrelang geübt haben\nEigentlich hatten Castelli und seine Frau geplant auf dem Rückweg von\nPrag ein paar Tage in den österreichischen Alpen zu verbringen. Doch\nnun geht Antonio nicht mehr runter vom Gas er eilt über den Brenner\nund kommt um 14 Uhr im Luigi-Sacco-Krankenhaus in Mailand an das\nEnde der 192oer Jahre als Sanatorium für Tuberkulosepatienten\ngegründet wurde bevor es 1974 zum Universitätskrankenhaus wurde.\nSeine Station ist menschenleer keine Patienten kein Arzt niemand ist\nda. Er begreift sofort dass das was er und seine Kollegen jahrelang\ngeübt und simuliert haben nun plötzlich Realität geworden ist.\nCastelli weiß: Dies ist kein Film sondern es ist an der Zeit dass er sich\nden Bart abrasiert. Den Bart den er seit dreißig Jahren getragen hat.\nDetailansicht öffnen\nDamit die Masken besser haften hat Antonio Castelli sich den Bart\nabrasiert.\nAls er seine Reanimationseinheit betritt blickt Castelli in ein Chaos das\nvon einer schnellen Flucht zeugt. \"\"Also ging ich\" erzählt er \"\"in die\nAbteilung für Infektionskrankheiten wo wir simuliert hatten wie wir mit\nder Ebola-Krise vor fünf Jahren umgehen würden. In der Zeit seit dem\nTelefonat war es meinen Kollegen gelungen die gesamte Station zu\nevakuieren. Sie hatten vier Betten in einer abgeschlossenen Einheit\neingerichtet für Menschen mit hochansteckenden Krankheiten um sie\nmit den ersten Patienten aus Codogno dem Zentrum des Ausbruchs in\nder Lombardei zu belegen. Einer von ihnen - erst 42 Jahre alt - war die\nPerson die als 'Patient zweil bezeichnet wurde und Kontakt mit \"Patient\neins' hatte. Alles schien sich in einem beispiellosen Tempo zu\nverschlimmern. Am darauffolgenden Montag dem 24. Februar wurden\nauf der Intensivstation schon elf Betten benötigt.\"",

    "code": 200

}

```

{{< /tab >}}

{{< /tabs >}}
## **SDKs**
Using an SDK (API client) is the quickest way for a developer to speed up the development. An SDK takes care of a lot of low-level details of making requests and handling responses and lets you focus on writing code specific to your particular project. Check out our [GitHub repository](https://github.com/aspose-ocr-cloud) for a complete list of Aspose.OCR Cloud SDKs along with working examples, to get you started in no time. Please check [Available SDKs](/available-sdks/) article to learn how to add an SDK to your project.
## **SDK Examples**
**Extract Localized Text from an Image**

{{< tabs tabTotal="1" tabID="4" tabName1="C#" >}}

{{< tab tabNum="1" >}}

{{< gist "aspose-cloud" "5bb5820cacb5174de9619dd1d1ce3367" "RecognizeFromStorageDeFR.cs" >}}

{{< /tab >}}

{{< /tabs >}}




