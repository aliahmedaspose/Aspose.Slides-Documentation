---
title: Connector
type: docs
weight: 10
url: /java/connector/
---

## **Connect Shapes Using Connectors**
In order to add a connector shape for joining two shapes. Please follow the steps below:

1. Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain the reference of a slide by using its Index.
1. Add two add AutoShape's in selected slide using [addAutoShape](https://apireference.aspose.com/slides/java/com.aspose.slides/IShapeCollection#addAutoShape-int-float-float-float-float-) method exposed by [IShapeCollection](https://apireference.aspose.com/slides/java/com.aspose.slides/IShapeCollection) object.
1. Add Connector using [addConnector](https://apireference.aspose.com/slides/java/com.aspose.slides/IShapeCollection#addConnector-int-float-float-float-float-) method exposed by [IShapeCollection](https://apireference.aspose.com/slides/java/com.aspose.slides/IShapeCollection) object by defining Connector Type.
1. Join the added shape using connectors.
1. Call Reroute() method to create shortest automatic connection path.
1. Write the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) as a PPTX file.
   In the example given below, we have added a connector between two shapes.

```php
// Instantiate Presentation class that represents the PPTX file
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Accessing shapes collection for selected slide
    $shapes = $pres->getSlides()->get_Item(0)->getShapes();
    
    // Add Autoshape Ellipse
    $ellipse = $shapes->addAutoShape(Java("com.aspose.slides.ShapeType")->Ellipse, 0, 100, 100, 100);
    
    // Add Autoshape Rectangle
    $rectangle = $shapes->addAutoShape(Java("com.aspose.slides.ShapeType")->Rectangle, 100, 300, 100, 100);
    
    // Adding connector shape to slide shape collection
    $connector = $shapes->addConnector(Java("com.aspose.slides.ShapeType")->BentConnector2, 0, 0, 10, 10);
    
    // Joining Shapes to connectors
    $connector->setStartShapeConnectedTo($ellipse);
    $connector->setEndShapeConnectedTo($rectangle);
    
    // Call reroute to set the automatic shortest path between shapes
    $connector->reroute();
    
    // Saving Presentation
    $pres->save("output.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

{{% alert color="primary" %}} 

Method [IConnector.reroute()](https://apireference.aspose.com/slides/java/com.aspose.slides/IConnector#reroute--) reroutes connector so that it take the shortest possible path between the shapes it connect. To do this, the [reroute()](https://apireference.aspose.com/slides/java/com.aspose.slides/IConnector#reroute--) method may change the [StartShapeConnectionSiteIndex](https://apireference.aspose.com/slides/java/com.aspose.slides/IConnector#setStartShapeConnectionSiteIndex-long-) and [EndShapeConnectionSiteIndex](https://apireference.aspose.com/slides/java/com.aspose.slides/IConnector#setEndShapeConnectionSiteIndex-long-).

{{% /alert %}} 

## **Use Desired Connection Site**
In order to add a connector shape for joining two shapes. Please follow the steps below:

1. Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain the reference of a slide by using its Index.
1. Add two add AutoShape's in selected slide using [addAutoShape](https://apireference.aspose.com/slides/java/com.aspose.slides/IShapeCollection#addAutoShape-int-float-float-float-float-) method exposed by [IShapeCollection](https://apireference.aspose.com/slides/java/com.aspose.slides/IShapeCollection) object.
1. Add Connector using [addConnector](https://apireference.aspose.com/slides/java/com.aspose.slides/IShapeCollection#addConnector-int-float-float-float-float-) method exposed by [IShapeCollection](https://apireference.aspose.com/slides/java/com.aspose.slides/IShapeCollection) object by defining Connector Type.
1. Join the added shape using connectors.
1. Setting the desired connection site on shape for connector.
1. Write the presentation as a PPTX file.

In the example given below, we have added a connector between two shapes.

```php
// Instantiate Presentation class that represents the PPTX file
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Accessing shapes collection for selected slide
    $shapes = $pres->getSlides()->get_Item(0)->getShapes();

    // Add Autoshape Ellipse
    $ellipse = $shapes->addAutoShape(Java("com.aspose.slides.ShapeType")->Ellipse, 0, 100, 100, 100);

    // Add Autoshape Rectangle
    $rectangle = $shapes->addAutoShape(Java("com.aspose.slides.ShapeType")->Rectangle, 100, 300, 100, 100);

    // Adding connector shape to slide shape collection
    $connector = $shapes->addConnector(Java("com.aspose.slides.ShapeType")->BentConnector2, 0, 0, 10, 10);

    // Joining Shapes to connectors
    $connector->setStartShapeConnectedTo($ellipse);
    $connector->setEndShapeConnectedTo($rectangle);

    // Setting the desired connection site index of Ellipse shape for
    // connector to get connected
    $wantedIndex = 6;

    // Checking if desired index is less than maximum site index count
    if ($ellipse->getConnectionSiteCount() > $wantedIndex) 
    {
        // Setting the desired connection site for connector on Ellipse
        $connector->setStartShapeConnectionSiteIndex($wantedIndex);
    }

    // Saving presentation
    $pres->save("output.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Find Angle of Connector Lines**
In order to calculate the angle for connector line, please follow the steps below:

1. Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class and load the presentation.
1. Obtain the reference of a slide by using its Index.
1. Access the Connector Line shape.
1. Use the line width, height, shape frame height and shape frame width to calculate the angle.

In the example given below, we have calculated the angle for connector line shape in slide.

```php
// Instantiate Presentation class that represents the PPTX file
$pres = new Java("com.aspose.slides.Presentation", "ConnectorLineAngle.pptx");
try {
    $slide = $pres->getSlides()->get_Item(0);
    
    for ($i = 0; $i < $slide->getShapes()->size(); $i++)
    {
        dir = 0.0;
        $shape = $slide->getShapes()->get_Item($i);
        if ($shape instanceof AutoShape)
        {
            $ashp = $shape;
            if ($ashp->getShapeType() == Java("com.aspose.slides.ShapeType")->Line)
            {
                dir = getDirection($ashp->getWidth(), $ashp->getHeight(),
                        $ashp->getFrame()->getFlipH() > 0, $ashp->getFrame()->getFlipV() > 0);
            }
        }
        else if ($shape instanceof Connector)
        {
            $ashp = $shape;
            $dir = getDirection($ashp->getWidth(), $ashp->getHeight(),
                    $ashp->getFrame()->getFlipH() > 0, $ashp->getFrame()->getFlipV() > 0);
        }

        echo($dir);
    }
} finally {
    if ($pres != null) $pres->dispose();
}
```
```php
public static double getDirection($w, $h, $flipH, $flipV)
{
    $endLineX = $w * ($flipH ? -1 : 1);
    $endLineY = $h * ($flipV ? -1 : 1);
    $endYAxisX = 0;
    $endYAxisY = $h;
    $angle = atan2($endYAxisY, $endYAxisX) - atan2($endLineY, $endLineX);
    if ($angle < 0) $angle += 2 * M_PI;
    return $angle * 180.0 / M_PI;
}
```
