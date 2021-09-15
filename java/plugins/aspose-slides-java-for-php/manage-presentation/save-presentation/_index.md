---
title: Save Presentation
type: docs
weight: 70
url: /java/save-presentation/
---

## **Overview**
{{% alert color="primary" %}} 

[Opening Presentation](/slides/java/opening-a-presentation/) described how to use the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class to open a presentation. This article explains how to create and save presentations.

{{% /alert %}} 

The [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class holds a presentation's content. Whether creating a presentation from scratch or modifying an existing one, when finished, you want to save the presentation. With Aspose.Slides for Java, it can be saved as a **file** or **stream**. This article explains how to save a presentation in different ways:

## **Save Presentation to File**
Save a presentation to file by calling the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class [**Save**](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation#save-java.lang.String-int-) method. Simply pass the file name and [**SaveFormat**](https://apireference.aspose.com/slides/java/com.aspose.slides/SaveFormat) to the [**Save**](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation#save-java.lang.String-int-) method.

The examples that follow show how to save a presentation with Aspose.Slides for Java.

```php
// Instantiate a Presentation object that represents a PPT file
$pres = new Java("com.aspose.slides.Presentation");
try {
    // ...do some work here...
    
    // Save your presentation to a file
    $pres->save("demoPass.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Save Presentation to Stream**
It is possible to save a presentation to a stream by passing an output stream to the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class [**Save**](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation#save-java.io.OutputStream-int-) method. There are many types of streams to which a presentation can be saved. In the below example we have created a new Presentation file, add text in shape and Save the presentation to the stream.

```php
// Instantiate a Presentation object that represents a PPT file
$pres = new Java("com.aspose.slides.Presentation");
try {
    $shape = $pres->getSlides()->get_Item(0)->getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Rectangle, 200, 200, 200, 200);

    // Add text to shape
    $shape->getTextFrame()->setText("This demo shows how to Create PowerPoint file and save it to Stream.");

    $os = new Java("java.io.FileOutputStream", "Save_As_Stream_out.pptx");

    $pres->save($os, Java("com.aspose.slides.SaveFormat")->Pptx);

    $os->close();
} catch (JavaException $e) {
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Save Presentation with Predefined View Type**
Aspose.Slides for Java provides a facility to set the view type for the generated presentation when it is opened in PowerPoint through the [ViewProperties](https://apireference.aspose.com/slides/java/com.aspose.slides/ViewProperties) class. The [**setLastView**](https://apireference.aspose.com/slides/java/com.aspose.slides/ViewProperties#setLastView-int-) property is used to set the view type by using the [**ViewType**](https://apireference.aspose.com/slides/java/com.aspose.slides/ViewType) enumerator.

```php
// Opening the presentation file
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Setting view type
    $pres->getViewProperties()->setLastView((new Java("java.lang.Integer", Java("com.aspose.slides.ViewType")->SlideMasterView))->byteValue());
    
    // Saving presentation
    $pres->save("newDemo.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Save Presentation to Strict Open XML Spreadsheet Format**
Aspose.Slides allows you to save the presentation in Strict Open XML format. For that purpose, it provides the [**PptxOptions**](https://apireference.aspose.com/slides/java/com.aspose.slides/pptxoptions) class where you can set the Conformance property while saving the presentation file. If you set its value as [**Conformance.Iso29500_2008_Strict**](https://apireference.aspose.com/slides/java/com.aspose.slides/Conformance#Iso29500_2008_Strict), then the output presentation file will be saved in Strict Open XML format.

The following sample code creates a presentation and saves it in the Strict Open XML Format. While calling the [**Save**](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation#save-java.lang.String-int-com.aspose.slides.ISaveOptions-) method for the presentation, the [**PptxOptions**](https://apireference.aspose.com/slides/java/com.aspose.slides/pptxoptions) object is passed into it with the Conformance property set as [**Conformance.Iso29500_2008_Strict**](https://apireference.aspose.com/slides/java/com.aspose.slides/Conformance#Iso29500_2008_Strict).

```php
// Instantiate a Presentation object that represents a PPT file
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Get the first slide
    $slide = $pres->getSlides()->get_Item(0);
    
    // Add an autoshape of type line
    $slide->getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Line, 50, 150, 300, 0);
    
    //Setting strick XML save options
    $options = new Java("com.aspose.slides.PptxOptions");
    $options->setConformance(Conformance.Iso29500_2008_Strict);
    
    // Save your presentation to a file
    $pres->save("demoPass.pptx", Java("com.aspose.slides.SaveFormat")->Pptx, $options);
} finally {
    if ($pres != null) $pres->dispose();
}

```

## **Save Progress Updates in Percentage**
New [**IProgressCallback**](https://apireference.aspose.com/slides/java/com.aspose.slides/IProgressCallback) interface has been added to [**ISaveOptions**](https://apireference.aspose.com/slides/java/com.aspose.slides/ISaveOptions) interface and [**SaveOptions** ](https://apireference.aspose.com/slides/java/com.aspose.slides/SaveOptions)abstract class. [**IProgressCallback**](https://apireference.aspose.com/slides/java/com.aspose.slides/IProgressCallback) interface represents a callback object for saving progress updates in percentage.  

The following code snippets below show how to use [IProgressCallback](https://apireference.aspose.com/slides/java/com.aspose.slides/IProgressCallback) interface:

```php
// Opening the presentation file
$pres = new Java("com.aspose.slides.Presentation", "ConvertToPDF.pptx");
try {
    $saveOptions = new Java("com.aspose.slides.PdfOptions");
    $saveOptions->setProgressCallback(new Java("com.aspose.slides.ExportProgressHandler"));
    $pres->save("ConvertToPDF.pdf", Java("com.aspose.slides.SaveFormat")->Pdf, $saveOptions);
} finally {
    $pres->dispose();
}
```
```php
class ExportProgressHandler implements IProgressCallback 
{
    public void reporting(double progressValue) 
	{
        // Use progress percentage value here
        $progress = Double.valueOf(progressValue)->intValue();
        echo(progress . "% file converted");
    }
}
```
