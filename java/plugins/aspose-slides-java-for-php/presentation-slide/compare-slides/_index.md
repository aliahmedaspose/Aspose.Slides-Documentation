---
title: Compare Slides
type: docs
weight: 50
url: /java/compare-slides/
---

## **Compare Two Slides**
Equals method has been added to [IBaseSlide](https://apireference.aspose.com/slides/java/com.aspose.slides/IBaseSlide) interface and [BaseSlide](https://apireference.aspose.com/slides/java/com.aspose.slides/BaseSlide) class. It returns true for the slides/layout and slides/master slides which identical by its structure and static content. 

Two slides are equal if all shapes, styles, texts, animation and other settings. etc. are equal. The comparison doesn't take into account unique identifier values, e.g. SlideId and dynamic content, e.g. current date value in Date Placeholder.

```php
Presentation presentation1 = new Java("com.aspose.slides.Presentation", "AccessSlides.pptx");
try {
    $presentation2 = new Java("com.aspose.slides.Presentation", "HelloWorld.pptx");
    try {
        for ($i = 0; $i < presentation1->getMasters()->size(); $i++)
        {
            for ($j = 0; $j < presentation2->getMasters()->size(); $j++)
            {
                if ($presentation1->getMasters()->get_Item($i) == ($presentation2->getMasters()->get_Item($j)))
                    echo(sprintf("SomePresentation1 MasterSlide#%d is equal to SomePresentation2 MasterSlide#%d", $i, $j));
            }
        }
    } finally {
        presentation2->dispose();
    }
} finally {
    presentation1->dispose();
}
```
