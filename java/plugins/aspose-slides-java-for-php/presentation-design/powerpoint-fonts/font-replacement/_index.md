---
title: Font Replacement
type: docs
weight: 60
url: /java/font-replacement/
---

## **Replacing Fonts Explicitly**
To replace the fonts using explicit replacement following steps are used:

- Load the desired presentation.
- Load the font that is to replace inside the presentation.
- Load the replacing font.
- Replace the fonts.
- Write the modified presentation as a PPTX file.

The implementation of the above steps is given below.

```php
// Load presentation
$pres = new Java("com.aspose.slides.Presentation", "Fonts.pptx");
try {
    // Load source font to be replaced
    IFontData sourceFont = new  Java("com.aspose.slides.FontData"), "Arial");
    
    // Load the replacing font
    IFontData destFont = new  Java("com.aspose.slides.FontData"), "Times New Roman");
    
    // Replace the fonts
    $pres->getFontsManager().replaceFont(sourceFont, destFont);
    
    // Save the presentation
    $pres->save("UpdatedFont_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```
