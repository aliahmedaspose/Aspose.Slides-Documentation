---
title: Convert PowerPoint PPT(X) to PDF Notes
type: docs
weight: 50
url: /java/convert-powerpoint-ppt-and-pptx-to-pdf-notes/
keywords: "convert powerpoint to pdf notes in java"
description: "Convert PowerPoint to PDF notes in Java"
---

## **Convert PowerPoint to PDF with Custom Slide Size**
The following example shows how to convert a presentation to a PDF notes document with custom slide size. Where each inch equals 72.

```php
// Instantiate a Presentation object that represents a presentation file
$presIn = new Java("com.aspose.slides.Presentation", "SelectedSlides.pptx");
$presOut = new Java("com.aspose.slides.Presentation");
try {
    $slide = presIn->getSlides()->get_Item(0);
    $presOut->getSlides()->insertClone(0, $slide);
    
    // Setting Slide Type and Size
    $presOut->getSlideSize()->setSize(612, 792, Java("com.aspose.slides.SlideSizeScaleType")->EnsureFit);
        
    $pdfOptions = new Java("com.aspose.slides.PdfOptions");
    $pdfOptions->getNotesCommentsLayouting()->setNotesPosition(Java("com.aspose.slides.NotesPositions")->BottomFull);

    $presOut->save("PDF-SelectedSlide.pdf", Java("com.aspose.slides.SaveFormat")->Pdf, $pdfOptions);
} finally {
    if ($presIn != null) $presIn->dispose();
    if ($presOut != null) $presOut->dispose();
}
```

## **Convert PowerPoint to PDF in Notes Slide View**
The [**Save**](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation#save-java.lang.String-int-) method exposed by [**Presentation**](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class can be used to convert the whole presentation in Notes Slide view to PDF. The code snippets below update the sample presentation to PDF in Notes Slide view.

```php
$pres = new Java("com.aspose.slides.Presentation", "presentation.pptx");
try {
    $pdfOptions = new Java("com.aspose.slides.PdfOptions");
    $pdfOptions->getNotesCommentsLayouting()->setNotesPosition(Java("com.aspose.slides.NotesPositions")->BottomFull);

    $pres->save($resourcesOutputPath+"PDF-Notes.pdf", Java("com.aspose.slides.SaveFormat")->Pdf, $pdfOptions);
} finally {
    if ($pres != null) $pres->dispose();
}
```