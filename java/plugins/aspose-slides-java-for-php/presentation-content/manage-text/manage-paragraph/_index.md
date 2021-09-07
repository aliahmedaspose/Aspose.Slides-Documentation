---
title: Manage Paragraph
type: docs
weight: 30
url: /java/manage-paragraph/
---


## **Multiple Paragraphs having Multiple Portions**
An ITextFame object can have one or more Paragraphs (every paragraph is created through a carriage return), that is a collection of $objects. Furthermore, an $object can have one or more Portions (a collection of IPortion objects. An IPortion object manages text and its formatting properties. So, it means that $object has capacity to handle text with different formatting properties through its underlying IPortion objects.
Please follow the steps below to add TextFrame having 3 paragraphs and 3 portions for each paragraph using Aspose.Slides for Java:

- Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
- Obtain the reference of a slide by using its Index.
- Add an [IAutoShape](https://apireference.aspose.com/slides/java/com.aspose.slides/IAutoShape) of Rectangle type to the slide.
- Access the [ITextFrame](https://apireference.aspose.com/slides/java/com.aspose.slides/ITextFrame) associated with the [IAutoShape](https://apireference.aspose.com/slides/java/com.aspose.slides/IAutoShape).
- Create two [IParagraph](https://apireference.aspose.com/slides/java/com.aspose.slides/IParagraph) objects and add it to the [IParagraphs](https://apireference.aspose.com/slides/java/com.aspose.slides/IParagraph) collection of the [ITextFrame](https://apireference.aspose.com/slides/java/com.aspose.slides/ITextFrame).
- Create three [IPortion](https://apireference.aspose.com/slides/java/com.aspose.slides/IPortion) objects for each new [IParagraph](https://apireference.aspose.com/slides/java/com.aspose.slides/IParagraph) (two Portion objects for default Paragraph) and add each [IPortion](https://apireference.aspose.com/slides/java/com.aspose.slides/IPortion) object to the [IPortions](https://apireference.aspose.com/slides/java/com.aspose.slides/IPortion) collection of each [IParagraph](https://apireference.aspose.com/slides/java/com.aspose.slides/IParagraph).
- Set some text for each [Portion](https://apireference.aspose.com/slides/java/com.aspose.slides/Portion).
- Apply the desired formatting features to each [Portion](https://apireference.aspose.com/slides/java/com.aspose.slides/Portion) using different formatting properties exposed by [IPortion](https://apireference.aspose.com/slides/java/com.aspose.slides/IPortion) object.
- Write the modified presentation as a PPTX file.

The implementation of the above steps is given below.

```php
// Instantiate a Presentation class that represents a PPTX file
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Accessing first slide
    $slide = $pres->getSlides()->get_Item(0);

    // Add an AutoShape of Rectangle type
    $ashp = $slide->getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Rectangle, 50, 150, 300, 150);

    // Access TextFrame of the AutoShape
    $tf = $ashp->getTextFrame();

    // Create Paragraphs and Portions with different text formats
    $para0 = $tf->getParagraphs()->get_Item(0);
    $port01 = new Java("com.aspose.slides.Portion");
    $port02 = new Java("com.aspose.slides.Portion");
    para0->getPortions()->add($port01);
    para0->getPortions()->add($port02);

    $para1 = new Java("com.aspose.slides.Paragraph");
    $tf->getParagraphs()->add($para1);
    $port10 = new Java("com.aspose.slides.Portion");
    $port11 = new Java("com.aspose.slides.Portion");
    $port12 = new Java("com.aspose.slides.Portion");
    $para2->getPortions()->add($port10);
    $para2->getPortions()->add($port11);
    $para2->getPortions()->add($port12);

    $para2 = new Java("com.aspose.slides.Paragraph");
    $tf->getParagraphs()->add($para2);
    $port20 = new Java("com.aspose.slides.Portion");
    $port21 = new Java("com.aspose.slides.Portion");
    $port22 = new Java("com.aspose.slides.Portion");
    $para2->getPortions()->add($port20);
    $para2->getPortions()->add($port21);
    $para2->getPortions()->add($port22);

    for ($i = 0; $i < 3; $i++) 
    {
        for ($j = 0; $j < 3; $j++) 
        {
            $portion = $tf->getParagraphs()->get_Item($i)->getPortions()->get_Item($j); 
            $portion->setText("Portion0" + $j);
            if ($j == 0) {
                $portion->getPortionFormat()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
                $portion->getPortionFormat()->getFillFormat()->getSolidFillColor()->setColor(Java("java.awt.Color")->RED);
                $portion->getPortionFormat()->setFontBold(Java("com.aspose.slides.NullableBool")->True);
                $portion->getPortionFormat()->setFontHeight(15);
            } else if ($j == 1) {
                $portion->getPortionFormat()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
                $portion->getPortionFormat()->getFillFormat()->getSolidFillColor()->setColor(Java("java.awt.Color")->BLUE);
                $portion->getPortionFormat()->setFontItalic(Java("com.aspose.slides.NullableBool")->True);
                $portion->getPortionFormat()->setFontHeight(18);
            }
        }
    }

    //Write PPTX to Disk
    $pres->save("multiParaPort_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Paragraph Indent**
This page will illustrate how we can manage paragraph indent. We will see how developers can use this feature of Aspose.Slides for Java. Please follow the steps below to manage the paragraph indent using Aspose.Slides for Java:

1. Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain the reference of a slide by using its Position.
1. Add a Rectangle shape in the slide.
1. Add a [ITextFrame](https://apireference.aspose.com/slides/java/com.aspose.slides/ITextFrame) with three Paragraphs in the Rectangle.
1. Hide the Lines of the Rectangle.
1. Set indent of each [IParagraph](https://apireference.aspose.com/slides/java/com.aspose.slides/IParagraph) using its BulletOffset property.
1. Write the modified presentation as a PPT file.

The implementation of the above steps is given below.

```php
// Instantiate Presentation Class
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Get first slide
    $sld = $pres->getSlides()->get_Item(0);
    
    // Add a Rectangle Shape
    $rect = $sld->getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Rectangle, 100, 100, 500, 150);
    
    // Add TextFrame to the Rectangle
    $tf = $rect->addTextFrame("This is first line \rThis is second line \rThis is third line");
    
    // Set the text to fit the shape
    $tf->getJava("com.aspose.slides.TextFrameFormat")->setAutofitType(Java("com.aspose.slides.TextAutofitType")->Shape);
    
    // Hide the lines of the Rectangle
    $rect->getLineFormat()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
    
    // Get first Paragraph in the TextFrame and set its Indent
    $para1 = $tf->getParagraphs()->get_Item(0);
    // Setting paragraph bullet style and symbol
    $para2->getJava("com.aspose.slides.ParagraphFormat")->getBullet()->setType(Java("com.aspose.slides.BulletType")->Symbol);
    $para2->getJava("com.aspose.slides.ParagraphFormat")->getBullet()->setChar((char)8226);
    $para2->getJava("com.aspose.slides.ParagraphFormat")->setAlignment(Java("com.aspose.slides.TextAlignment")->Left);
    
    $para2->getJava("com.aspose.slides.ParagraphFormat")->setDepth(2);
    $para2->getJava("com.aspose.slides.ParagraphFormat")->setIndent(30);
    
    // Get second Paragraph in the TextFrame and set its Indent
    $para2 = $tf->getParagraphs()->get_Item(1);
    $para2->getJava("com.aspose.slides.ParagraphFormat")->getBullet()->setType(Java("com.aspose.slides.BulletType")->Symbol);
    $para2->getJava("com.aspose.slides.ParagraphFormat")->getBullet()->setChar((char)8226);
    $para2->getJava("com.aspose.slides.ParagraphFormat")->setAlignment(Java("com.aspose.slides.TextAlignment")->Left);
    $para2->getJava("com.aspose.slides.ParagraphFormat")->setDepth(2);
    $para2->getJava("com.aspose.slides.ParagraphFormat")->setIndent(40);
    
    // Get third Paragraph in the TextFrame and set its Indent
    $para3 = $tf->getParagraphs()->get_Item(2);
    $para3->getJava("com.aspose.slides.ParagraphFormat")->getBullet()->setType(Java("com.aspose.slides.BulletType")->Symbol);
    $para3->getJava("com.aspose.slides.ParagraphFormat")->getBullet()->setChar((char)8226);
    $para3->getJava("com.aspose.slides.ParagraphFormat")->setAlignment(Java("com.aspose.slides.TextAlignment")->Left);
    $para3->getJava("com.aspose.slides.ParagraphFormat")->setDepth(2);
    $para3->getJava("com.aspose.slides.ParagraphFormat")->setIndent(50);
    
    //Write the Presentation to disk
    $pres->save("InOutDent_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **End Paragraph Run Properties for Paragraph**
This page will illustrate how we can manage end paragraph run properties. We will see how developers can use this feature of Aspose.Slides for Java. Please follow the steps below to manage the End paragraph Run Properties using Aspose.Slides for Java:

1. Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain the reference of a slide by using its Position.
1. Add a Rectangle shape in the slide.
1. Add a [TextFrame](https://apireference.aspose.com/slides/java/com.aspose.slides/TextFrame) with two Paragraphs in the Rectangle.
1. Set Font Height and Font type of paragraphs.
1. Set End properties of paragraphs.
1. Write the modified presentation as a PPTX file.

The implementation of the above steps is given below.

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $shape = $pres->getSlides()->get_Item(0)->getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Rectangle, 10, 10, 200, 250);

    $para1 = new Java("com.aspose.slides.Paragraph");
    $para2->getPortions()->add(new Java("com.aspose.slides.Portion", "Sample text"));

    $para2 = new Java("com.aspose.slides.Paragraph");
    $para2->getPortions()->add(new Java("com.aspose.slides.Portion", "Sample text 2"));

    $portionFormat = new Java("com.aspose.slides.PortionFormat");
    $portionFormat->setFontHeight(48);
    $portionFormat->setLatinFont(new  Java("com.aspose.slides.FontData", "Times New Roman"));
    $para2->setEndParagraphPortionFormat($portionFormat);

    $shape->getTextFrame()->getParagraphs()->add($para1);
    $shape->getTextFrame()->getParagraphs()->add($para2);

    $pres->save(resourcesOutputPath+"pres.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Import HTML Text in Paragraphs**
This topic is also part of a series of topics about managing text paragraphs. Aspose.Slides for Java has enhanced support for adding HTML text or saving paragraphs text to HTML. This article shows how to manage paragraphs to use HTML data and shows how developers can use this small yet powerful feature. To manage paragraph bullets using Aspose.Slides for Java:

- Create an instance of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
- Access the desired slide in slide collection using the [ISlide](https://apireference.aspose.com/slides/java/com.aspose.slides/ISlide) object.
- Add an autoshape to the selected slide.
- Add and access the [ITextFrame](https://apireference.aspose.com/slides/java/com.aspose.slides/ITextFrame) of the added shape.
- Remove the default paragraph in the [ITextFrame](https://apireference.aspose.com/slides/java/com.aspose.slides/ITextFrame).
- Read the source HTML file in a TextReader.
- Create the first paragraph instance using the [Paragraph](https://apireference.aspose.com/slides/java/com.aspose.slides/Paragraph) class.
- Add the HTML file content in the read TextReader to the TextFrame's ParagraphCollection.
- Save the presentation.

The implementation of the above steps is given below.

```php
// Create Empty presentation instance
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Acesss the default first slide of presentation
    $slide = $pres->getSlides()->get_Item(0);

    // Adding the AutoShape to accomodate the HTML content
    $ashape = $slide->getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Rectangle, 10, 10,
            $pres->getSlideSize()->getSize()->getWidth() - 20, $pres->getSlideSize()->getSize()->getHeight() - 10);

    $ashape->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->NoFill);

    // Adding text frame to the shape
    $ashape->addTextFrame("");

    // Clearing all paragraphs in added text frame
    $ashape->getTextFrame()->getParagraphs()->clear();

    // Loading the HTML file using stream reader
    $tr = new StreamReader("file.html");

    // Adding text from HTML stream reader in text frame
    $ashape->getTextFrame()->getParagraphs()->addFromHtml($tr->readToEnd());

    // Saving Presentation
    $pres->save("output_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Export Paragraphs Text to HTML**
Please follow the steps below to see how to export the paragraph text to HTML using Aspose.Slides for Java:

- Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class and load the desired presentation.
- Access the desired slide into the slide collection using [ISlide](https://apireference.aspose.com/slides/java/com.aspose.slides/ISlide) object.
- Access the desired shape for which text need to be exported to HTML.
- Access the [TextFrame](https://apireference.aspose.com/slides/java/com.aspose.slides/TextFrame) of the accessed shape.
- Create an instance of StreamWriter and add the new HTML file.
- Export the desired number of paragraphs data by providing starting index to the StreamWriter.
  
The implementation of the above steps is given below.

```php
// Load the presentation file
$pres = new Java("com.aspose.slides.Presentation", "ExportingHTMLText.pptx");
try {
    // Acesss the default first slide of presentation
    $slide = $pres->getSlides()->get_Item(0);

    // Desired index
    $index = 0;

    // Accessing the added shape
    $ashape = $slide->getShapes()->get_Item($index);

    // Creating output HTML file
    $os = new Java("java.io.FileOutputStream", "output.html");
    $writer = new Java("java.io.OutputStreamWriter", $os, "UTF-8");

    //Extracting first paragraph as HTML
    // Writing Paragraphs data to HTML by providing paragraph starting index, total paragraphs to be copied
    $writer->write($ashape->getTextFrame()->getParagraphs().exportToHtml(0, $ashape->getTextFrame()->getParagraphs()->getCount(), null));
    $writer->close();
} catch (JavaException $e) {
} finally {
    if ($pres != null) $pres->dispose();
}
```

