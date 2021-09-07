---
title: Custom Shape
type: docs
weight: 10
url: /java/custom-shape/
---

# Shape Geometry Customization (Shape Points Editing)

## Overview

Customization of the shape geometry assumes editing points of an existing shape. 

![overview_image](custom_shape_0.png)

To provide the mentioned functionality [GeometryPath](https://apireference.aspose.com/slides/java/com.aspose.slides/GeometryPath) class and [IGeometryPath](https://apireference.aspose.com/slides/java/com.aspose.slides/IGeometryPath) interface have been added. [GeometryPath](https://apireference.aspose.com/slides/java/com.aspose.slides/GeometryPath) instance represents a geometry path of the [IGeometryShape](https://apireference.aspose.com/slides/java/com.aspose.slides/IGeometryShape) object. 

To retrieve [GeometryPath](https://apireference.aspose.com/slides/java/com.aspose.slides/GeometryPath) from the [IGeometryShape](https://apireference.aspose.com/slides/java/com.aspose.slides/IGeometryShape) instance [IGeometryShape->getGeometryPaths](https://apireference.aspose.com/slides/java/com.aspose.slides/IGeometryShape#getGeometryPaths--) method has been added. Shapes may be built from a few smaller shapes (e.g. an "equal" sign) so this method returns an array of [GeometryPath](https://apireference.aspose.com/slides/java/com.aspose.slides/GeometryPath) objects. 

To set [GeometryPath](https://apireference.aspose.com/slides/java/com.aspose.slides/GeometryPath) to the shape two methods have been added: 
[IGeometryShape->setGeometryPath](https://apireference.aspose.com/slides/java/com.aspose.slides/IGeometryShape#setGeometryPath-com.aspose.slides.IGeometryPath-) for solid shapes and [IGeometryShape->setGeometryPaths](https://apireference.aspose.com/slides/java/com.aspose.slides/IGeometryShape#setGeometryPaths-com.aspose.slides.IGeometryPath:A-) for composite shapes.

[IGeometryPath](https://apireference.aspose.com/slides/java/com.aspose.slides/IGeometryPath) provides methods for adding segments of various types:

**Adds line** to the end of the path
```php
public void lineTo($point);
public void lineTo($x, $y);
```
**Adds line** to the specified place of the path:
```php    
public void lineTo($point, $index);
public void lineTo($x, $y, $index);
```
**Adds cubic Bezier curve** at the end the path:
```php
public void cubicBezierTo($point1, $point2, $point3);
public void cubicBezierTo($x1, $y1, $x2, $y2, $x3, $y3);
```
**Adds cubic Bezier curve** to the specified place of the path:
```php
public void cubicBezierTo($point1, $point2, $point3, $index);
public void cubicBezierTo($x1, $y1, $x2, $y2, $x3, $y3, $index);
```
**Adds quadratic Bezier curve** at the end the path:
```php
public void quadraticBezierTo($point1, $point2);
public void quadraticBezierTo($x1, $y1, $x2, $y2);
```
**Adds quadratic Bezier curve** to the specified place of the path:
```php
public void quadraticBezierTo($point1, $point2, $index);
public void quadraticBezierTo($x1, $y1, $x2, $y2, $index);
```
**Appends the specified arc** to the path:
```php
public void arcTo($width, $heigth, $startAngle, $sweepAngle);
```
**Closes the current figure** of this path:
```php
public void closeFigure();
```
**Sets next point position**:
```php
public void moveTo($point);
public void moveTo($x, $y);
```
**Removes path segment** at the specified index:
```php
public void removeAt($index);
```
Methods [IGeometryPath->getStroke](https://apireference.aspose.com/slides/java/com.aspose.slides/IGeometryPath#getStroke--), [IGeometryPath->getStroke](https://apireference.aspose.com/slides/java/com.aspose.slides/IGeometryPath#setStroke-boolean-), [IGeometryPath->getFillMode](https://apireference.aspose.com/slides/java/com.aspose.slides/IGeometryPath#getFillMode--) and [IGeometryPath->setFillMode](https://apireference.aspose.com/slides/java/com.aspose.slides/IGeometryPath#setFillMode-byte-) set an appearance of the geometry path.

Method [IGeometryPath->getPathData](https://apireference.aspose.com/slides/java/com.aspose.slides/IGeometryPath#getPathData--) returns the geometry path of [GeometryShape](https://apireference.aspose.com/slides/java/com.aspose.slides/GeometryShape) as an array of path segments.


*To provide more options of shape geometry customization [ShapeUtil](https://apireference.aspose.com/slides/java/com.aspose.slides/ShapeUtil) class has been added. Methods of this class allow to convert [GeometryPath](https://apireference.aspose.com/slides/java/com.aspose.slides/GeometryPath) to [GraphicsPath](https://docs.microsoft.com/en-us/dotnet/api/system.drawing.drawing2d?view=dotnet-plat-ext-5.0) back and forth.*

# Examples and Use Cases

## Add Custom Points to Shape

- Create an instance of the [GeometryShape](https://apireference.aspose.com/slides/java/com.aspose.slides/GeometryShape) class of type [Java("com.aspose.slides.ShapeType")->Rectangle](https://apireference.aspose.com/slides/java/com.aspose.slides/ShapeType#Rectangle)
- Retrieve an instance of the [GeometryPath](https://apireference.aspose.com/slides/java/com.aspose.slides/GeometryPath) class from the shape.
- Add a new point between two top points of the path.
- Add a new point between two bottom points of the path.
- Apply the path to the shape.
  
```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $shape = $pres->getSlides()->get_Item(0)->
            getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Rectangle, 100, 100, 200, 100);
    $geometryPath = $shape->getGeometryPaths()[0];

    $geometryPath->lineTo(100, 50, 1);
    $geometryPath->lineTo(100, 50, 4);
    $shape->setGeometryPath($geometryPath);
} finally {
    if ($pres != null) $pres->dispose();
}
```

![example1_image](custom_shape_1.png)

##  Remove Points from Shape

- Create an instance of [GeometryShape](https://apireference.aspose.com/slides/java/com.aspose.slides/GeometryShape) class of type [Java("com.aspose.slides.ShapeType")->Heart](https://apireference.aspose.com/slides/java/com.aspose.slides/ShapeType#Heart).
- Retrieve an instance of the [GeometryPath](https://apireference.aspose.com/slides/java/com.aspose.slides/GeometryPath) class from the shape.
- Remove segment of the path.
- Apply the path to the shape.
  
```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $shape = $pres->getSlides()->get_Item(0)->
            getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Heart, 100, 100, 300, 300);

    $path = $shape->getGeometryPaths()[0];
    $path->removeAt(2);
    $shape->setGeometryPath($path);
} finally {
    if ($pres != null) $pres->dispose();
}
```
![example2_image](custom_shape_2.png)

##  Create Custom Shape

- Calculate points of the shape.
- Create an instance of the [GeometryPath](https://apireference.aspose.com/slides/java/com.aspose.slides/GeometryPath) class. 
- Fill the path with the points.
- Create an instance of the [GeometryShape](https://apireference.aspose.com/slides/java/com.aspose.slides/GeometryShape) class. 
- Apply the path to the shape.

```php
List<Java("java.awt.geom.Point2D")->Float> points = new ArrayList<Java("java.awt.geom.Point2D")->Float>();

$R = 100;
$r = 50;
$step = 72;

for ($angle = -90; $angle < 270; $angle += $step)
{
    $radians = $angle * (M_PI / 180);
    $x = R * cos($radians);
    $y = R * sin($radians);
    $points->add(Java("java.awt.geom.Point2D")->Float($x + $R, $y + $R));

    $radians = M_PI * (angle + step / 2) / 180.0;
    $x = r * cos($radians);
    $y = r * sin($radians);
    points->add(Java("java.awt.geom.Point2D")->Float($x + $R, $y + $R));
}

$starPath = new Java("com.aspose.slides.GeometryPath");
$starPath->moveTo($points->get(0));

for ($i = 1; $i < $points->size(); $i++)
{
    $starPath->lineTo($points->get($i));
}

$starPath->closeFigure();

$pres = new Java("com.aspose.slides.Presentation");
try {
    $shape = $pres->getSlides()->get_Item(0)->
            getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Rectangle, 100, 100, $R * 2, $R * 2);

    $shape->setGeometryPath($starPath);
} finally {
    if ($pres != null) $pres->dispose();
}

```
![example3_image](custom_shape_3.png)


## Create Composite Custom Shape

  - Create an instance of the [GeometryShape](https://apireference.aspose.com/slides/java/com.aspose.slides/GeometryShape) class.
  - Create first instance of the [GeometryPath](https://apireference.aspose.com/slides/java/com.aspose.slides/GeometryPath) class.
  - Create second instance of the [GeometryPath](https://apireference.aspose.com/slides/java/com.aspose.slides/GeometryPath) class.
  - Apply the paths to the shape.

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $shape = $pres->getSlides()->get_Item(0)->
            getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Rectangle, 100, 100, 200, 100);

    $geometryPath0 = new Java("com.aspose.slides.GeometryPath");
    $geometryPath0->moveTo(0, 0);
    $geometryPath0->lineTo($shape->getWidth(), 0);
    $geometryPath0->lineTo($shape->getWidth(), $shape->getHeight()/3);
    $geometryPath0->lineTo(0, $shape->getHeight() / 3);
    $geometryPath0->closeFigure();

    $geometryPath1 = new Java("com.aspose.slides.GeometryPath");
    $geometryPath1->moveTo(0, $shape->getHeight()/3 * 2);
    $geometryPath1->lineTo($shape->getWidth(), $shape->getHeight() / 3 * 2);
    $geometryPath1->lineTo($shape->getWidth(), $shape->getHeight());
    $geometryPath1->lineTo(0, $shape->getHeight());
    $geometryPath1->closeFigure();

    $Array = new JavaClass("java.lang.reflect.Array");
    $GeometryPath = new JavaClass("com.aspose.slides.GeometryPath");
    $geometryPathArray = $Array->newInstance($GeometryPath, 2);
    $geometryPathArray[0] = $geometryPath0;
    $geometryPathArray[1] = $geometryPath1;

    $shape->setGeometryPaths($geometryPathArray);
} finally {
    if ($pres != null) $pres->dispose();
}
```
![example4_image](custom_shape_4.png)

## Conversion of java.awt.Shape to GeometryPath

- Create an instance of the [GeometryShape](https://apireference.aspose.com/slides/java/com.aspose.slides/GeometryShape) class.
- Create an instance of the [java.awt.Shape](https://docs.oracle.com/javase/7/docs/api/java/awt/Shape.html) class.
- Convert the [Shape](https://docs.oracle.com/javase/7/docs/api/java/awt/Shape.html) instance to the  [GeometryPath](https://apireference.aspose.com/slides/java/com.aspose.slides/GeometryPath) instance using [ShapeUtil](https://apireference.aspose.com/slides/java/com.aspose.slides/ShapeUtil).
- Apply the paths to the shape.
  
```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Create new shape
    $shape = $pres->getSlides()->get_Item(0)->
            getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Rectangle, 100, 100, 300, 100);

    // Get geometry path of the shape
    $originalPath = $shape->getGeometryPaths()[0];
    $originalPath->setFillMode(Java("com.aspose.slides.PathFillModeType")->None);

    // Create new graphics path with text
    $graphicsPath;
    $font = Java("java.awt.Font", "Arial", Font.PLAIN, 40);
    $text = "Text in shape";
    $img = new Java("java.awt.image.BufferedImage", 100, 100, Java("java.awt.image.BufferedImage")->TYPE_INT_ARGB);
    $g2 = $img->createGraphics();

    try
    {
        $glyphVector = $font->createGlyphVector($g2->getFontRenderContext(), $text);
        $graphicsPath = $glyphVector->getOutline(20, (-$glyphVector->getVisualBounds()->getY()) + 10);
    }
    finally {
        $g2->dispose();
    }

    // Convert graphics path to geometry path
    $textPath = ShapeUtil->graphicsPathToGeometryPath(PathFillModeTypegraphicsPath);
    $textPath->setFillMode(Java("com.aspose.slides.PathFillModeType")->Normal);

    // Set combination of new geometry path and origin geometry path to the shape
    $Array = new JavaClass("java.lang.reflect.Array");
    $IGeometryPath = new JavaClass("com.aspose.slides.IGeometryPath");
    $igeometryPathArray = $Array->newInstance($IGeometryPath, 2);
    $igeometryPathArray[0] = $originalPath;
    $igeometryPathArray[1] = $textPath;
        
    $shape->setGeometryPaths($igeometryPathArray);

    // Save the presentation
    $pres->save(resultPath, Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```
![example5_image](custom_shape_5.png)
