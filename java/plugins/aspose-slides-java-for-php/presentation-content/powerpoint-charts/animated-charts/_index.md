---
title: Animated Charts
type: docs
weight: 80
url: /java/animated-charts/
---


{{% alert color="primary" %}} 

Aspose.Slides for Java supports animating the chart elements. **Series**, **Categories**, **Series Elements**, **Categories Elements** can be animated with [**ISequence**.**addEffect**](https://apireference.aspose.com/slides/java/com.aspose.slides/ISequence#addEffect-com.aspose.slides.IChart-int-int-int-int-int-) method and two enums [**EffectChartMajorGroupingType**](https://apireference.aspose.com/slides/java/com.aspose.slides/EffectChartMajorGroupingType) and [**EffectChartMinorGroupingType**](https://apireference.aspose.com/slides/java/com.aspose.slides/EffectChartMinorGroupingType).

{{% /alert %}} 

## **Chart Series Animation**
If you want to animate a chart series, write the code according to the steps listed below:

1. Load a presentation.
1. Get reference of the chart object.
1. Animate the series.
1. Write the presentation file to disk.

In the example given below, we animated chart series.

```php
// Instantiate Presentation class that represents a presentation file
$pres = new Java("com.aspose.slides.Presentation", "ExistingChart.pptx");
try {
    // Get reference of the chart object
    $slide = $pres->getSlides()->get_Item(0);
    $shapes = $slide->getShapes();
    $chart = $shapes->get_Item(0);

    // Animate the series
    $slide->getTimeline()->getMainSequence()->addEffect($chart, Java("com.aspose.slides.EffectType")->Fade, Java("com.aspose.slides.EffectSubtype")->None,
            Java("com.aspose.slides.EffectSubtype")->AfterPrevious);

    $slide->getTimeline()->getMainSequence())->addEffect($chart,
            Java("com.aspose.slides.EffectChartMajorGroupingType")->BySeries, 0,
            Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);

    $slide->getTimeline()->getMainSequence())->addEffect($chart,
            Java("com.aspose.slides.EffectChartMajorGroupingType")->BySeries, 1,
            Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);

    $slide->getTimeline()->getMainSequence())->addEffect($chart,
            Java("com.aspose.slides.EffectChartMajorGroupingType")->BySeries, 2,
            Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);

    $slide->getTimeline()->getMainSequence())->addEffect($chart,
            Java("com.aspose.slides.EffectChartMajorGroupingType")->BySeries, 3,
            Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);

    // Write the modified presentation to disk
    $pres->save("AnimatingSeries_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Chart Category Animation**
If you want to animate a chart series, write the code according to the steps listed below:

1. Load a presentation.
1. Get reference of the chart object.
1. Animate the Category.
1. Write the presentation file to disk.

In the example given below, we animated chart category.

```php
// Instantiate Presentation class that represents a presentation file
$pres = new Java("com.aspose.slides.Presentation", "ExistingChart.pptx");
try {
    $slide = $pres->getSlides()->get_Item(0);
    $shapes = $slide->getShapes();
    $chart = $shapes->get_Item(0);

    $slide->getTimeline()->getMainSequence()->addEffect($chart, Java("com.aspose.slides.EffectType")->Fade, Java("com.aspose.slides.EffectSubtype")->None,
            Java("com.aspose.slides.EffectSubtype")->AfterPrevious);

    $slide->getTimeline()->getMainSequence())->addEffect($chart,
            Java("com.aspose.slides.EffectChartMajorGroupingType")->ByCategory, 0, 
            Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    
    $slide->getTimeline()->getMainSequence())->addEffect($chart, 
            Java("com.aspose.slides.EffectChartMajorGroupingType")->ByCategory, 1, 
            Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    
    $slide->getTimeline()->getMainSequence())->addEffect($chart, 
            Java("com.aspose.slides.EffectChartMajorGroupingType")->ByCategory, 2, 
            Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    
    $slide->getTimeline()->getMainSequence())->addEffect($chart, 
            Java("com.aspose.slides.EffectChartMajorGroupingType")->ByCategory, 3, 
            Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);

    $pres->save("Sample_Animation_C.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Animation in Series Element**
If you want to animate series elements, write the code according to the steps listed below:

1. Load a presentation.
1. Get reference of the chart object.
1. Animate series elements.
1. Write the presentation file to disk.

In the example given below, we have animated series' elements.

```php
// Instantiate Presentation class that represents a presentation file
$pres = new Java("com.aspose.slides.Presentation", "ExistingChart.pptx");
try {
    // Get reference of the chart object
    $slide = $pres->getSlides()->get_Item(0);
    $shapes = $slide->getShapes();
    $chart = $shapes->get_Item(0);

    // Animate series elements
    $slide->getTimeline()->getMainSequence()->addEffect($chart, Java("com.aspose.slides.EffectType")->Fade, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);

    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInSeries, 
            0, 0, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInSeries, 
            0, 1, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInSeries, 
            0, 2, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInSeries, 
            0, 3, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);

    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInSeries, 
            1, 0, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInSeries, 
            1, 1, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInSeries, 
            1, 2, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInSeries, 
            1, 3, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);

    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInSeries, 
            2, 0, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInSeries, 
            2, 1, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInSeries, 
            2, 2, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInSeries, 
            2, 3, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);

    // Write the presentation file to disk 
    $pres->save("AnimatingSeriesElements_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Animation in Category Element**
If you want to animate categories elements, write the code according to the steps listed below:

1. Load a presentation.
1. Get reference of the chart object.
1. Animate categories elements.
1. Write the presentation file to disk.

In the example given below, we have animated categories elements.

```php
// Instantiate Presentation class that represents a presentation file
$pres = new Java("com.aspose.slides.Presentation", "ExistingChart.pptx");
try {
    // Get reference of the chart object
    $slide = $pres->getSlides()->get_Item(0);
    $shapes = $slide->getShapes();
    $chart = $shapes->get_Item(0);

    // Animate categories' elements
    $slide->getTimeline()->getMainSequence()->addEffect($chart, Java("com.aspose.slides.EffectType")->Fade, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInCategory, 
            0, 0, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInCategory, 
            0, 1, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInCategory, 
            0, 2, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInCategory, 
            0, 3, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);

    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInCategory, 
            1, 0, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInCategory, 
            1, 1, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInCategory, 
            1, 2, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInCategory, 
            1, 3, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);

    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInCategory, 
            2, 0, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInCategory, 
            2, 1, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInCategory, 
            2, 2, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);
    $slide->getTimeline()->getMainSequence())->addEffect($chart, Java("com.aspose.slides.EffectChartMinorGroupingType")->ByElementInCategory, 
            2, 3, Java("com.aspose.slides.EffectType")->Appear, Java("com.aspose.slides.EffectSubtype")->None, Java("com.aspose.slides.EffectSubtype")->AfterPrevious);

    // Write the presentation file to disk
    $pres->save("AnimatingCategoriesElements_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```