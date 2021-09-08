---
title: Convert PowerPoint PPT(X) to TIFF
type: docs
weight: 90
url: /java/convert-powerpoint-ppt-and-pptx-to-tiff/
keywords: "PowerPoint PPT(X) to TIFF in java"
description: "Convert PowerPoint PPT(X) to TIFF in Java"
---

## **Convert PPT(X) to TIFF**
{{% alert color="primary" %}} 

TIFF format is known for its flexibility to accommodate multipage images and data. Keeping in view the importance and popularity of [TIFF ](https://wiki.fileformat.com/image/tiff/)format, Aspose.Slides for Java provides the support for converting presentations into TIFF document.

{{% /alert %}} 

The [**Save**](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation#save-java.lang.String-int-com.aspose.slides.ISaveOptions-) method exposed by [Presentation](https://apireference.aspose.com/java/slides/com.aspose.slides/presentation) class can be called by developers to convert the whole presentation into TIFF document. Further, [TiffOptions](https://apireference.aspose.com/java/slides/com.aspose.slides/tiffoptions) class exposes [**ImageSize** ](https://apireference.aspose.com/java/slides/com.aspose.slides/TiffOptions#setImageSize-Dimension-)property enabling the developer to define the size of the image if required.

## **Convert PPT(X) to TIFF with Default Size**
The following example shows how to convert a presentation into a [TIFF](https://wiki.fileformat.com/image/tiff/) document with default options.

```php
// Instantiate a Presentation object that represents a presentation file
$pres = new Java("com.aspose.slides.Presentation", "presentation.pptx");
try {
    // Saving the presentation to TIFF document
    $pres->save("tiff-image.tiff", Java("com.aspose.slides.SaveFormat")->Tiff);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Convert PPT(X) to TIFF with Custom Size**
The following example shows how to convert a presentation into TIFF document with customized image size using [TiffOptions](https://apireference.aspose.com/java/slides/com.aspose.slides/TiffOptions) class.

```php
// Instantiate a Presentation object that represents a Presentation file
$pres = new Java("com.aspose.slides.Presentation", "presentation.pptx");
try {
    // Instantiate the TiffOptions class
    $opts = new Java("com.aspose.slides.TiffOptions");
    
    // Setting compression type
    // Possible values are:
    // Default - Specifies the default compression scheme (LZW).
    // None - Specifies no compression.
    // CCITT3
    // CCITT4
    // LZW
    // RLE
    $opts->setCompressionType(Java("com.aspose.slides.TiffCompressionTypes")->Default);
    
    // Depth – depends on the compression type and cannot be set manually.
    
    // Setting image DPI
    $opts->setDpiX(200);
    $opts->setDpiY(100);
    
    // Set Image Size
    $opts->setImageSize(new Java("java.awt.Dimension", 1728, 1078));
    
    $options = $opts->getNotesCommentsLayouting();
    $options->setNotesPosition(Java("com.aspose.slides.NotesPositions")->BottomFull);
    // Save the presentation to TIFF with specified image size
    $pres->save("tiff-ImageSize.tiff", Java("com.aspose.slides.SaveFormat")->Tiff, $opts);
} finally {
    if ($pres != null) $pres->dispose();
}    
```

## **Convert PPT(X) to TIFF with Custom Image Pixel Format**
The following example shows how to convert a presentation into a TIFF document with customized Image Pixel Format using [TiffOptions](https://apireference.aspose.com/java/slides/com.aspose.slides/TiffOptions) class. You can also include comments in generated TIFF by using [**TiffOptions**](https://apireference.aspose.com/java/slides/com.aspose.slides/TiffOptions) class.

```php
// Instantiate a Presentation object that represents a Presentation file
$pres = new Java("com.aspose.slides.Presentation", "presentation.pptx");
try {
    $options = new Java("com.aspose.slides.TiffOptions");
    $options->setPixelFormat(Java("com.aspose.slides.ImagePixelFormat")->Format8bppIndexed);
    
    /*
     * ImagePixelFormat contains the following values (as could be seen from documentation):
     * Format1bppIndexed; // 1 bits per pixel, indexed.
     * Format4bppIndexed; // 4 bits per pixel, indexed.
     * Format8bppIndexed; // 8 bits per pixel, indexed.
     * Format24bppRgb;    // 24 bits per pixel, RGB.
     * Format32bppArgb;   // 32 bits per pixel, ARGB.
     */
    
    // Save the presentation to TIFF with specified image size
    $pres->save("Tiff-PixelFormat.tiff", Java("com.aspose.slides.SaveFormat")->Tiff, $options);
} finally {
    if ($pres != null) $pres->dispose();
}
```
