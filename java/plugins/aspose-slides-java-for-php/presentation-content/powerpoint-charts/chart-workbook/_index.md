---
title: Chart Workbook
type: docs
weight: 70
url: /java/chart-workbook/
---


## **Chart Workbook**
### **Set Chart Data from Workbook**
A new property has been added to set chart data from workbook. Now Aspose.Slides does allow [readWorkbookStream()](https://apireference.aspose.com/slides/java/com.aspose.slides/IChartData#readWorkbookStream--) and [wrtiteWorkbookStream()](https://apireference.aspose.com/slides/java/com.aspose.slides/IChartData#writeWorkbookStream-byte:A-) methods to read and write chart data workbooks containing chart data edited using Aspose.Cells. However, the chart data needs to be organized in same way or of similar type as of source type. Below sample example is given.

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->Pie, 50, 50, 500, 400);
    $chart->getChartData()->getChartDataWorkbook()->clear(0);

    $workbook = new Java("com.aspose.slides.Workbook", "a1.xlsx");

    $mem = new Java("java.io.ByteArrayOutputStream");
    $workbook->save($mem, Java("com.aspose.cells.SaveFormat")->XLSX);

    $chart->getChartData()->writeWorkbookStream($mem->toByteArray());

    $chart->getChartData()->setRange("Sheet1!$A$1:$B$9");
    $series = $chart->getChartData()->getSeries()->get_Item(0);
    $series->getParentSeriesGroup()->setColorVaried(true);
    $pres->save("response2.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} catch (JavaException $ex) {
} finally {
    if ($pres != null) $pres->dispose();
}
```

### **Set WorkBook Cell as Chart DataLabel**
Aspose.Slides for Java provides a simple API for getting value from WorkBook Cell used as DataLabel:

1. Create an instance of the [Presentation](http://www.aspose.com/api/java/slides/com.aspose.slides/classes/Presentation) class.
1. Obtain a slide's reference by its index.
1. Add a chart with default data along with the Bubble type.
1. Accessing the chart series.
1. Setting Workbook cell as data label.
1. Save the presentation to a PPTX file.

```php
// Create an instance of Presentation class
$pres = new Java("com.aspose.slides.Presentation", "chart.pptx");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->Bubble, 50, 50, 600, 400, true);

    $series = $chart->getChartData()->getSeries()->get_Item(0);

    $series->getLabels()->getDefaultDataLabelFormat()->setShowLabelValueFromCell(true);

    $wb = $chart->getChartData()->getChartDataWorkbook();

    $series->getLabels()->get_Item(0)->setValueFromCell($wb->getCell(0, "A10", "Label 0 cell value"));
    $series->getLabels()->get_Item(1)->setValueFromCell($wb->getCell(0, "A11", "Label 1 cell value"));
    $series->getLabels()->get_Item(2)->setValueFromCell($wb->getCell(0, "A12", "Label 2 cell value"));

    $pres->save("resultchart.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

### **Get Chart External Data Source Workbook Path**
Aspose.Slides for Java provides a simple API for getting value from WorkBook Cell used as DataLabel:

1. Create an instance of the [Presentation](http://www.aspose.com/api/java/slides/com.aspose.slides/classes/Presentation) class.
1. Obtain a slide's reference by its index.
1. Create object for chart shape
1. Create object for source type of ChartDataSourceType which represents data source of the chart.
1. If Source Type is equal to external workbook the get chart external data source workbook path.

```php
// Create an instance of Presentation class
$pres = new Java("com.aspose.slides.Presentation", "chart.pptx");
try {
    $slide = $pres->getSlides()->get_Item(1);
    $chart = $slide->getShapes()->get_Item(0);
    $sourceType = $chart->getChartData()->getDataSourceType();
    
    if ($sourceType == Java("com.aspose.slides.DataSourceType")->ExternalWorkbook)
    {
        $path = $chart->getChartData()->getExternalWorkbookPath();
    }
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **External Workbook**
{{% alert color="primary" %}} 
Aspose.Slides for Java for 19.4 supports external workbooks as a data source for charts.
{{% /alert %}} 

### **Create External Workbook**
This article demonstrates how to create an external workbook from scratch using Aspose.Slides for Java. [**IChartData->readWorkbookStream()**](https://apireference.aspose.com/slides/java/com.aspose.slides/IChartData#readWorkbookStream--) and [**IChartData->setExternalWorkbook()**](https://apireference.aspose.com/slides/java/com.aspose.slides/IChartData#setExternalWorkbook-java.lang.String-) methods can be used to create an external workbook from scratch or to make an internal workbook external.

The implementation is demonstrated below in an example.

```php
// Create an instance of Presentation class
$pres = new Java("com.aspose.slides.Presentation", "chart.pptx");
try {
    $externalWbPath = $dataPath . "externalWorkbook1.xlsx";
    
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->Pie, 50, 50, 400, 600);

    java.io.File file = new File($externalWbPath);
    if ($file.exists())
        $file.delete();

    $worbookData = $chart->getChartData()->readWorkbookStream();
    $outputStream = new Java("java.io.FileOutputStream", $file);
    $outputStream->write($worbookData);
    $outputStream->close();

    $chart->getChartData()->setExternalWorkbook($externalWbPath);

    $pres->save("output.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} catch (JavaException $e) {
} finally {
    if ($pres != null) $pres->dispose();
}
```

### **Set External Workbook**
Using Aspose.Slides for Java, an external workbook can be assigned to a chart as a data source. For this purpose [**IChartData.SetExternalWorkbook**](https://apireference.aspose.com/slides/java/com.aspose.slides/IChartData#setExternalWorkbook-java.lang.String-) method has been added.

The method [**setExternalWorkbook()**](https://apireference.aspose.com/slides/java/com.aspose.slides/IChartData#setExternalWorkbook-java.lang.String-) can be also used to update a path to the external workbook if it has been moved. Workbooks placed on remote resources unavailable for data editing but still can be assigned as an external data source. If the relative path was provided for an external workbook, it converts to full path automatically.

The implementation is demonstrated below in an example.

```php
// Create an instance of Presentation class
$pres = new Java("com.aspose.slides.Presentation", "chart.pptx");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->Pie, 50, 50, 400, 600, false);
    $chartData = $chart->getChartData();

    $chartData->setExternalWorkbook($dataPath . "externalWorkbook.xlsx");

    $chartData->getSeries()->add($chartData->getChartDataWorkbook()->getCell(0, "B1"), Java("com.aspose.slides.ChartType")->Pie);
    $chartData->getSeries()->get_Item(0)->getDataPoints()->addDataPointForPieSeries($chartData->getChartDataWorkbook()->getCell(0, "B2"));
    $chartData->getSeries()->get_Item(0)->getDataPoints()->addDataPointForPieSeries($chartData->getChartDataWorkbook()->getCell(0, "B3"));
    $chartData->getSeries()->get_Item(0)->getDataPoints()->addDataPointForPieSeries($chartData->getChartDataWorkbook()->getCell(0, "B4"));

    $chartData->getCategories()->add($chartData->getChartDataWorkbook()->getCell(0, "A2"));
    $chartData->getCategories()->add($chartData->getChartDataWorkbook()->getCell(0, "A3"));
    $chartData->getCategories()->add($chartData->getChartDataWorkbook()->getCell(0, "A4"));
    
    $pres->save("Presentation_with_externalWorkbook.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

The [**setExternalWorkbook(System workbookPath, boolean updateChartData)**](https://apireference.aspose.com/slides/java/com.aspose.slides/IChartData#setExternalWorkbook-java.lang.String-boolean-) method has been added with **updateChartData** parameter to the [**IChartData**](https://apireference.aspose.com/slides/java/com.aspose.slides/IChartData) interface and [**ChartData**](https://apireference.aspose.com/slides/java/com.aspose.slides/ChartData) class.

The **updateChartData** parameter defines whether an excel workbook will be loaded or not. If the value is ***false*** only the workbook path will be updated. Chart data will not be loaded and updated from the target workbook. This is useful when the target workbook does not yet exist or is not available. If the value is **true** chart data will be updated from the target workbook as the [**setExternalWorkbook(String)**](https://apireference.aspose.com/slides/java/com.aspose.slides/IChartData#setExternalWorkbook-java.lang.String-) method does.

```php
// Create an instance of Presentation class
$pres = new Java("com.aspose.slides.Presentation", "chart.pptx");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->Pie, 50, 50, 400, 600, true);
    $chartData = $chart->getChartData();

    $chartData->setExternalWorkbook("http://path/doesnt/exists", false);

    $pres->save("Presentation_with_externalWorkbookWithUpdateChartData.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

### **Edit Chart Data**
Using Aspose.Slides for Java, Chart data in external workbooks can be edited the same way it works for internal workbooks. If external workbook cannot be loaded an exception is thrown.

The implementation is demonstrated below in an example.

```php
// Create an instance of Presentation class
$pres = new Java("com.aspose.slides.Presentation", "chart.pptx");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->get_Item(0);
    $chartData = $chart->getChartData();
    
    $chartData->getSeries()->get_Item(0)->getDataPoints()->get_Item(0)->getValue()->getAsCell()->setValue(100);
    
    $pres->save("presentation_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```