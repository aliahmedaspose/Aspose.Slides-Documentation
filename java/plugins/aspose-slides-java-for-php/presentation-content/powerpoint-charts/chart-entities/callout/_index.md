---
title: Callout
type: docs
url: /java/callout/
---

## **Using Callouts**
New methods [**getShowLabelAsDataCallout()**](https://apireference.aspose.com/slides/java/com.aspose.slides/IDataLabelFormat#getShowLabelAsDataCallout--) and [**setShowLabelAsDataCallout()**](https://apireference.aspose.com/slides/java/com.aspose.slides/IDataLabelFormat#setShowLabelAsDataCallout-boolean-) have been added to [DataLabelFormat](http://www.aspose.com/api/java/slides/com.aspose.slides/classes/DataLabelFormat) class and [IDataLabelFormat](http://www.aspose.com/api/java/slides/com.aspose.slides/interfaces/IDataLabelFormat) interface. These methods determine either specified chart's data label will be displayed as data callout or as data label.

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->Pie, 50, 50, 500, 400);
    
    $chart->getChartData()->getSeries()->get_Item(0)->getLabels()->getDefaultDataLabelFormat()->setShowValue(true);
    $chart->getChartData()->getSeries()->get_Item(0)->getLabels()->getDefaultDataLabelFormat()->setShowLabelAsDataCallout(true);
    $chart->getChartData()->getSeries()->get_Item(0)->getLabels()->get_Item(2)->getDataLabelFormat()->setShowLabelAsDataCallout(false);
    
    $pres->save("DisplayCharts.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Set Callout for Doughnut Chart**
Aspose.Slides for Java provides support for setting series data label callout shape for a Doughnut $chart-> Below sample example is given. 

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $slide = $pres->getSlides()->get_Item(0);
    $chart = $slide->getShapes()->addChart(Java("com.aspose.slides.ChartType")->Doughnut, 10, 10, 500, 500, false);
    $workBook = $chart->getChartData()->getChartDataWorkbook();
    $chart->getChartData()->getSeries()->clear();
    $chart->getChartData()->getCategories()->clear();
    $chart->setLegend(false);
    $seriesIndex = 0;
    while ($seriesIndex < 15)
    {
        $series = $chart->getChartData()->getSeries()->add($workBook->getCell(0, 0, $seriesIndex + 1, "SERIES " . $seriesIndex), $chart->getType());
        $series->setExplosion(0);
        $series->getParentSeriesGroup()->setDoughnutHoleSize((new Java("java.lang.Integer", 20))->byteValue());
        $series->getParentSeriesGroup()->setFirstSliceAngle(351);
        $seriesIndex++;
    }
    $categoryIndex = 0;
    while ($categoryIndex < 15)
    {
        $chart->getChartData()->getCategories()->add($workBook->getCell(0, $categoryIndex + 1, 0, "CATEGORY " . $categoryIndex));
        $i = 0;
        while ($i< $chart->getChartData()->getSeries()->size())
        {
            $iCS = $chart->getChartData()->getSeries()->get_Item($i);
            $dataPoint = $iCS->getDataPoints()->addDataPointForDoughnutSeries($workBook->getCell(0, $categoryIndex + 1, i + 1, 1));
            $dataPoint->getFormat()->getFill()->setFillType(Java("com.aspose.slides.FillType")->Solid);
            $dataPoint->getFormat()->getLine()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
            $dataPoint->getFormat()->getLine()->getFillFormat()->getSolidFillColor()->setColor($java.awt.Color.WHITE);
            $dataPoint->getFormat()->getLine()->setWidth(1);
            $dataPoint->getFormat()->getLine()->setStyle(Java("com.aspose.slides.LineStyle")->Single);
            $dataPoint->getFormat()->getLine()->setDashStyle(Java("com.aspose.slides.LineDashStyle")->Solid);
            if ($i == $chart->getChartData()->getSeries()->size() - 1)
            {
               $lbl = $dataPoint->getLabel();
               $lbl->getTextFormat()->getTextBlockFormat()->setAutofitType(Java("com.aspose.slides.TextAutofitType")->Shape);
               $lbl->getDataLabelFormat()->getTextFormat()->getPortionFormat()->setFontBold(Java("com.aspose.slides.NullableBool")->True);
               $lbl->getDataLabelFormat()->getTextFormat()->getPortionFormat()->setLatinFont(new  Java("com.aspose.slides.FontData", "DINPro-Bold"));
               $lbl->getDataLabelFormat()->getTextFormat()->getPortionFormat()->setFontHeight(12);
               $lbl->getDataLabelFormat()->getTextFormat()->getPortionFormat()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
               $lbl->getDataLabelFormat()->getTextFormat()->getPortionFormat()->getFillFormat()->getSolidFillColor()->setColor($java.awt.Color.LIGHT_GRAY);
               $lbl->getDataLabelFormat()->getFormat()->getLine()->getFillFormat()->getSolidFillColor()->setColor($java.awt.Color.WHITE);
               $lbl->getDataLabelFormat()->setShowValue(false);
               $lbl->getDataLabelFormat()->setShowCategoryName(true);
               $lbl->getDataLabelFormat()->setShowSeriesName(false);
               $lbl->getDataLabelFormat()->setShowLeaderLines(true);
               $lbl->getDataLabelFormat()->setShowLabelAsDataCallout(false);
               $chart->validateChartLayout();
               $lbl->setX($lbl->getX()+ 0.5);
               $lbl->setY($lbl->getY()+ 0.5);
            }
            i++;
        }
        $categoryIndex++;
    }
    $pres->save("chart.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```
