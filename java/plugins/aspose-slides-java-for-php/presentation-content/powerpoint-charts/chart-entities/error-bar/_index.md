---
title: Error Bar
type: docs
url: /java/error-bar/
---

## **Add Error Bar**
Aspose.Slides for Java provides a simple API for managing error bar values. The sample code applies when using a custom value type. To specify a value, use the **ErrorBarCustomValues** property of a specific data point in the [**DataPoints**](https://apireference.aspose.com/slides/java/com.aspose.slides/IChartSeriesCollection) collection of series:

1. Create an instance of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Add a bubble chart on desired slide.
1. Access the first chart series and set the error bar X format.
1. Access the first chart series and set the error bar Y format.
1. Setting bars values and format.
1. Write the modified presentation to a PPTX file.

```php
// Create an instance of Presentation class
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Creating a bubble chart
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->Bubble, 50, 50, 400, 300, true);

    // Adding Error bars and setting its format
    $errBarX = $chart->getChartData()->getSeries()->get_Item(0)->getErrorBarsXFormat();
    $errBarY = $chart->getChartData()->getSeries()->get_Item(0)->getErrorBarsYFormat();

    $errBarX->isVisible();
    $errBarY->isVisible();
    $errBarX->setValueType((new Java("java.lang.Integer", Java("com.aspose.slides.ErrorBarValueType")->Fixed))->byteValue());
    $errBarX->setValue(0.1);
    $errBarY->setValueType((new Java("java.lang.Integer", Java("com.aspose.slides.ErrorBarValueType")->Percentage))->byteValue());
    $errBarY->setValue(5);
    $errBarX->setType((new Java("java.lang.Integer", Java("com.aspose.slides.ErrorBarType")->Plus))->byteValue());
    $errBarY->getFormat()->getLine()->setWidth(2.0);
    errBarX.hasEndCap();

    // Saving presentation
    $pres->save("ErrorBars.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Add Custom Error Bar Value**
Aspose.Slides for Java provides a simple API for managing custom error bar values. The sample code applies when the [**IErrorBarsFormat.ValueType**](https://apireference.aspose.com/slides/java/com.aspose.slides/IErrorBarsFormat#getValue--) property is equal to **Custom**. To specify a value, use the **ErrorBarCustomValues** property of a specific data point in the [**DataPoints**](https://apireference.aspose.com/slides/java/com.aspose.slides/IChartSeriesCollection) collection of series:

1. Create an instance of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Add a bubble chart on desired slide.
1. Access the first chart series and set the error bar X format.
1. Access the first chart series and set the error bar Y format.
1. Access the chart series individual data points and setting the Error Bar values for individual series data point.
1. Setting bars values and format.
1. Write the modified presentation to a PPTX file.

```php
// Create an instance of Presentation class
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Creating a bubble chart
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->Bubble, 50, 50, 400, 300, true);

    // Adding custom Error bars and setting its format
    $series = $chart->getChartData()->getSeries()->get_Item(0);
    $errBarX = $series->getErrorBarsXFormat();
    $errBarY = $series->getErrorBarsYFormat();
    $errBarX->isVisible();
    $errBarY->isVisible();
    $errBarX->setValueType((new Java("java.lang.Integer", Java("com.aspose.slides.ErrorBarValueType")->Custom))->byteValue());
    $errBarY->setValueType((new Java("java.lang.Integer", Java("com.aspose.slides.ErrorBarValueType")->Custom))->byteValue());

    // Accessing chart series data point and setting error bars values for
    // individual point
    $points = $series->getDataPoints();
    $points->getDataSourceTypeForErrorBarsCustomValues()->setDataSourceTypeForXPlusValues((new Java("java.lang.Integer", Java("com.aspose.slides.DataSourceType")->DoubleLiterals))->byteValue());
    $points->getDataSourceTypeForErrorBarsCustomValues()->setDataSourceTypeForXMinusValues((new Java("java.lang.Integer", Java("com.aspose.slides.DataSourceType")->DoubleLiterals))->byteValue());
    $points->getDataSourceTypeForErrorBarsCustomValues()->setDataSourceTypeForYPlusValues((new Java("java.lang.Integer", Java("com.aspose.slides.DataSourceType")->DoubleLiterals))->byteValue());
    $points->getDataSourceTypeForErrorBarsCustomValues()->setDataSourceTypeForYMinusValues((new Java("java.lang.Integer", Java("com.aspose.slides.DataSourceType")->DoubleLiterals))->byteValue());

    // Setting error bars for chart series points
    for ($i = 0; $i < $points->size(); $i++) {
        $points->get_Item($i)->getErrorBarsCustomValues()->getXMinus()->setAsLiteralDouble($i+ 1);
        $points->get_Item($i)->getErrorBarsCustomValues()->getXPlus()->setAsLiteralDouble($i+ 1);
        $points->get_Item($i)->getErrorBarsCustomValues()->getYMinus()->setAsLiteralDouble($i+ 1);
        $points->get_Item($i)->getErrorBarsCustomValues()->getYPlus()->setAsLiteralDouble($i+ 1);
    }

    // Saving presentation
    $pres->save("ErrorBarsCustomValues.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```