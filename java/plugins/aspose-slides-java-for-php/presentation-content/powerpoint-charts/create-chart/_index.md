---
title: Create Chart
type: docs
weight: 10
url: /java/create-chart/
---

## **Create Chart**
Aspose.Slides for Java allows developers to create custom charts from slides. Aspose.Slides for Java creates charts independently of Aspose.Cells. 

Aspose.Slides for Java has simple APIs that allow you to create different types of charts, update charts, and perform other tasks involving charts. 



## **Creating Normal Charts**
1. Create an instance of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain the reference of a slide by index.
1. Add a chart with default data along with the desired type.
1. Add a chart title.
1. Access the chart data worksheet.
1. Clear all the default series and categories.
1. Add new series and categories.
1. Add new chart data for chart series.
1. Add fill color for chart series.
1. Add chart series labels.
1. Write the modified presentation as a PPTX file.

Sample code used to create a normal chart:

```php
// Instantiate Presentation class that represents PPTX file
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Access first slide
    $sld = $pres->getSlides()->get_Item(0);
    
    // Add chart with default data
    $chart = $sld->getShapes()->addChart(Java("com.aspose.slides.ChartType")->ClusteredColumn, 0, 0, 500, 500);
    
    // Setting chart Title
    $chart->getChartTitle()->addTextFrameForOverriding("Sample Title");
    $chart->getChartTitle()->getTextFrameForOverriding()->getTextFrameFormat()->setCenterText(Java("com.aspose.slides.NullableBool")->True);
    $chart->getChartTitle()->setHeight(20);
    $chart->hasTitle();
    
    // Set first series to Show Values
    $chart->getChartData()->getSeries()->get_Item(0)->getLabels()->getDefaultDataLabelFormat()->setShowValue(true);
    
    // Setting the index of chart data sheet
    $defaultWorksheetIndex = 0;
    
    // Getting the chart data WorkSheet
    $fact = $chart->getChartData()->getChartDataWorkbook();
    
    // Delete default generated series and categories
    $chart->getChartData()->getSeries()->clear();
    $chart->getChartData()->getCategories()->clear();
    $s = $chart->getChartData()->getSeries()->size();
    s = $chart->getChartData()->getCategories()->size();
    
    // Adding new series
    $chart->getChartData()->getSeries()->add(fact->getCell($defaultWorksheetIndex, 0, 1, "Series 1"),chart->getType());
    $chart->getChartData()->getSeries()->add(fact->getCell($defaultWorksheetIndex, 0, 2, "Series 2"),chart->getType());
    
    // Adding new categories
    $chart->getChartData()->getCategories()->add(fact->getCell($defaultWorksheetIndex, 1, 0, "Caetegoty 1"));
    $chart->getChartData()->getCategories()->add(fact->getCell($defaultWorksheetIndex, 2, 0, "Caetegoty 2"));
    $chart->getChartData()->getCategories()->add(fact->getCell($defaultWorksheetIndex, 3, 0, "Caetegoty 3"));
    
    // Take first chart series
    $series = $chart->getChartData()->getSeries()->get_Item(0);
    
    // Now populating series data
    $series->getDataPoints()->addDataPointForBarSeries(fact->getCell($defaultWorksheetIndex, 1, 1, 20));
    $series->getDataPoints()->addDataPointForBarSeries(fact->getCell($defaultWorksheetIndex, 2, 1, 50));
    $series->getDataPoints()->addDataPointForBarSeries(fact->getCell($defaultWorksheetIndex, 3, 1, 30));
    
    // Setting fill color for series
    $series->getFormat()->getFill()->setFillType(Java("com.aspose.slides.FillType")->Solid);
    $series->getFormat()->getFill()->getSolidFillColor()->setColor(Java("java.awt.Color")->RED);
    
    // Take second chart series
    $series = $chart->getChartData()->getSeries()->get_Item(1);
    
    // Now populating series data
    $series->getDataPoints()->addDataPointForBarSeries(fact->getCell($defaultWorksheetIndex, 1, 2, 30));
    $series->getDataPoints()->addDataPointForBarSeries(fact->getCell($defaultWorksheetIndex, 2, 2, 10));
    $series->getDataPoints()->addDataPointForBarSeries(fact->getCell($defaultWorksheetIndex, 3, 2, 60));
    
    // Setting fill color for series
    $series->getFormat()->getFill()->setFillType(Java("com.aspose.slides.FillType")->Solid);
    $series->getFormat()->getFill()->getSolidFillColor()->setColor(Java("java.awt.Color")->GREEN);
    
    // create custom labels for each of categories for new series
    // first label will be show Category name
    $lbl = $series->getDataPoints()->get_Item(0)->getLabel();
    $lbl->getDataLabelFormat()->setShowCategoryName(true);
    
    lbl = $series->getDataPoints()->get_Item(1)->getLabel();
    $lbl->getDataLabelFormat()->setShowSeriesName(true);
    
    // Show value for third label
    $lbl = $series->getDataPoints()->get_Item(2)->getLabel();
    $lbl->getDataLabelFormat()->setShowValue(true);
    $lbl->getDataLabelFormat()->setShowSeriesName(true);
    $lbl->getDataLabelFormat()->setSeparator("/");
    
    // Save presentation with chart
    $pres->save("output.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Creating Scattered Charts**
Sample code used to create a scatter chart with different series of markers:

```php
// Instantiate Presentation class that represents PPTX file
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Access first slide
    $slide = $pres->getSlides()->get_Item(0);

    // Creating the default chart
    $chart = $slide->getShapes()->addChart(Java("com.aspose.slides.ChartType")->ScatterWithSmoothLines, 0, 0, 400, 400);
    
    // Getting the default chart data worksheet index
    $defaultWorksheetIndex = 0;
    
    // Getting the chart data worksheet
    $fact = $chart->getChartData()->getChartDataWorkbook();
    
    // Delete demo series
    $chart->getChartData()->getSeries()->clear();
    
    // Add new series
    $chart->getChartData()->getSeries()->add(fact->getCell($defaultWorksheetIndex, 1, 1, "Series 1"), $chart->getType());
    $chart->getChartData()->getSeries()->add(fact->getCell($defaultWorksheetIndex, 1, 3, "Series 2"), $chart->getType());
    
    // Take first chart series
    $series = $chart->getChartData()->getSeries()->get_Item(0);
    
    // Add new point (1:3) there.
    $series->getDataPoints()->addDataPointForScatterSeries(fact->getCell($defaultWorksheetIndex, 2, 1, 1), $fact->getCell($defaultWorksheetIndex, 2, 2, 3));
    
    // Add new point (2:10)
    $series->getDataPoints()->addDataPointForScatterSeries(fact->getCell($defaultWorksheetIndex, 3, 1, 2), $fact->getCell($defaultWorksheetIndex, 3, 2, 10));
    
    // Edit the type of series
    $series->setType(Java("com.aspose.slides.ChartType")->ScatterWithStraightLinesAndMarkers);
    
    // Changing the chart series marker
    $series->getMarker()->setSize(10);
    $series->getMarker()->setSymbol(Java("com.aspose.slides.MarkerStyleType")->Star);
    
    // Take second chart series
    $series = $chart->getChartData()->getSeries()->get_Item(1);
    
    // Add new point (5:2) there.
    $series->getDataPoints()->addDataPointForScatterSeries(fact->getCell($defaultWorksheetIndex, 2, 3, 5), $fact->getCell($defaultWorksheetIndex, 2, 4, 2));
    
    // Add new point (3:1)
    $series->getDataPoints()->addDataPointForScatterSeries(fact->getCell($defaultWorksheetIndex, 3, 3, 3), $fact->getCell($defaultWorksheetIndex, 3, 4, 1));
    
    // Add new point (2:2)
    $series->getDataPoints()->addDataPointForScatterSeries(fact->getCell($defaultWorksheetIndex, 4, 3, 2), $fact->getCell($defaultWorksheetIndex, 4, 4, 2));
    
    // Add new point (5:1)
    $series->getDataPoints()->addDataPointForScatterSeries(fact->getCell($defaultWorksheetIndex, 5, 3, 5), $fact->getCell($defaultWorksheetIndex, 5, 4, 1));
    
    // Changing the chart series marker
    $series->getMarker()->setSize(10);
    $series->getMarker()->setSymbol(Java("com.aspose.slides.MarkerStyleType")->Circle);
    
    $pres->save("AsposeChart_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Creating Pie Charts**
1. Create an instance of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain a slide's reference by its index.
1. Add a chart with default data along with the desired type ([ChartType](https://apireference.aspose.com/slides/java/com.aspose.slides/ChartType).Pie).
1. Access the chart data [IChartDataWorkbook](https://apireference.aspose.com/slides/java/com.aspose.slides/IChartDataWorkbook).
1. Clear the default series and categories.
1. Add new series and categories.
1. Add new chart data for the chart series.
1. Add new points for charts and add custom colors for the pie chart's sectors.
1. Set labels for series.
1. Set leader lines for series labels.
1. Set the rotation angle for pie chart slides.
1. Write the modified presentation to a PPTX file

Sample code used to create a pie chart:

```php
// Instantiate Presentation class that represents PPTX file
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Access first slide
    $slides = $pres->getSlides()->get_Item(0);
    
    // Add chart with default data
    $chart = $slides->getShapes()->addChart(Java("com.aspose.slides.ChartType")->Pie, 100, 100, 400, 400);
    
    // Setting chart Title
    $chart->getChartTitle()->addTextFrameForOverriding("Sample Title");
    $chart->getChartTitle()->getTextFrameForOverriding()->getTextFrameFormat()->setCenterText(Java("com.aspose.slides.NullableBool")->True);
    $chart->getChartTitle()->setHeight(20);
    $chart->setTitle(true);
    
    // Set first series to Show Values
    $chart->getChartData()->getSeries()->get_Item(0)->getLabels()->getDefaultDataLabelFormat()->setShowValue(true);
    
    // Setting the index of chart data sheet
    $defaultWorksheetIndex = 0;
    
    // Getting the chart data worksheet
    $fact = $chart->getChartData()->getChartDataWorkbook();
    
    // Delete default generated series and categories
    $chart->getChartData()->getSeries()->clear();
    $chart->getChartData()->getCategories()->clear();
    
    // Adding new categories
    $chart->getChartData()->getCategories()->add(fact->getCell(0, 1, 0, "First Qtr"));
    $chart->getChartData()->getCategories()->add(fact->getCell(0, 2, 0, "2nd Qtr"));
    $chart->getChartData()->getCategories()->add(fact->getCell(0, 3, 0, "3rd Qtr"));
    
    // Adding new series
    $series = $chart->getChartData()->getSeries()->add(fact->getCell(0, 0, 1, "Series 1"), $chart->getType());
    
    // Now populating series data
    $series->getDataPoints()->addDataPointForPieSeries(fact->getCell($defaultWorksheetIndex, 1, 1, 20));
    $series->getDataPoints()->addDataPointForPieSeries(fact->getCell($defaultWorksheetIndex, 2, 1, 50));
    $series->getDataPoints()->addDataPointForPieSeries(fact->getCell($defaultWorksheetIndex, 3, 1, 30));
    
    // Not working in new version
    // Adding new points and setting sector color
    // series.IsColorVaried = true;
    $chart->getChartData()->getSeriesGroups()->get_Item(0)->setColorVaried(true);
    
    $point = $series->getDataPoints()->get_Item(0);
    $point->getFormat()->getFill()->setFillType(Java("com.aspose.slides.FillType")->Solid);
    $point->getFormat()->getFill()->getSolidFillColor()->setColor(Java("java.awt.Color")->CYAN);
	
    // Setting Sector border
    $point->getFormat()->getLine()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
    $point->getFormat()->getLine()->getFillFormat()->getSolidFillColor()->setColor(Java("java.awt.Color")->GRAY);
    $point->getFormat()->getLine()->setWidth(3.0);
    $point->getFormat()->getLine()->setStyle(Java("com.aspose.slides.LineStyle")->ThinThick);
    $point->getFormat()->getLine()->setDashStyle(Java("com.aspose.slides.LineDashStyle")->DashDot);
    
    $point1 = $series->getDataPoints()->get_Item(1);
    $point1->getFormat()->getFill()->setFillType(Java("com.aspose.slides.FillType")->Solid);
    $point1->getFormat()->getFill()->getSolidFillColor()->setColor(Java("java.awt.Color")->ORANGE);
    
    // Setting Sector border
    $point1->getFormat()->getLine()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
    $point1->getFormat()->getLine()->getFillFormat()->getSolidFillColor()->setColor(Java("java.awt.Color")->BLUE);
    $point1->getFormat()->getLine()->setWidth(3.0);
    $point1->getFormat()->getLine()->setStyle(Java("com.aspose.slides.LineStyle")->Single);
    $point1->getFormat()->getLine()->setDashStyle(Java("com.aspose.slides.LineDashStyle")->LargeDashDot);
    
    $point2 = $series->getDataPoints()->get_Item(2);
    $point2->getFormat()->getFill()->setFillType(Java("com.aspose.slides.FillType")->Solid);
    $point2->getFormat()->getFill()->getSolidFillColor()->setColor(Java("java.awt.Color")->YELLOW);
    
    // Setting Sector border
    $point2->getFormat()->getLine()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
    $point2->getFormat()->getLine()->getFillFormat()->getSolidFillColor()->setColor(Java("java.awt.Color")->RED);
    $point2->getFormat()->getLine()->setWidth(2.0);
    $point2->getFormat()->getLine()->setStyle(Java("com.aspose.slides.LineStyle")->ThinThin);
    $point2->getFormat()->getLine()->setDashStyle(Java("com.aspose.slides.LineDashStyle")->LargeDashDotDot);
    
    // Create custom labels for each of categories for new series
    $lbl1 = $series->getDataPoints()->get_Item(0)->getLabel();
    
    // lbl.ShowCategoryName = true;
    $lbl1->getDataLabelFormat()->setShowValue(true);
    
    $lbl2 = $series->getDataPoints()->get_Item(1)->getLabel();
    $lbl2->getDataLabelFormat()->setShowValue(true);
    $lbl2->getDataLabelFormat()->setShowLegendKey(true);
    $lbl2->getDataLabelFormat()->setShowPercentage(true);
    
    $lbl3 = $series->getDataPoints()->get_Item(2)->getLabel();
    $lbl3->getDataLabelFormat()->setShowSeriesName(true);
    $lbl3->getDataLabelFormat()->setShowPercentage(true);
    
    // Showing Leader Lines for Chart
    $series->getLabels()->getDefaultDataLabelFormat()->setShowLeaderLines(true);
    
    // Setting Rotation Angle for Pie Chart Sectors
    $chart->getChartData()->getSeriesGroups()->get_Item(0)->setFirstSliceAngle(180);
    
    // Save presentation with chart
    $pres->save("PieChart_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Creating Tree Map Charts**
1. Create an instance of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain a slide's reference by its index.
1. Add a chart with default data along with the desired type ([ChartType](https://apireference.aspose.com/slides/java/com.aspose.slides/ChartType).TreeMap).
1. Access the chart data [IChartDataWorkbook](https://apireference.aspose.com/slides/java/com.aspose.slides/IChartDataWorkbook).
1. Clear the default series and categories.
1. Add new series and categories.
1. Add new chart data for the chart series.
1. Write the modified presentation to a PPTX file

Sample code used to create a chart:

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->Treemap, 50, 50, 500, 400);
    $chart->getChartData()->getCategories()->clear();
    $chart->getChartData()->getSeries()->clear();

    $wb = $chart->getChartData()->getChartDataWorkbook();
    $wb->clear(0);

    //branch 1
    $leaf = $chart->getChartData()->getCategories()->add($wb->getCell(0, "C1", "Leaf1"));
    $leaf->getGroupingLevels()->setGroupingItem(1, "Stem1");
    $leaf->getGroupingLevels()->setGroupingItem(2, "Branch1");

    $chart->getChartData()->getCategories()->add($wb->getCell(0, "C2", "Leaf2"));

    $leaf = $chart->getChartData()->getCategories()->add($wb->getCell(0, "C3", "Leaf3"));
    $leaf->getGroupingLevels()->setGroupingItem(1, "Stem2");

    $chart->getChartData()->getCategories()->add($wb->getCell(0, "C4", "Leaf4"));

    //branch 2
    $leaf = $chart->getChartData()->getCategories()->add($wb->getCell(0, "C5", "Leaf5"));
    $leaf->getGroupingLevels()->setGroupingItem(1, "Stem3");
    $leaf->getGroupingLevels()->setGroupingItem(2, "Branch2");

    $chart->getChartData()->getCategories()->add($wb->getCell(0, "C6", "Leaf6"));

    $leaf = $chart->getChartData()->getCategories()->add($wb->getCell(0, "C7", "Leaf7"));
    $leaf->getGroupingLevels()->setGroupingItem(1, "Stem4");

    $chart->getChartData()->getCategories()->add($wb->getCell(0, "C8", "Leaf8"));

    $series = $chart->getChartData()->getSeries()->add(Java("com.aspose.slides.ChartType")->Treemap);
    $series->getLabels()->getDefaultDataLabelFormat()->setShowCategoryName(true);
    $series->getDataPoints()->addDataPointForTreemapSeries($wb->getCell(0, "D1", 4));
    $series->getDataPoints()->addDataPointForTreemapSeries($wb->getCell(0, "D2", 5));
    $series->getDataPoints()->addDataPointForTreemapSeries($wb->getCell(0, "D3", 3));
    $series->getDataPoints()->addDataPointForTreemapSeries($wb->getCell(0, "D4", 6));
    $series->getDataPoints()->addDataPointForTreemapSeries($wb->getCell(0, "D5", 9));
    $series->getDataPoints()->addDataPointForTreemapSeries($wb->getCell(0, "D6", 9));
    $series->getDataPoints()->addDataPointForTreemapSeries($wb->getCell(0, "D7", 4));
    $series->getDataPoints()->addDataPointForTreemapSeries($wb->getCell(0, "D8", 3));

    $series->setParentLabelLayout(Java("com.aspose.slides.ParentLabelLayoutType")->Overlapping);

    $pres->save("Treemap.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Creating Stock Charts**
1. Create an instance of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain a slide's reference by its index.
1. Add a chart with default data along with the desired type ([ChartType](https://apireference.aspose.com/slides/java/com.aspose.slides/ChartType).OpenHighLowClose).
1. Access the chart data [IChartDataWorkbook](https://apireference.aspose.com/slides/java/com.aspose.slides/IChartDataWorkbook).
1. Clear the default series and categories.
1. Add new series and categories.
1. Add new chart data for the chart series.
1. Specify HiLowLines format.
1. Write the modified presentation to a PPTX file

Sample code used to create a chart:

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->OpenHighLowClose, 50, 50, 600, 400, false);

    $chart->getChartData()->getSeries()->clear();
    $chart->getChartData()->getCategories()->clear();

    $wb = $chart->getChartData()->getChartDataWorkbook();

    $chart->getChartData()->getCategories()->add($wb->getCell(0, 1, 0, "A"));
    $chart->getChartData()->getCategories()->add($wb->getCell(0, 2, 0, "B"));
    $chart->getChartData()->getCategories()->add($wb->getCell(0, 3, 0, "C"));

    $chart->getChartData()->getSeries()->add($wb->getCell(0, 0, 1, "Open"), $chart->getType());
    $chart->getChartData()->getSeries()->add($wb->getCell(0, 0, 2, "High"), $chart->getType());
    $chart->getChartData()->getSeries()->add($wb->getCell(0, 0, 3, "Low"), $chart->getType());
    $chart->getChartData()->getSeries()->add($wb->getCell(0, 0, 4, "Close"), $chart->getType());

    $series = $chart->getChartData()->getSeries()->get_Item(0);

    $series->getDataPoints()->addDataPointForStockSeries($wb->getCell(0, 1, 1, 72));
    $series->getDataPoints()->addDataPointForStockSeries($wb->getCell(0, 2, 1, 25));
    $series->getDataPoints()->addDataPointForStockSeries($wb->getCell(0, 3, 1, 38));

    $series = $chart->getChartData()->getSeries()->get_Item(1);
    $series->getDataPoints()->addDataPointForStockSeries($wb->getCell(0, 1, 2, 172));
    $series->getDataPoints()->addDataPointForStockSeries($wb->getCell(0, 2, 2, 57));
    $series->getDataPoints()->addDataPointForStockSeries($wb->getCell(0, 3, 2, 57));

    $series = $chart->getChartData()->getSeries()->get_Item(2);
    $series->getDataPoints()->addDataPointForStockSeries($wb->getCell(0, 1, 3, 12));
    $series->getDataPoints()->addDataPointForStockSeries($wb->getCell(0, 2, 3, 12));
    $series->getDataPoints()->addDataPointForStockSeries($wb->getCell(0, 3, 3, 13));

    $series = $chart->getChartData()->getSeries()->get_Item(3);
    $series->getDataPoints()->addDataPointForStockSeries($wb->getCell(0, 1, 4, 25));
    $series->getDataPoints()->addDataPointForStockSeries($wb->getCell(0, 2, 4, 38));
    $series->getDataPoints()->addDataPointForStockSeries($wb->getCell(0, 3, 4, 50));

    $chart->getChartData()->getSeriesGroups()->get_Item(0)->getUpDownBars()->setUpDownBars(true);
    $chart->getChartData()->getSeriesGroups()->get_Item(0)->getHiLowLinesFormat()->getLine()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);

    foreach( $chart->getChartData()->getSeries() as $ser )
    {
        $ser->getFormat()->getLine()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->NoFill);
    }

    $pres->save("output.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Creating Box and Whisker Charts**
1. Create an instance of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain a slide's reference by its index.
1. Add a chart with default data along with the desired type ([ChartType](https://apireference.aspose.com/slides/java/com.aspose.slides/ChartType).BoxAndWhisker).
1. Access the chart data [IChartDataWorkbook](https://apireference.aspose.com/slides/java/com.aspose.slides/IChartDataWorkbook).
1. Clear the default series and categories.
1. Add new series and categories.
1. Add new chart data for the chart series.
1. Write the modified presentation to a PPTX file

The following code is used to create a $chart->

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->BoxAndWhisker, 50, 50, 500, 400);
    $chart->getChartData()->getCategories()->clear();
    $chart->getChartData()->getSeries()->clear();

    $wb = $chart->getChartData()->getChartDataWorkbook();
    $wb->clear(0);

    $chart->getChartData()->getCategories()->add($wb->getCell(0, "A1", "Category 1"));
    $chart->getChartData()->getCategories()->add($wb->getCell(0, "A2", "Category 1"));
    $chart->getChartData()->getCategories()->add($wb->getCell(0, "A3", "Category 1"));
    $chart->getChartData()->getCategories()->add($wb->getCell(0, "A4", "Category 1"));
    $chart->getChartData()->getCategories()->add($wb->getCell(0, "A5", "Category 1"));
    $chart->getChartData()->getCategories()->add($wb->getCell(0, "A6", "Category 1"));

    $series = $chart->getChartData()->getSeries()->add(Java("com.aspose.slides.ChartType")->BoxAndWhisker);

    $series->setQuartileMethod(QuartileMethodType.Exclusive);
    $series->setShowMeanLine(true);
    $series->setShowMeanMarkers(true);
    $series->setShowInnerPoints(true);
    $series->setShowOutlierPoints(true);

    $series->getDataPoints()->addDataPointForBoxAndWhiskerSeries($wb->getCell(0, "B1", 15));
    $series->getDataPoints()->addDataPointForBoxAndWhiskerSeries($wb->getCell(0, "B2", 41));
    $series->getDataPoints()->addDataPointForBoxAndWhiskerSeries($wb->getCell(0, "B3", 16));
    $series->getDataPoints()->addDataPointForBoxAndWhiskerSeries($wb->getCell(0, "B4", 10));
    $series->getDataPoints()->addDataPointForBoxAndWhiskerSeries($wb->getCell(0, "B5", 23));
    $series->getDataPoints()->addDataPointForBoxAndWhiskerSeries($wb->getCell(0, "B6", 16));

    $pres->save("BoxAndWhisker.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Creating Funnel Charts**
1. Create an instance of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain a slide's reference by its index.
1. Add a chart with default data along with the desired type ([ChartType](https://apireference.aspose.com/slides/java/com.aspose.slides/ChartType).Funnel).
1. Write the modified presentation to a PPTX file

The following code is used to create a $chart->

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->Funnel, 50, 50, 500, 400);
    $chart->getChartData()->getCategories()->clear();
    $chart->getChartData()->getSeries()->clear();

    $wb = $chart->getChartData()->getChartDataWorkbook();

    $wb->clear(0);

    $chart->getChartData()->getCategories()->add($wb->getCell(0, "A1", "Category 1"));
    $chart->getChartData()->getCategories()->add($wb->getCell(0, "A2", "Category 2"));
    $chart->getChartData()->getCategories()->add($wb->getCell(0, "A3", "Category 3"));
    $chart->getChartData()->getCategories()->add($wb->getCell(0, "A4", "Category 4"));
    $chart->getChartData()->getCategories()->add($wb->getCell(0, "A5", "Category 5"));
    $chart->getChartData()->getCategories()->add($wb->getCell(0, "A6", "Category 6"));

    $series = $chart->getChartData()->getSeries()->add(Java("com.aspose.slides.ChartType")->Funnel);

    $series->getDataPoints()->addDataPointForFunnelSeries($wb->getCell(0, "B1", 50));
    $series->getDataPoints()->addDataPointForFunnelSeries($wb->getCell(0, "B2", 100));
    $series->getDataPoints()->addDataPointForFunnelSeries($wb->getCell(0, "B3", 200));
    $series->getDataPoints()->addDataPointForFunnelSeries($wb->getCell(0, "B4", 300));
    $series->getDataPoints()->addDataPointForFunnelSeries($wb->getCell(0, "B5", 400));
    $series->getDataPoints()->addDataPointForFunnelSeries($wb->getCell(0, "B6", 500));

    $pres->save("Funnel.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Creating Sunburst Charts**
1. Create an instance of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain a slide's reference by its index.
1. Add a chart with default data along with the desired type ([ChartType](https://apireference.aspose.com/slides/java/com.aspose.slides/ChartType).sunburst).
1. Write the modified presentation to a PPTX file

The following code is used to create a $chart->

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->Sunburst, 50, 50, 500, 400);
    $chart->getChartData()->getCategories()->clear();
    $chart->getChartData()->getSeries()->clear();

    $wb = $chart->getChartData()->getChartDataWorkbook();
    $wb->clear(0);

    //branch 1
    $leaf = $chart->getChartData()->getCategories()->add($wb->getCell(0, "C1", "Leaf1"));
    $leaf->getGroupingLevels()->setGroupingItem(1, "Stem1");
    $leaf->getGroupingLevels()->setGroupingItem(2, "Branch1");

    $chart->getChartData()->getCategories()->add($wb->getCell(0, "C2", "Leaf2"));

    $leaf = $chart->getChartData()->getCategories()->add($wb->getCell(0, "C3", "Leaf3"));
    $leaf->getGroupingLevels()->setGroupingItem(1, "Stem2");

    $chart->getChartData()->getCategories()->add($wb->getCell(0, "C4", "Leaf4"));

    //branch 2
    $leaf = $chart->getChartData()->getCategories()->add($wb->getCell(0, "C5", "Leaf5"));
    $leaf->getGroupingLevels()->setGroupingItem(1, "Stem3");
    $leaf->getGroupingLevels()->setGroupingItem(2, "Branch2");

    $chart->getChartData()->getCategories()->add($wb->getCell(0, "C6", "Leaf6"));

    $leaf = $chart->getChartData()->getCategories()->add($wb->getCell(0, "C7", "Leaf7"));
    $leaf->getGroupingLevels()->setGroupingItem(1, "Stem4");

    $chart->getChartData()->getCategories()->add($wb->getCell(0, "C8", "Leaf8"));

    $series = $chart->getChartData()->getSeries()->add(Java("com.aspose.slides.ChartType")->Sunburst);
    $series->getLabels()->getDefaultDataLabelFormat()->setShowCategoryName(true);
    $series->getDataPoints()->addDataPointForSunburstSeries($wb->getCell(0, "D1", 4));
    $series->getDataPoints()->addDataPointForSunburstSeries($wb->getCell(0, "D2", 5));
    $series->getDataPoints()->addDataPointForSunburstSeries($wb->getCell(0, "D3", 3));
    $series->getDataPoints()->addDataPointForSunburstSeries($wb->getCell(0, "D4", 6));
    $series->getDataPoints()->addDataPointForSunburstSeries($wb->getCell(0, "D5", 9));
    $series->getDataPoints()->addDataPointForSunburstSeries($wb->getCell(0, "D6", 9));
    $series->getDataPoints()->addDataPointForSunburstSeries($wb->getCell(0, "D7", 4));
    $series->getDataPoints()->addDataPointForSunburstSeries($wb->getCell(0, "D8", 3));
    
    $pres->save("Sunburst.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Creating Histogram Charts**
1. Create an instance of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain a slide's reference by its index.
1. Add a chart with default data along with the desired type ([ChartType](https://apireference.aspose.com/slides/java/com.aspose.slides/ChartType).Histogram).
1. Access the chart data [IChartDataWorkbook](https://apireference.aspose.com/slides/java/com.aspose.slides/IChartDataWorkbook).
1. Clear the default series and categories.
1. Add new series and categories.
1. Write the modified presentation to a PPTX file

The following code is used to create a $chart->

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->Histogram, 50, 50, 500, 400);
    $chart->getChartData()->getCategories()->clear();
    $chart->getChartData()->getSeries()->clear();

    $wb = $chart->getChartData()->getChartDataWorkbook();
    $wb->clear(0);

    $series = $chart->getChartData()->getSeries()->add(Java("com.aspose.slides.ChartType")->Histogram);
    $series->getDataPoints()->addDataPointForHistogramSeries($wb->getCell(0, "A1", 15));
    $series->getDataPoints()->addDataPointForHistogramSeries($wb->getCell(0, "A2", -41));
    $series->getDataPoints()->addDataPointForHistogramSeries($wb->getCell(0, "A3", 16));
    $series->getDataPoints()->addDataPointForHistogramSeries($wb->getCell(0, "A4", 10));
    $series->getDataPoints()->addDataPointForHistogramSeries($wb->getCell(0, "A5", -23));
    $series->getDataPoints()->addDataPointForHistogramSeries($wb->getCell(0, "A6", 16));

    $chart->getAxes()->getHorizontalAxis()->setAggregationType(AxisAggregationType.Automatic;)

    $pres->save("Histogram.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Creating Multi Category Charts**
1. Create an instance of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain a slide's reference by its index.
1. Add a chart with default data along with the desired type ([ChartType](https://apireference.aspose.com/slides/java/com.aspose.slides/ChartType).ClusteredColumn).
1. Access the chart data [IChartDataWorkbook](https://apireference.aspose.com/slides/java/com.aspose.slides/IChartDataWorkbook).
1. Clear the default series and categories.
1. Add new series and categories.
1. Add new chart data for the chart series.
1. Write the modified presentation to a PPTX file.

The following code is used to create a $chart->

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $ch = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->ClusteredColumn, 100, 100, 600, 450);
    $ch->getChartData()->getSeries()->clear();
    $ch->getChartData()->getCategories()->clear();
    
    $fact = $ch->getChartData()->getChartDataWorkbook();
    $fact->clear(0);
    $defaultWorksheetIndex = 0;

    $category = $ch->getChartData()->getCategories()->add(fact->getCell(0, "c2", "A"));
    category->getGroupingLevels()->setGroupingItem(1, "Group1");
    category = $ch->getChartData()->getCategories()->add(fact->getCell(0, "c3", "B"));

    category = $ch->getChartData()->getCategories()->add(fact->getCell(0, "c4", "C"));
    category->getGroupingLevels()->setGroupingItem(1, "Group2");
    category = $ch->getChartData()->getCategories()->add(fact->getCell(0, "c5", "D"));

    category = $ch->getChartData()->getCategories()->add(fact->getCell(0, "c6", "E"));
    category->getGroupingLevels()->setGroupingItem(1, "Group3");
    category = $ch->getChartData()->getCategories()->add(fact->getCell(0, "c7", "F"));

    category = $ch->getChartData()->getCategories()->add(fact->getCell(0, "c8", "G"));
    category->getGroupingLevels()->setGroupingItem(1, "Group4");
    category = $ch->getChartData()->getCategories()->add(fact->getCell(0, "c9", "H"));

    // Adding Series
    $series = $ch->getChartData()->getSeries()->add(fact->getCell(0, "D1", "Series 1"),
            Java("com.aspose.slides.ChartType")->ClusteredColumn);

    $series->getDataPoints()->addDataPointForBarSeries(fact->getCell($defaultWorksheetIndex, "D2", 10));
    $series->getDataPoints()->addDataPointForBarSeries(fact->getCell($defaultWorksheetIndex, "D3", 20));
    $series->getDataPoints()->addDataPointForBarSeries(fact->getCell($defaultWorksheetIndex, "D4", 30));
    $series->getDataPoints()->addDataPointForBarSeries(fact->getCell($defaultWorksheetIndex, "D5", 40));
    $series->getDataPoints()->addDataPointForBarSeries(fact->getCell($defaultWorksheetIndex, "D6", 50));
    $series->getDataPoints()->addDataPointForBarSeries(fact->getCell($defaultWorksheetIndex, "D7", 60));
    $series->getDataPoints()->addDataPointForBarSeries(fact->getCell($defaultWorksheetIndex, "D8", 70));
    $series->getDataPoints()->addDataPointForBarSeries(fact->getCell($defaultWorksheetIndex, "D9", 80));
    
    // Save presentation with chart
    $pres->save("AsposeChart_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Updating Charts**
To update a chart, do this:

- Open an instance of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class containing the $chart->
- Obtain the reference of a slide by using its Index.
- Traverse through all shapes to find the desired $chart->
- Access the chart data worksheet.
- Modify the chart data series data by changing series values.
- Add a new series and populate the data in it.
- Write the modified presentation as a PPTX file.

Code sample used to update a chart:

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Access first slideMarker
    $sld = $pres->getSlides()->get_Item(0);

    // Get chart with default data
    $chart = $sld->getShapes()->get_Item(0);

    // Setting the index of chart data sheet
    $defaultWorksheetIndex = 0;

    // Getting the chart data worksheet
    $fact = $chart->getChartData()->getChartDataWorkbook();

    // Changing chart Category Name
    $fact->getCell($defaultWorksheetIndex, 1, 0, "Modified Category 1");
    $fact->getCell($defaultWorksheetIndex, 2, 0, "Modified Category 2");

    // Take first chart series
    $series = $chart->getChartData()->getSeries()->get_Item(0);

    // Now updating series data
    $fact->getCell($defaultWorksheetIndex, 0, 1, "New_Series1");// Modifying series name
    $series->getDataPoints()->get_Item(0)->getValue()->setData(90);
    $series->getDataPoints()->get_Item(1)->getValue()->setData(123);
    $series->getDataPoints()->get_Item(2)->getValue()->setData(44);

    // Take Second chart series
    $series = $chart->getChartData()->getSeries()->get_Item(1);

    // Now updating series data
    $fact->getCell($defaultWorksheetIndex, 0, 2, "New_Series2");// Modifying series name
    $series->getDataPoints()->get_Item(0)->getValue()->setData(23);
    $series->getDataPoints()->get_Item(1)->getValue()->setData(67);
    $series->getDataPoints()->get_Item(2)->getValue()->setData(99);

    // Now, Adding a new series
    $chart->getChartData()->getSeries()->add(fact->getCell($defaultWorksheetIndex, 0, 3, "Series 3"), $chart->getType());

    // Take 3rd chart series
    $series = $chart->getChartData()->getSeries()->get_Item(2);

    // Now populating series data
    $series->getDataPoints()->addDataPointForBarSeries(fact->getCell($defaultWorksheetIndex, 1, 3, 20));
    $series->getDataPoints()->addDataPointForBarSeries(fact->getCell($defaultWorksheetIndex, 2, 3, 50));
    $series->getDataPoints()->addDataPointForBarSeries(fact->getCell($defaultWorksheetIndex, 3, 3, 30));

    $chart->setType(Java("com.aspose.slides.ChartType")->ClusteredCylinder);

    // Save presentation with chart
    $pres->save("AsposeChartModified_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Setting Data Range for Charts**

To set the data range for a chart, do this:

- Open an instance of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class containing the $chart->
- Obtain the reference of a slide by using its Index.
- Traverse through all shapes to find the desired $chart->
- Access the chart data and set the range.
- Save the modified presentation as a PPTX file.

Code sample used to set data range for a chart:

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $slide = $pres->getSlides()->get_Item(0);
    $chart = $slide->getShapes()->get_Item(0);
    
    $chart->getChartData()->setRange("Sheet1!A1:B4");
    
    $pres->save("SetDataRange_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Using Default Markers in Charts**
Aspose.Slides for Java has a simple API that can help you set the chart series marker automatically. When you use a default marker in charts, each chart series get different default marker symbols automatically.

Code sample used to set a chart series marker automatically:

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $slide = $pres->getSlides()->get_Item(0);
    $chart = $slide->getShapes()->addChart(Java("com.aspose.slides.ChartType")->LineWithMarkers, 10, 10, 400, 400);

    $chart->getChartData()->getSeries()->clear();
    $chart->getChartData()->getCategories()->clear();

    $fact = $chart->getChartData()->getChartDataWorkbook();
    $chart->getChartData()->getSeries()->add(fact->getCell(0, 0, 1, "Series 1"), $chart->getType());
    $series = $chart->getChartData()->getSeries()->get_Item(0);

    $chart->getChartData()->getCategories()->add(fact->getCell(0, 1, 0, "C1"));
    $series->getDataPoints()->addDataPointForLineSeries(fact->getCell(0, 1, 1, 24));
    $chart->getChartData()->getCategories()->add(fact->getCell(0, 2, 0, "C2"));
    $series->getDataPoints()->addDataPointForLineSeries(fact->getCell(0, 2, 1, 23));
    $chart->getChartData()->getCategories()->add(fact->getCell(0, 3, 0, "C3"));
    $series->getDataPoints()->addDataPointForLineSeries(fact->getCell(0, 3, 1, -10));
    $chart->getChartData()->getCategories()->add(fact->getCell(0, 4, 0, "C4"));
    $series->getDataPoints()->addDataPointForLineSeries(fact->getCell(0, 4, 1, null));

    $chart->getChartData()->getSeries()->add(fact->getCell(0, 0, 2, "Series 2"), $chart->getType());
    //Take second chart series
    $series2 = $chart->getChartData()->getSeries()->get_Item(1);

    //Now populating series data
    $series2->getDataPoints()->addDataPointForLineSeries(fact->getCell(0, 1, 2, 30));
    $series2->getDataPoints()->addDataPointForLineSeries(fact->getCell(0, 2, 2, 10));
    $series2->getDataPoints()->addDataPointForLineSeries(fact->getCell(0, 3, 2, 60));
    $series2->getDataPoints()->addDataPointForLineSeries(fact->getCell(0, 4, 2, 40));

    $chart->setLegend(true);
    $chart->getLegend()->setOverlay(false);

    $pres->save("DefaultMarkersInChart.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```
