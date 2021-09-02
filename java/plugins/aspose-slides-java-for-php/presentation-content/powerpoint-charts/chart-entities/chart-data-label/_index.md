---
title: Chart Data Label
type: docs
url: /java/chart-data-label/
---

## **Set Precision of Data in Chart Data Labels**
Aspose.Slides for Java provides a simple API for setting precision of data in chart data label. Below sample example is given. 

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->Line, 50, 50, 450, 300);
    
    $chart->setDataTable(true);
    $chart->getChartData()->getSeries()->get_Item(0)->setNumberFormatOfValues("#,##0.00");

    $pres->save("output.pptx",Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Display Percentage as Labels**
Aspose.Slides for Java supports displaying the percentage as labels. In this topic, we will see with example how to display the percentage as labels using Aspose.Slides. In order to set percentage as display. Please follow the steps below.

1. Instantiate [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) object.
1. Add stacked column $chart->
1. Calculate the series data point values for particular categories.
1. Displaying the percentage as labels.
1. Set properties of label.
1. Write presentation to disk.

In the example given below, we have set the percentage as label.

```php
// Creating empty presentation
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Access first slide
    $slide = $pres->getSlides()->get_Item(0);
    
    $chart = $slide->getShapes()->addChart(Java("com.aspose.slides.ChartType")->StackedColumn, 20, 20, 400, 400);
    $series;
    double[] total_for_Cat = new double[chart->getChartData()->getCategories()->size()];
    for ($k = 0; k < $chart->getChartData()->getCategories()->size(); k++) {
        $cat = $chart->getChartData()->getCategories()->get_Item(k);
    
        for ($i = 0; i < $chart->getChartData()->getSeries()->size(); i++) {
            total_for_Cat[k] = total_for_Cat[k] + ($chart->getChartData()->getSeries()->get_Item($i)->getDataPoints()->get_Item(k)->getValue()->getData());
        }
    }
    
    $dataPontPercent = 0;
    for ($x = 0; x < $chart->getChartData()->getSeries()->size(); x++) {
        $series = $chart->getChartData()->getSeries()->get_Item(x);
        $series->getLabels()->getDefaultDataLabelFormat()->setShowLegendKey(false);
    
        for ($j = 0; j < $series->getDataPoints()->size(); j++) {
            $lbl = $series->getDataPoints()->get_Item($j)->getLabel();
            $dataPontPercent = ((series->getDataPoints()->get_Item($j)->getValue()->getData())) / (total_for_Cat[j]) * 100;
    
            $port = new Java("com.aspose.slides.Portion");
            $port->setText(String.format("{0:F2} %.2", $dataPontPercent));
            $port->getPortionFormat()->setFontHeight(8);
            $lbl->getTextFrameForOverriding()->setText("");
            $para =$lbl->getTextFrameForOverriding()->getParagraphs()->get_Item(0);
            $para->getPortions()->add($port);
    
           $lbl->getDataLabelFormat()->setShowSeriesName(false);
           $lbl->getDataLabelFormat()->setShowPercentage(false);
           $lbl->getDataLabelFormat()->setShowLegendKey(false);
           $lbl->getDataLabelFormat()->setShowCategoryName(false);
           $lbl->getDataLabelFormat()->setShowBubbleSize(false);
        }
    }
    
    // Save presentation with chart
    $pres->save("output.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Set Percentage Sign with Chart Data Labels**
In order to set the percentage sign with chart data labels. Please follow the steps below:

- Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
- Get reference of the slide.
- Add PercentsStackedColumn chart on a slide.
- Set NumberFormatLinkedToSource to false.
- Getting the chart data worksheet.
- Add new series.
- Setting the fill color of series.
- Setting LabelFormat properties.
- Write the presentation as a PPTX file.

```php
// Creating empty presentation
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Get reference of the slide
    $slide = $pres->getSlides()->get_Item(0);
    
    // Add PercentsStackedColumn chart on a slide
    $chart = $slide->getShapes()->addChart(Java("com.aspose.slides.ChartType")->PercentsStackedColumn, 20, 20, 500, 400);
    
    // Set NumberFormatLinkedToSource to false
    $chart->getAxes()->getVerticalAxis()->setNumberFormatLinkedToSource(false);
    $chart->getAxes()->getVerticalAxis()->setNumberFormat("0.00%");
    
    $chart->getChartData()->getSeries()->clear();
    $defaultWorksheetIndex = 0;
    
    // Getting the chart data worksheet
    $workbook = $chart->getChartData()->getChartDataWorkbook();
    
    // Add new series
    $series = $chart->getChartData()->getSeries()->add(workbook->getCell($defaultWorksheetIndex, 0, 1, "Reds"), $chart->getType());
    $series->getDataPoints()->addDataPointForBarSeries(workbook->getCell($defaultWorksheetIndex, 1, 1, 0.30));
    $series->getDataPoints()->addDataPointForBarSeries(workbook->getCell($defaultWorksheetIndex, 2, 1, 0.50));
    $series->getDataPoints()->addDataPointForBarSeries(workbook->getCell($defaultWorksheetIndex, 3, 1, 0.80));
    $series->getDataPoints()->addDataPointForBarSeries(workbook->getCell($defaultWorksheetIndex, 4, 1, 0.65));
    
    // Setting the fill color of series
    $series->getFormat()->getFill()->setFillType(Java("com.aspose.slides.FillType")->Solid);
    $series->getFormat()->getFill()->getSolidFillColor()->setColor(Java("java.awt.Color")->RED);
    
    // Setting LabelFormat properties
    $series->getLabels()->getDefaultDataLabelFormat()->setShowValue(true);
    $series->getLabels()->getDefaultDataLabelFormat()->setNumberFormatLinkedToSource(false);
    $series->getLabels()->getDefaultDataLabelFormat()->setNumberFormat("0.0%");
    $series->getLabels()->getDefaultDataLabelFormat()->getTextFormat()->getPortionFormat()->setFontHeight(10);
    $series->getLabels()->getDefaultDataLabelFormat()->getTextFormat()->getPortionFormat()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
    $series->getLabels()->getDefaultDataLabelFormat()->getTextFormat()->getPortionFormat()->getFillFormat()->getSolidFillColor()->setColor(Java("java.awt.Color")->WHITE);
    $series->getLabels()->getDefaultDataLabelFormat()->setShowValue(true);
    
    // Add new series
    $series2 = $chart->getChartData()->getSeries()->add(workbook->getCell($defaultWorksheetIndex, 0, 2, "Blues"), $chart->getType());
    $series2->getDataPoints()->addDataPointForBarSeries(workbook->getCell($defaultWorksheetIndex, 1, 2, 0.70));
    $series2->getDataPoints()->addDataPointForBarSeries(workbook->getCell($defaultWorksheetIndex, 2, 2, 0.50));
    $series2->getDataPoints()->addDataPointForBarSeries(workbook->getCell($defaultWorksheetIndex, 3, 2, 0.20));
    $series2->getDataPoints()->addDataPointForBarSeries(workbook->getCell($defaultWorksheetIndex, 4, 2, 0.35));
    
    // Setting Fill type and color
    $series2->getFormat()->getFill()->setFillType(Java("com.aspose.slides.FillType")->Solid);
    $series2->getFormat()->getFill()->getSolidFillColor()->setColor(Java("java.awt.Color")->BLUE);
    $series2->getLabels()->getDefaultDataLabelFormat()->setShowValue(true);
    $series2->getLabels()->getDefaultDataLabelFormat()->setNumberFormatLinkedToSource(false);
    $series2->getLabels()->getDefaultDataLabelFormat()->setNumberFormat("0.0%");
    $series2->getLabels()->getDefaultDataLabelFormat()->getTextFormat()->getPortionFormat()->setFontHeight(10);
    $series2->getLabels()->getDefaultDataLabelFormat()->getTextFormat()->getPortionFormat()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
    $series2->getLabels()->getDefaultDataLabelFormat()->getTextFormat()->getPortionFormat()->getFillFormat()->getSolidFillColor()->setColor(Java("java.awt.Color")->WHITE);
    
    // Write presentation to disk
    $pres->save("SetDataLabelsPercentageSign_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Set Label Distances**
In order to set the Label Distance. Please follow the steps below:

- Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
- Get reference of the slide.
- Adding a chart on slide.
- Setting the position of label from axis.
- Write the presentation as a PPTX file.

In the example given below, we have set the label distance from category axis.

```php
// Creating empty presentation
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Get reference of the slide
    $sld = $pres->getSlides()->get_Item(0);
    
    // Adding a chart on slide
    $ch = $sld->getShapes()->addChart(Java("com.aspose.slides.ChartType")->ClusteredColumn, 20, 20, 500, 300);
    
    // Setting the position of label from axis
    $ch->getAxes()->getHorizontalAxis()->setLabelOffset(500);
    
    // Write the presentation to disk
    $pres->save("output.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```
