---
title: Shape Animation
type: docs
weight: 50
url: /java/shape-animation/
---

Animation is one of the most important parts of the presentations that make them more attractive and meaningful. Aspose.Slides for Java also allows developers to apply different kinds of animation effects on different kinds of shapes. In this topic, we will show how to apply animation effects on shapes.

Here we will apply the PathFootball effect (one of more than 150 available effects) on a TextBox that will be activated on clicking the bevel shape (some sort of button). To apply such animation effect, please follow the steps below:

- Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
- Obtain the reference of a slide by using its Index.
- Add an [IAutoShape](https://apireference.aspose.com/slides/java/com.aspose.slides/IAutoShape) of Rectangle type.
- Add an [IAutoShape](https://apireference.aspose.com/slides/java/com.aspose.slides/IAutoShape) of [Bevel](https://apireference.aspose.com/slides/java/com.aspose.slides/ShapeType#Bevel) type (which when clicked causes the animations to take effect).
- Create a sequence of effects on this [Bevel](https://apireference.aspose.com/slides/java/com.aspose.slides/ShapeType#Bevel) shape.
- Create a custom User Path.
- Add commands to the Path for moving.
- Write the presentation to the disk as a PPTX file.

This sample code, based on the steps above, shows you how to apply the PathFootball effect to a TextBox activated when the bevel shape gets clicked:

```php
// Instantiate PrseetationEx class that represents the PPTX
$pres = new Java("com.aspose.slides.Presentation");
try {
    $sld = $pres->getSlides()->get_Item(0);

    // Now create effect "PathFootball" for existing shape from scratch.
    $ashp = $sld->getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Rectangle, 150, 150, 250, 25);
    $ashp->addTextFrame("Animated TextBox");

    // Add PathFootBall animation effect
    $pres->getSlides()->get_Item(0)->getTimeline()->getMainSequence()->addEffect($ashp, Java("com.aspose.slides.EffectType")->PathFootball,
            Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);

    // Create some kind of "button".
    $shapeTrigger = $pres->getSlides()->get_Item(0)->getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Bevel, 10, 10, 20, 20);

    // Create sequence of effects for this button.
    $seqInter = $pres->getSlides()->get_Item(0)->getTimeline()->getInteractiveSequences()->add($shapeTrigger);

    // Create custom user path. Our object will be moved only after "button" click.
    $fxUserPath = seqInter->addEffect($ashp, Java("com.aspose.slides.EffectType")->PathUser, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->OnClick);

    // Created path is empty so we should add commands for moving.
    $motionBhv = ($fxUserPath->getBehaviors()->get_Item(0));

    Java("java.awt.geom.Point2D")->Float[] $pts = new Java("java.awt.geom.Point2D")->Float[1];
    $pts[0] = Java("java.awt.geom.Point2D")->Float(0.076, 0.59);
    $motionBhv->getPath()->add(Java("com.aspose.slides.MotionCommandPathType")->LineTo, $pts, Java("com.aspose.slides.MotionPathPointsType")->Auto, true);
    $pts[0] = Java("java.awt.geom.Point2D")->Float(-0.076, -0.59);
    $motionBhv->getPath()->add(Java("com.aspose.slides.MotionCommandPathType")->LineTo, $pts, Java("com.aspose.slides.MotionPathPointsType")->Auto, false);
    $motionBhv->getPath()->add(Java("com.aspose.slides.MotionCommandPathType")->End, null, Java("com.aspose.slides.MotionPathPointsType")->Auto, false);

    //Write the presentation as PPTX to disk
    $pres->save("AnimExample_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```