---
title: Chart Axis
type: docs
url: /java/chart-axis/
---

## **Get Actual Max Value of Vertical Axis on Chart**
Aspose.Slides for Java provides a simple API for getting value of vertical axis. 

1. Create an instance of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Access first slide.
1. Add chart with default data.
1. Get actual maximum value on the axis.
1. Get actual minimum value on the axis.
1. Get actual major unit of the axis.
1. Get actual minor unit of the axis.
1. Get actual major unit scale of the axis.
1. Get actual minor unit scale of the axis.

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

## **Switch Data Over Axis**
A new property has been added which Swap the data over the axis. Data being charted on the X axis will move to the Y axis and vice versa. Below sample example is given.

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->ClusteredColumn, 100, 100, 400, 300);

    //Switching rows and columns
    $chart->getChartData()->switchRowColumn();

    // Saving presentation
    $pres->save("SwitchChartRowColumns_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Change Category Axis**
**CategoryAxisType** can be changed to [Date](https://apireference.aspose.com/slides/java/com.aspose.slides/CategoryAxisType#Date) or [Text](https://apireference.aspose.com/slides/java/com.aspose.slides/CategoryAxisType#Text). However, **CategoryAxisType.Auto** is not supported at the moment. New methods [**getCategoryAxisType**](https://apireference.aspose.com/slides/java/com.aspose.slides/IAxis#getCategoryAxisType--) and [**setCategoryAxisType**](https://apireference.aspose.com/slides/java/com.aspose.slides/IAxis#setCategoryAxisType-int-) have been added to [**IAxis**](https://apireference.aspose.com/slides/java/com.aspose.slides/IAxis) interface and [Axis](https://apireference.aspose.com/slides/java/com.aspose.slides/Axis) class which specifies type of category axis.

```php
$pres = new Java("com.aspose.slides.Presentation", "ExistingChart.pptx");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->get_Item(0);
    
    $chart->getAxes()->getHorizontalAxis()->setCategoryAxisType(Java("com.aspose.slides.CategoryAxisType")->Date);
    $chart->getAxes()->getHorizontalAxis()->setAutomaticMajorUnit(false);
    $chart->getAxes()->getHorizontalAxis()->setMajorUnit(1);
    $chart->getAxes()->getHorizontalAxis()->setMajorUnitScale(Java("com.aspose.slides.TimeUnitType")->Months);
    
    $pres->save("ChangeChartCategoryAxis_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Set Date Format for Category Axis Value**
Aspose.Slides for Java provides a simple API for setting date format for category axis value. Below sample example is given. 

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->Area, 50, 50, 450, 300);

    $wb = $chart->getChartData()->getChartDataWorkbook();
    $wb->clear(0);

    $chart->getChartData()->getCategories()->clear();
    $chart->getChartData()->getSeries()->clear();
    $chart->getChartData()->getCategories()->add($wb->getCell(0, "A2", convertToOADate(new Java("java.util.GregorianCalendar", 2015, 1, 1))));
    $chart->getChartData()->getCategories()->add($wb->getCell(0, "A3", convertToOADate(new Java("java.util.GregorianCalendar", 2016, 1, 1))));
    $chart->getChartData()->getCategories()->add($wb->getCell(0, "A4", convertToOADate(new Java("java.util.GregorianCalendar", 2017, 1, 1))));
    $chart->getChartData()->getCategories()->add($wb->getCell(0, "A5", convertToOADate(new Java("java.util.GregorianCalendar", 2018, 1, 1))));

    $series = $chart->getChartData()->getSeries()->add(Java("com.aspose.slides.ChartType")->Line);
    $series->getDataPoints()->addDataPointForLineSeries($wb->getCell(0, "B2", 1));
    $series->getDataPoints()->addDataPointForLineSeries($wb->getCell(0, "B3", 2));
    $series->getDataPoints()->addDataPointForLineSeries($wb->getCell(0, "B4", 3));
    $series->getDataPoints()->addDataPointForLineSeries($wb->getCell(0, "B5", 4));
    $chart->getAxes()->getHorizontalAxis()->setCategoryAxisType(Java("com.aspose.slides.CategoryAxisType")->Date);
    $chart->getAxes()->getHorizontalAxis()->setNumberFormatLinkedToSource(false);
    $chart->getAxes()->getHorizontalAxis()->setNumberFormat("yyyy");
	
    $pres->save("output.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```
```php
public static String convertToOADate(GregorianCalendar date) throws ParseException
{
    $oaDate;
    $myFormat = new SimpleDateFormat("dd MM yyyy");
    $baseDate = $myFormat.parse("30 12 1899");
    $days = TimeUnit.DAYS.convert($date->getTimeInMillis() - $baseDate->getTime(), TimeUnit.MILLISECONDS);
    $oaDate = $days + ($date->get(Calendar.HOUR_OF_DAY) / 24) + ($date->get(Calendar.MINUTE) / (60 * 24)) + ($date->get(Calendar.SECOND) / (60 * 24 * 60));
    return String.valueOf($oaDate);
}
```

## **Set Rotation Angle for Chart Axis Title**
Aspose.Slides for Java provides a simple API for setting rotation angle for chart axis title. Below sample example is given. 

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->ClusteredColumn, 50, 50, 450, 300);
    
    $chart->getAxes()->getVerticalAxis()->setTitle(true);
    $chart->getAxes()->getVerticalAxis()->getTitle()->getTextFormat()->getTextBlockFormat()->setRotationAngle(90);

    $pres->save("output.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}

```

## **Set Position Axis in Category or Value Axis**
Aspose.Slides for Java provides a simple API for setting Position axis in category or Value axis. Below sample example is given. 

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->ClusteredColumn, 50, 50, 450, 300);
    
    $chart->getAxes()->getHorizontalAxis()->setAxisBetweenCategories(true);

    $pres->save("output.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Show Display Unit label on Chart Value Axis**
Aspose.Slides for Java provides support for showing Display unit label on chart value axis. Below sample example is given. 

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $chart = $pres->getSlides()->get_Item(0)->getShapes()->addChart(Java("com.aspose.slides.ChartType")->ClusteredColumn, 50, 50, 450, 300);

    $chart->getAxes()->getVerticalAxis()->setDisplayUnit(Java("com.aspose.slides.DisplayUnitType")->Millions);
    
    $pres->save("output.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```
