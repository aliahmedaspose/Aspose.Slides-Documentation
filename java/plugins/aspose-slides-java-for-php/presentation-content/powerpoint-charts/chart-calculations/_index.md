---
title: Chart Calculations
type: docs
weight: 50
url: /java/chart-calculations/
---

## **Calculate Actual Values of Chart Elements**
Aspose.Slides for Java provides a simple API for getting these properties. Properties of [IAxis](https://apireference.aspose.com/slides/java/com.aspose.slides/IAxis) interface provide information about actual position of axis chart element ([IAxis->getActualMaxValue](https://apireference.aspose.com/slides/java/com.aspose.slides/IAxis#getActualMaxValue--), [IAxis->getActualMinValue](https://apireference.aspose.com/slides/java/com.aspose.slides/IAxis#getActualMinValue--), [IAxis->getActualMajorUnit](https://apireference.aspose.com/slides/java/com.aspose.slides/IAxis#getActualMajorUnit--), [IAxis->getActualMinorUnit](https://apireference.aspose.com/slides/java/com.aspose.slides/IAxis#getActualMinorUnit--), [IAxis->getActualMajorUnitScale](https://apireference.aspose.com/slides/java/com.aspose.slides/IAxis#getActualMajorUnitScale--), [IAxis->getActualMinorUnitScale](https://apireference.aspose.com/slides/java/com.aspose.slides/IAxis#getActualMinorUnitScale--)). It is necessary to call method [IChart.validateChartLayout()](https://apireference.aspose.com/slides/java/com.aspose.slides/IChart#validateChartLayout--) previously to fill properties with actual values.

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->Area, 100, 100, 500, 350);
    $chart->validateChartLayout();
    
    $maxValue = $chart->getAxes()->getVerticalAxis()->getActualMaxValue();
    $minValue = $chart->getAxes()->getVerticalAxis()->getActualMinValue();
    
    $majorUnit = $chart->getAxes()->getHorizontalAxis()->getActualMajorUnit();
    $minorUnit = $chart->getAxes()->getHorizontalAxis()->getActualMinorUnit();
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Calculate Actual Position of Parent Chart Elements**
Aspose.Slides for Java provides a simple API for getting these properties. Properties of [IActualLayout](https://apireference.aspose.com/slides/java/com.aspose.slides/IActualLayout) interface provide information about actual position of parent chart element ([IActualLayout->getActualX](https://apireference.aspose.com/slides/java/com.aspose.slides/IActualLayout#getActualX--), [IActualLayout->getActualY](https://apireference.aspose.com/slides/java/com.aspose.slides/IActualLayout#getActualY--), [IActualLayout->getActualWidth](https://apireference.aspose.com/slides/java/com.aspose.slides/IActualLayout#getActualWidth--), [IActualLayout->getActualHeight](https://apireference.aspose.com/slides/java/com.aspose.slides/IActualLayout#getActualHeight--)). It is necessary to call method [IChart.validateChartLayout()](https://apireference.aspose.com/slides/java/com.aspose.slides/IChart#validateChartLayout--) previously to fill properties with actual values.

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->ClusteredColumn, 100, 100, 500, 350);
    $chart->validateChartLayout();

    $x = $chart->getPlotArea()->getActualX();
    $y = $chart->getPlotArea()->getActualY();
    $w = $chart->getPlotArea()->getActualWidth();
    $h = $chart->getPlotArea()->getActualHeight();
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Hide Information from Chart**
This topic helps you to understand how to hide information from $chart-> Using Aspose.Slides for Java you can hide **Title, Vertical Axis, Horizontal Axis** and **Grid Lines** from $chart-> Below code example shows how to use these properties.

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $slide = $pres->getSlides()->get_Item(0);
    $chart = $slide->getShapes()->addChart(Java("com.aspose.slides.ChartType")->LineWithMarkers, 140, 118, 320, 370);

    //Hiding chart Title
    $chart->setTitle(false);

    ///Hiding Values axis
    $chart->getAxes()->getVerticalAxis()->setVisible(false);

    //Category Axis visibility
    $chart->getAxes()->getHorizontalAxis()->setVisible(false);

    //Hiding Legend
    $chart->setLegend(false);

    //Hiding MajorGridLines
    $chart->getAxes()->getHorizontalAxis()->getMajorGridLinesFormat()->getLine()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->NoFill);

    for ($i = 0; i < $chart->getChartData()->getSeries()->size(); i++)
    {
        $chart->getChartData()->getSeries()->removeAt($i);
    }

    $series = $chart->getChartData()->getSeries()->get_Item(0);

    $series->getMarker()->setSymbol(Java("com.aspose.slides.MarkerStyleType")->Circle);
    $series->getLabels()->getDefaultDataLabelFormat()->setShowValue(true);
    $series->getLabels()->getDefaultDataLabelFormat()->setPosition(Java("com.aspose.slides.LegendDataLabelPosition")->Top);
    $series->getMarker()->setSize(15);

    //Setting series line color
    $series->getFormat()->getLine()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
    $series->getFormat()->getLine()->getFillFormat()->getSolidFillColor()->setColor(Java("java.awt.Color")->MAGENTA);
    $series->getFormat()->getLine()->setDashStyle(Java("com.aspose.slides.LineDashStyle")->Solid);

    $pres->save("HideInformationFromChart.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```