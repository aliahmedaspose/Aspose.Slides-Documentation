---
title: Trend Line
type: docs
url: /java/trend-line/
---

## **Add Trend Line**
Aspose.Slides for Java provides a simple API for managing different chart Trend Lines:

1. Create an instance of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain a slide's reference by its index.
1. Add a chart with default data along with the any of desired type (this example uses Java("com.aspose.slides.ChartType")->ClusteredColumn).
1. Adding exponential trend line for chart series 1.
1. Adding linear trend line for chart series 1.
1. Adding logarithmic trend line for chart series 2.
1. Adding moving average trend line for chart series 2.
1. Adding polynomial trend line for chart series 3.
1. Adding power trend line for chart series 3.
1. Write the modified presentation to a PPTX file.

The following code is used to create a chart with Trend Lines.

```php
// Create an instance of Presentation class
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Creating a clustered column chart
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->ClusteredColumn, 20, 20, 500, 400);
    
    // Adding ponential trend line for chart series 1
    $tredLinep = $chart->getChartData()->getSeries()->get_Item(0)->getTrendLines()->add(Java("com.aspose.slides.TrendlineType")->Exponential);
    $tredLinep->setDisplayEquation(false);
    $tredLinep->setDisplayRSquaredValue(false);
    
    // Adding Linear trend line for chart series 1
    $tredLineLin = $chart->getChartData()->getSeries()->get_Item(0)->getTrendLines()->add(Java("com.aspose.slides.TrendlineType")->Linear);
    $tredLineLin->setTrendlineType(Java("com.aspose.slides.TrendlineType")->Linear);
    $tredLineLin->getFormat()->getLine()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
    $tredLineLin->getFormat()->getLine()->getFillFormat()->getSolidFillColor()->setColor(Java("java.awt.Color")->RED);
    
    
    // Adding Logarithmic trend line for chart series 2
    $tredLineLog = $chart->getChartData()->getSeries()->get_Item(1)->getTrendLines()->add(Java("com.aspose.slides.TrendlineType")->Logarithmic);
    $tredLineLog->setTrendlineType(Java("com.aspose.slides.TrendlineType")->Logarithmic);
    tredLineLog->addTextFrameForOverriding("New log trend line");
    
    // Adding MovingAverage trend line for chart series 2
    $tredLineMovAvg = $chart->getChartData()->getSeries()->get_Item(1)->getTrendLines()->add(Java("com.aspose.slides.TrendlineType")->MovingAverage);
    $tredLineMovAvg->setTrendlineType(Java("com.aspose.slides.TrendlineType")->MovingAverage);
    $tredLineMovAvg->setPeriod((new Java("java.lang.Integer", 3))->byteValue());
    $tredLineMovAvg->setTrendlineName("New TrendLine Name");
    
    // Adding Polynomial trend line for chart series 3
    $tredLinePol = $chart->getChartData()->getSeries()->get_Item(2)->getTrendLines()->add(Java("com.aspose.slides.TrendlineType")->Polynomial);
    $tredLinePol->setTrendlineType(Java("com.aspose.slides.TrendlineType")->Polynomial);
    $tredLinePol->setForward(1);
    $tredLinePol->setOrder((new Java("java.lang.Integer", 3))->byteValue());
    
    // Adding Power trend line for chart series 3
    $tredLinePower = $chart->getChartData()->getSeries()->get_Item(1)->getTrendLines()->add(Java("com.aspose.slides.TrendlineType")->Power);
    $tredLinePower->setTrendlineType(Java("com.aspose.slides.TrendlineType")->Power);
    $tredLinePower->setBackward(1);
    
    // Saving presentation
    $pres->save("ChartTrendLines_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Add Custom Line**
Aspose.Slides for Java provides a simple API to add custom lines in a $chart-> To add a simple plain line to a selected slide of the presentation, please follow the steps below:

- Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class
- Obtain the reference of a slide by using its Index
- Create a new chart using AddChart method exposed by Shapes object
- Add an AutoShape of Line type using AddAutoShape method exposed by Shapes object
- Set the Color of the shape lines.
- Write the modified presentation as a PPTX file

The following code is used to create a chart with Custom Lines.

```php
// Create an instance of Presentation class
$pres = new Java("com.aspose.slides.Presentation");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->ClusteredColumn, 100, 100, 500, 400);
    $shape = $chart->getUserShapes()->getShapes()->addAutoShape(Java("com.aspose.slides.ShapeType")->Line, 0, $chart->getHeight()/2, $chart->getWidth(), 0);
    
    $shape->getLineFormat()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
    $shape->getLineFormat()->getFillFormat()->getSolidFillColor()->setColor($java.awt.Color.RED);
    
    $pres->save("Presentation.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```