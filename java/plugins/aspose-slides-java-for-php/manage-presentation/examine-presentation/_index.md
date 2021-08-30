---
title: Examine Presentation
type: docs
weight: 30
url: /java/examine-presentation/

---

Aspose.Slides for Java allows you to examine a presentation to find out its properties and understand its behavior. 

{{% alert title="TIP" color="dark" %}} 

The [PresentationInfo](https://apireference.aspose.com/slides/java/com.aspose.slides/PresentationInfo) class contains most of the properties and methods needed for operations here. 

{{% /alert %}} 

## **Checking a Presentation Format**

Before working on a presentation, you may want to find out what format (PPT, PPTX, ODP, and others) the presentation is in at the moment.

You can check a presentation's format without loading the presentation. See this sample code:

```php
$info = Java("com.aspose.slides.PresentationFactory")->getInstance()->getPresentationInfo("pres.pptx");
echo($info->getLoadFormat()); // PPTX

$info2 = Java("com.aspose.slides.PresentationFactory")->getInstance()->getPresentationInfo("pres.ppt");
echo(info2->getLoadFormat()); // PPT

$info3 = Java("com.aspose.slides.PresentationFactory")->getInstance()->getPresentationInfo("pres.odp");
echo(info3->getLoadFormat()); // ODP
```

## **Getting the Properties of a Presentation**

This sample code in Java shows you how to get a presentation’s properties (information about the presentation):

```php
$info = Java("com.aspose.slides.PresentationFactory")->getInstance()->getPresentationInfo("pres.pptx");
$props = $info->readDocumentProperties();
echo($props->getCreatedTime());
echo($props->getSubject());
echo($props->getTitle());
// .. 
```

## **Updating the Properties of a Presentation**

Aspose.Slides provides the [PresentationInfo.updateDocumentProperties](https://apireference.aspose.com/slides/java/com.aspose.slides/PresentationInfo#updateDocumentProperties-com.aspose.slides.IDocumentProperties-) method that allows you to make changes to a presentation’s properties.

This sample code shows you how to edit the properties for a presentation in Java:

```php
$info = Java("com.aspose.slides.PresentationFactory")->getInstance()->getPresentationInfo("pres.pptx");

$props = $info->readDocumentProperties();
$props->setTitle("My title");
$info->updateDocumentProperties($props);
```

### **Useful Links**

To get more information about a presentation and its security attributes, you may find these links useful:

- [Checking whether a Presentation is Encrypted](https://docs.aspose.com/slides/java/password-protected-presentation/#checking-whether-a-presentation-is-encrypted)
- [Checking whether a Presentation is Write Protected (read-only)](https://docs.aspose.com/slides/java/password-protected-presentation/#checking-whether-a-presentation-is-write-protected)
- [Confirming the Password Used to Protect a Presentation](https://docs.aspose.com/slides/java/password-protected-presentation/#validating-or-confirming-that-a-specific-password-has-been-used-to-protect-a-presentation)