---
title: Portion
type: docs
weight: 10
url: /java/portion/
---

## **Get Position Coordinates of Portion**
[**getCoordinates()**](https://apireference.aspose.com/slides/java/com.aspose.slides/IPortion#getCoordinates--) method has been added to [IPortion](http://www.aspose.com/api/java/slides/com.aspose.slides/interfaces/IPortion) and [Portion](http://www.aspose.com/api/java/slides/com.aspose.slides/classes/Portion) class which allows retrieving the coordinates of the beginning of the portion.

```php
// Instantiate Prseetation class that represents the PPTX
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Reshaping the context of presentation
    $shape = $pres->getSlides()->get_Item(0)->getShapes()->get_Item(0);
    
    $textFrame = (ITextFrame) $shape->getTextFrame();
    
    for ($paragraph : $textFrame->getParagraphs()) 
    {
        for ($portion : paragraph->getPortions()) 
        {
            $point = $portion->getCoordinates();
            echo("X: " + point.x + " Y: " + point.y);
        }
    }
} finally {
    if ($pres != null) $pres->dispose();
}
```
