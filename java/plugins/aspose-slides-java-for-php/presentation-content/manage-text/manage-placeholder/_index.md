---
title: Manage Placeholder
type: docs
weight: 10
url: /java/manage-placeholder/
---

## **Change Text in a Placeholder**
Using [Aspose.Slides for Java](/slides/java/), developers can also find and modify a specific Placeholder present in a slide. In this topic, we are going to demonstrate with the help of an example that how the text contained inside a Placeholder can be replaced or modified using Aspose.Slides for Java. The following two steps will be used to modify text in Placeholder.

Step 1: Create a Slide Containing a Placeholder

First of all, create a presentation file with a slide containing a Placeholder. You can create this presentation either MS PowerPoint. This is just the demonstration of replacing text in a Placeholder, so, you can create this presentation by yourself. This presentation will be used in the next step and the text in its Placeholder will be replaced.

Step 2: Replace Text of the Placeholder

To replace the text of a Placeholder, please follow the steps below:

- Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
- Obtain the reference of a slide by using its Index.
- Iterate through the Shapes and find the Placeholder shapes.
- Typecast the Placeholder shape to [AutoShape](https://apireference.aspose.com/slides/java/com.aspose.slides/AutoShape) and change the text using the [TextFrame](https://apireference.aspose.com/slides/java/com.aspose.slides/TextFrame) associated with [AutoShape](https://apireference.aspose.com/slides/java/com.aspose.slides/IAutoShape).
- Write the modified presentation as a PPTX file.

```php
// Instantiate Presentation class that represents PPTX
$pres = new Java("com.aspose.slides.Presentation", "ReplacingText.pptx");
try {

    // Access first slide
    $sld = $pres->getSlides()->get_Item(0);

    // Iterate through shapes to find the placeholder
    forech( $sld->getShapes() as $shp ) 
    {
        if ($shp->getPlaceholder() != null) {
            // Change the text of each placeholder
            $shp->getTextFrame()->setText("This is Placeholder");
        }
    }

    // Save the PPTX to Disk
    $pres->save("output_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Set Prompt Text in a Placeholder**
As we know that Standard and pre-built layouts contain placeholders with default text like **Click to add a title** or **Click to add subtitle**. Using Aspose.Slides you can add prompt text manually by accessing the default placeholders.

The code snippet below shows how to use this feature:

```php
$pres = new Java("com.aspose.slides.Presentation", "Presentation.pptx");
try {
    $slide = $pres->getSlides()->get_Item(0);
    forech( $slide->getSlide()->getShapes() as $shape ) // iterate through the slide
    {
        if ($shape->getPlaceholder() != null && shape instanceof AutoShape)
        {
            $text = "";
            if ($shape->getPlaceholder()->getType() == Java("com.aspose.slides.PlaceholderType")->CenteredTitle) //PowerPoint displays "Click to add title". 
            {
                $text = "Add Title";
            }
            else if ($shape->getPlaceholder()->getType() == Java("com.aspose.slides.PlaceholderType")->Subtitle) //add subtitle.
            {
                $text = "Add Subtitle";
            }

            $shape->getTextFrame()->setText($text);
            echo("Placeholder with text: " + text);
        }
    }

    $pres->save("Placeholders_PromptText.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```
