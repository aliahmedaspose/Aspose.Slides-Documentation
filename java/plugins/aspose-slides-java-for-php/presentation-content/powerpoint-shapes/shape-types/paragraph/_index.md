---
title: Paragraph
type: docs
weight: 10
url: /java/paragraph/
---


## Get Paragraph and Portion Coordinates in TextFrame ##
Using Aspose.Slides for Java, developers can now get the rectangular coordinates for Paragraph inside paragraphs collection of TextFrame. It also allows you to get [the coordinates of portion](https://apireference.aspose.com/slides/java/com.aspose.slides/IPortion#getCoordinates--) inside portion collection of a paragraph. In this topic, we are going to demonstrate with the help of an example that how to get the rectangular coordinates for paragraph along with position of portion inside a paragraph.

```php
$shape = $pres->getSlides()->get_Item(0)->getShapes()->get_Item(0);
$textFrame = shape->getTextFrame();
foreach( $textFrame->getParagraphs() as $paragraph ){
  foreach( $paragraph->getPortions() as $portion ){
    $point = $portion->getCoordinates();
  }
}
```


## **Get Rectangular Coordinates of Paragraph**
Using [**getRect()**](https://apireference.aspose.com/slides/java/com.aspose.slides/IParagraph#getRect--) method developers can get paragraph bounds rectangle.

```php
$pres = new Java("com.aspose.slides.Presentation", "HelloWorld.pptx");
try {
    $shape = $pres->getSlides()->get_Item(0)->getShapes()->get_Item(0);
    $textFrame = $shape->getTextFrame();
    $rect = $textFrame->getParagraphs()->get_Item(0)->getRect();
    echo("X: " . $rect.x . " Y: " . $rect.y . " Width: " . $rect.width . " Height: " . $rect.height);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Get size of paragraph and portion inside table cell text frame** ##

To get the [Portion](https://apireference.aspose.com/slides/java/com.aspose.slides/Portion) or [Paragraph](https://apireference.aspose.com/slides/java/com.aspose.slides/Paragraph) size and coordinates in a table cell text frame, you can use the [IPortion->getRect](https://apireference.aspose.com/slides/java/com.aspose.slides/IPortion#getRect--) and [IParagraph->getRect](https://apireference.aspose.com/slides/java/com.aspose.slides/IParagraph#getRect--) methods.

This sample code demonstrates the described operation:

```php
$pres = new Java("com.aspose.slides.Presentation", "source.pptx");
try {
    $tbl = (Table)pres->getSlides()->get_Item(0)->getShapes()->get_Item(0);
    $cell = $tbl->getRows()->get_Item(1)->get_Item(1);

    $x = $tbl->getX() + $tbl->getRows()->get_Item(1)->get_Item(1)->getOffsetX();
    $y = $tbl->getY() + $tbl->getRows()->get_Item(1)->get_Item(1)->getOffsetY();

    foreach( $cell->getTextFrame()->getParagraphs() as $para )
    {
        if ($para->getText() == (""))
            continue;

        $rect = $para->getRect();
        $shape =
                $pres->getSlides()->get_Item(0)->getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Rectangle,
                        $rect->getX() + $x, $rect->getY() + $y, $rect->getWidth(), $rect->getHeight());

        $shape->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->NoFill);
        $shape->getLineFormat()->getFillFormat()->getSolidFillColor()->setColor(Java("java.awt.Color")->YELLOW);
        $shape->getLineFormat()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);

        foreach( $para->getPortions() as $portion )
        {
            if ($portion->getText()->contains("0"))
            {
                $rect = $portion->getRect();
                $shape =
                        $pres->getSlides()->get_Item(0)->getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Rectangle,
                                $rect->getX() + $x, $rect->getY() + $y, $rect->getWidth(), $rect->getHeight());

                $shape->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->NoFill);
            }
        }
    }
} finally {
    if ($pres != null) $pres->dispose();
}
```
