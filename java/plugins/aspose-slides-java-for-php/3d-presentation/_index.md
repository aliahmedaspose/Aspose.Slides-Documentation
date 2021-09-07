---
title: 3D Presentation
type: docs
weight: 232
url: /java/3d-presentation/
---

## Overview
Since Aspose.Slides Java 20.9 its possible to create 3D in presentations. PowerPoint 3D is a way to give life to presentations. Show the real world objects 
with 3D presentation, demonstrate 3D model of your future business project, 3D model of the building or its interior, 3D model of the game character, 
or just a 3D representation of your data. 

PowerPoint 3D models can be created from 2D shapes, by applying such effects on them: 3D rotation, 3D depth and extrusion, 3D gradient, 3D text, etc. 
The list of 3D features applied to the shapes can be found in **[ThreeDFormat](https://apireference.aspose.com/slides/java/com.aspose.slides/ThreeDFormat)** class. 
The instance of the class can be get by:
 
- **[Shape->getThreeDFormat()](https://apireference.aspose.com/slides/java/com.aspose.slides/Shape#getThreeDFormat--)** method for creating a PowerPoint 3D Model.
- **[TextFrameFormat->getThreeDFormat()](https://apireference.aspose.com/slides/java/com.aspose.slides/TextFrameFormat#getThreeDFormat--)** method for creating a 3D Text 
(WordArt).

All effects implemented in **[ThreeDFormat](https://apireference.aspose.com/slides/java/com.aspose.slides/ThreeDFormat)** can be used for both shapes and text. 
Let us have a quick look on the main methods of **[ThreeDFormat](https://apireference.aspose.com/slides/java/com.aspose.slides/ThreeDFormat)** class. In the next example 
we create a rectangle 2D shape with a text on it. By getting camera view on the shape, we change its rotation and make looking as a 3D model. Setting a flat light 
and its direction to the top of the 3D model, bring more volume to the model. Changed materials, extrusion height and color make the 3D model look more alive.  
```php
<?php require_once("http://localhost:8087/JavaBridge/java/Java.inc");
$pres = new Java("com.aspose.slides.Presentation");
try {
    $shape = $pres->getSlides()->get_Item(0)->getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Rectangle, 200, 150, 200, 200);
    $shape->getTextFrame()->setText("3D");
    $shape->getTextFrame()->getParagraphs()->get_Item(0)->getJava("com.aspose.slides.ParagraphFormat")->getDefaultPortionFormat()->setFontHeight(64);
 
    $shape->getThreeDFormat()->getCamera()->setCameraType(Java("com.aspose.slides.CameraPresetType")->OrthographicFront);
    $shape->getThreeDFormat()->getCamera()->setRotation(20, 30, 40);
    $shape->getThreeDFormat()->getLightRig()->setLightType(Java("com.aspose.slides.LightRigPresetType")->Flat);
    $shape->getThreeDFormat()->getLightRig()->setDirection(Java("com.aspose.slides.LightingDirection")->Top);
    $shape->getThreeDFormat()->setMaterial(Java("com.aspose.slides.MaterialPresetType")->Flat);
    $shape->getThreeDFormat()->setExtrusionHeight(100);
    $shape->getThreeDFormat()->getExtrusionColor()->setColor(Java("java.awt.Color")->BLUE);
 
    try {
        Java("javax.imageio.ImageIO")->write($pres->getSlides()->get_Item(0)->getThumbnail(2, 2), "PNG", new Java("java.io.File", "sample_3d.png"));
    } catch (JavaException $e) {}
 
    $pres->save("sandbox_3d.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
?>
```

Here is the resulting 3D model:

![todo:image_alt_text](img_01_01.png)

## 3D Rotation
The rotation of 3D model in PowerPoint can be done via menu:

![todo:image_alt_text](img_02_01.png)

To rotate 3D model with Aspose.Slides API, use **[IThreeDFormat->getCamera()](https://apireference.aspose.com/slides/java/com.aspose.slides/ThreeDFormat#getCamera--)** 
method, set the rotation of the camera relatively to 3D shape:

```php
$shape = $pres->getSlides()->get_Item(0)->getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Rectangle, 200, 150, 200, 200);
$shape->getThreeDFormat()->getCamera()->setRotation(20, 30, 40);
// ... set other 3D scene parameters
try {
    Java("javax.imageio.ImageIO")->write($pres->getSlides()->get_Item(0)->getThumbnail(2, 2), "PNG", new Java("java.io.File", "sample_3d.png"));
} catch (JavaException $e) { }
```

## 3D Depth and Extrusion
**[IThreeDFormat->getExtrusionHeight()](https://apireference.aspose.com/slides/java/com.aspose.slides/ThreeDFormat#getExtrusionHeight--)** 
and **[IThreeDFormat->getExtrusionColor()](https://apireference.aspose.com/slides/java/com.aspose.slides/ThreeDFormat#getExtrusionColor--)** methods 
are used to create extrusion on shape:

```php
$shape = $pres->getSlides()->get_Item(0)->getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Rectangle, 200, 150, 200, 200);
$shape->getThreeDFormat()->getCamera()->setRotation(20, 30, 40);
$shape->getThreeDFormat()->setExtrusionHeight(100);
$shape->getThreeDFormat()->getExtrusionColor()->setColor(new Java("java.awt.Color", 128, 0, 128));
// ... set other 3D scene parameters
try {
    Java("javax.imageio.ImageIO")->write($pres->getSlides()->get_Item(0)->getThumbnail(2, 2), "PNG", new Java("java.io.File", "sample_3d.png"));
} catch (JavaException $e) { }
```

In PowerPoint, Depth of the shape is set via:

![todo:image_alt_text](img_02_02.png)

## 3D Gradient
3D gradient can bring more volume to PowerPoint 3D shape:

```php
<?php require_once("http://localhost:8087/JavaBridge/java/Java.inc");
$pres = new Java("com.aspose.slides.Presentation");
try {
    $shape = $pres->getSlides()->get_Item(0)->getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Rectangle, 200, 150, 250, 250);
    $shape->getTextFrame()->setText("3D");
    $shape->getTextFrame()->getParagraphs()->get_Item(0)->getJava("com.aspose.slides.ParagraphFormat")->getDefaultPortionFormat()->setFontHeight(64);
 
    $shape->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Gradient);
    $shape->getFillFormat()->getGradientFormat()->getGradientStops()->add(0, Java("java.awt.Color")->BLUE);
    $shape->getFillFormat()->getGradientFormat()->getGradientStops()->add(100, Java("java.awt.Color")->ORANGE);
 
    $shape->getThreeDFormat()->getCamera()->setCameraType(Java("com.aspose.slides.CameraPresetType")->OrthographicFront);
    $shape->getThreeDFormat()->getCamera()->setRotation(10, 20, 30);
    $shape->getThreeDFormat()->getLightRig()->setLightType(Java("com.aspose.slides.LightRigPresetType")->Flat);
    $shape->getThreeDFormat()->getLightRig()->setDirection(Java("com.aspose.slides.LightingDirection")->Top);
    $shape->getThreeDFormat()->setExtrusionHeight(150);
    $shape->getThreeDFormat()->getExtrusionColor()->setColor(new Java("java.awt.Color", 255, 140, 0));
 
    try {
        Java("javax.imageio.ImageIO")->write($pres->getSlides()->get_Item(0)->getThumbnail(2, 2), "PNG", new Java("java.io.File", "sample_3d.png"));
    } catch (JavaException $e) { }
} finally {
    if ($pres != null) $pres->dispose();
}
?>
```

Thats how it looks like:

![todo:image_alt_text](img_02_03.png)
  
You may also create an image gradient:
```php
$shape->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Picture);
$picture = null;
try {
	$fis = new Java("java.io.FileInputStream", new Java("java.io.File", "sample_3d.png"));
	$picture = $pres->getImages()->addImage($fis);
} catch (JavaException $e) { }
finally {
    if ($fis != null) $fis->close();
}
$shape->getFillFormat()->getPictureFillFormat()->getPicture()->setImage($picture);
$shape->getFillFormat()->getPictureFillFormat()->setPictureFillMode(Java("com.aspose.slides.PictureFillMode")->Stretch);
// .. setup 3D: $shape->ThreeDFormat->Camera, $shape->ThreeDFormat->LightRig, $shape->ThreeDFormat->Extrusion* properties
try {
    Java("javax.imageio.ImageIO")->write($pres->getSlides()->get_Item(0)->getThumbnail(2, 2), "PNG", new Java("java.io.File", "sample_3d.png"));
} catch (JavaException $e) { }
```


Here is the result:

![todo:image_alt_text](img_02_04.png)

## 3D Text (WordArt)
To create a 3D text (WordArt), do the following:
```php
<?php require_once("http://localhost:8087/JavaBridge/java/Java.inc");
$pres = new Java("com.aspose.slides.Presentation");
try {
    $shape = $pres->getSlides()->get_Item(0)->getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Rectangle, 200, 150, 200, 200);
 
    $shape->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->NoFill);
    $shape->getLineFormat()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->NoFill);
    $shape->getTextFrame()->setText("3D Text");
 
    $portion = $shape->getTextFrame()->getParagraphs()->get_Item(0)->getPortions()->get_Item(0);
    $portion->getPortionFormat()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Pattern);
    $portion->getPortionFormat()->getFillFormat()->getPatternFormat()->getForeColor()->setColor(new Java("java.awt.Color",  255, 140, 0));
    $portion->getPortionFormat()->getFillFormat()->getPatternFormat()->getBackColor()->setColor(Java("java.awt.Color")->WHITE);
    $portion->getPortionFormat()->getFillFormat()->getPatternFormat()->setPatternStyle(Java("com.aspose.slides.PatternStyle")->LargeGrid);
 
    $shape->getTextFrame()->getParagraphs()->get_Item(0)->getJava("com.aspose.slides.ParagraphFormat")->getDefaultPortionFormat()->setFontHeight(128);
 
    $textFrame = $shape->getTextFrame();
    // setup "Arch Up" WordArt transform effect
    $textFrame->getJava("com.aspose.slides.TextFrameFormat")->setTransform(Java("com.aspose.slides.TextShapeType")->ArchUp);
 
    $textFrame->getJava("com.aspose.slides.TextFrameFormat")->getThreeDFormat()->setExtrusionHeight(3.5);
    $textFrame->getJava("com.aspose.slides.TextFrameFormat")->getThreeDFormat()->setDepth(3);
    $textFrame->getJava("com.aspose.slides.TextFrameFormat")->getThreeDFormat()->setMaterial(Java("com.aspose.slides.MaterialPresetType")->Plastic);
    $textFrame->getJava("com.aspose.slides.TextFrameFormat")->getThreeDFormat()->getLightRig()->setDirection(Java("com.aspose.slides.LightingDirection")->Top);
    $textFrame->getJava("com.aspose.slides.TextFrameFormat")->getThreeDFormat()->getLightRig()->setLightType(Java("com.aspose.slides.LightRigPresetType")->Balanced);
    $textFrame->getJava("com.aspose.slides.TextFrameFormat")->getThreeDFormat()->getLightRig()->setRotation(0, 0, 40);
 
    $textFrame->getJava("com.aspose.slides.TextFrameFormat")->getThreeDFormat()->getCamera()->setCameraType(Java("com.aspose.slides.CameraPresetType")->PerspectiveContrastingRightFacing);
 
    try {
        Java("javax.imageio.ImageIO")->write($pres->getSlides()->get_Item(0)->getThumbnail(2, 2), "PNG", new Java("java.io.File", "text3d.png"));
    } catch (JavaException $e) { }
 
    $pres->save("text3d.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
	
} finally {
    if ($pres != null) $pres->dispose();
}
?>
```

Here is the result:

![todo:image_alt_text](img_02_05.png)

 
 
## Not Supported - Coming Soon
The following PowerPoint 3D features are not supported yet: 
- Bevel
- Material
- Contour
- Lighting


 

