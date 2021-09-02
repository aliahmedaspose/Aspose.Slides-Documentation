---
title: Font Substitution
type: docs
weight: 70
url: /java/font-substitution/
---


## **Rule Based Font Substitution**
To replace the fonts by setting some rules of replacement following steps are used:

- Load the desired presentation.
- Load the font that is to replaced inside the presentation.
- Load the replacing font.
- Add rule for replacement.
- Add the rule to presentation font replacement rule collection.
- Generate the slide image to observe the effect.

The implementation of the above steps is given below.

```php
// Load presentation
$pres = new Java("com.aspose.slides.Presentation", "Fonts.pptx");
try {
    // Load source font to be replaced
    $sourceFont = new  Java("com.aspose.slides.FontData", "SomeRareFont");
    
    // Load the replacing font
    $destFont = new  Java("com.aspose.slides.FontData", "Arial");
    
    // Add font rule for font replacement
    IFontSubstRule fontSubstRule = new FontSubstRule(sourceFont, destFont, FontSubstCondition.WhenInaccessible);
    
    // Add rule to font substitute rules collection
    IFontSubstRuleCollection fontSubstRuleCollection = new FontSubstRuleCollection();
    fontSubstRuleCollection->add(fontSubstRule);
    
    // Add font rule collection to rule list
    $pres->getFontsManager()->setFontSubstRuleList(fontSubstRuleCollection);
    
    // Arial font will be used instead of SomeRareFont when inaccessible
    $image = $pres->getSlides()->get_Item(0)->getThumbnail(1, 1);
    
    // Save the image to disk in JPEG format
    Java("javax.imageio.ImageIO")->write($image, "PNG", new Java("java.io.File", "Thumbnail_out.jpg"));
} catch (JavaException $e) {
} finally {
    if ($pres != null) $pres->dispose();
}
```

