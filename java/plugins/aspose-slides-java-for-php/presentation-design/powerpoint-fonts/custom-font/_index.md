---
title: Custom Font
type: docs
weight: 20
url: /java/custom-font/
---

{{% alert color="primary" %}} 

Aspose.Slides let you load fonts for rendering in presentations without even installing them. This article shows how to load fonts from custom directories without installing them.

{{% /alert %}}

## **Load Custom Fonts from .TTF**
Please follow the steps below to loading Fonts from external directories by using Aspose.Slides for Java API:

- Create an instance of [FontsLoader](https://apireference.aspose.com/slides/java/com.aspose.slides/FontsLoader) class and call the static method [loadExternalFonts](https://apireference.aspose.com/slides/java/com.aspose.slides/FontsLoader#loadExternalFonts-java.lang.String:A-).
- Perform render the presentation.
- [Clear the cache](https://apireference.aspose.com/slides/java/com.aspose.slides/FontsLoader#clearCache--) in the [FontsLoader](https://apireference.aspose.com/slides/java/com.aspose.slides/FontsLoader) class.

The implementation of the above is given below.

```php
// folders to seek fonts
$Array = new JavaClass("java.lang.reflect.Array");
$String = new JavaClass("java.lang.String");
$folders = $Array->newInstance($String, 1);
$folders[0] = $externalFontsDir;

// Load the custom font directory fonts
Java("com.aspose.slides.FontsLoader")->loadExternalFonts($folders);

// Do Some work and perform presentation/slides rendering
$pres = new Java("com.aspose.slides.Presentation", "DefaultFonts.pptx");
try {
    $pres->save("NewFonts_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();

    // Clear Font Cachce
    Java("com.aspose.slides.FontsLoader")->clearCache();
}
```

## **Get Custom Fonts Folder**
A new method has been added that returns folders where font files are searched. Those are folders that have been added with [loadExternalFonts](https://apireference.aspose.com/slides/java/com.aspose.slides/FontsLoader#loadExternalFonts-java.lang.String:A-) method as well as system font folders.

```php
//The following line shall return folders where font files are searched.
//Those are folders that have been added with LoadExternalFonts method as well as system font folders.
$fontFolders = Java("com.aspose.slides.FontsLoader")->getFontFolders();
```

## **Specify Custom Fonts Used With Presentation**
A new [getDocumentLevelFontSources](https://apireference.aspose.com/slides/java/com.aspose.slides/ILoadOptions#getDocumentLevelFontSources--) method has been added to [ILoadOptions](https://apireference.aspose.com/slides/java/com.aspose.slides/ILoadOptions) interface. It allows to specify external fonts that are used with the presentation.

```php
$Byte = new JavaClass("java.lang.Byte");
$Array = new JavaClass("java.lang.reflect.Array");

$file1 = new Java("java.io.File", "customfonts/CustomFont1.ttf");
$fis1 = new Java("java.io.FileInputStream", $file1);
try {
	$memoryFont1 = $Array->newInstance($Byte, $file1->length());
	$fis1->read($memoryFont1);
} catch (JavaException $e) { }
finally {
    if ($fis1 != null) $fis1->close();
}

$file2 = new Java("java.io.File", "customfonts/CustomFont2.ttf");
$fis2 = new Java("java.io.FileInputStream", $file2);
try {
	$memoryFont2 = $Array->newInstance($Byte, $file2->length());
	$fis2->read($memoryFont2);
} catch (JavaException $e) { }
finally {
    if ($fis2 != null) $fis2->close();
}

$loadOptions = new Java("com.aspose.slides.LoadOptions");

$String = new JavaClass("java.lang.String");
$folders = $Array->newInstance($String, 2);
$folders[0] = "assets/fonts";
$folders[1] = "global/fonts";

$loadOptions->getDocumentLevelFontSources()->setFontFolders($folders);

$memoryFonts = $Array->newInstance($Array, 2);
$memoryFont[0] = $memoryFont1;
$memoryFont[1] = $memoryFont2;

$loadOptions->getDocumentLevelFontSources()->setMemoryFonts($memoryFonts);

$pres = new Java("com.aspose.slides.Presentation", "MyPresentation.pptx", $loadOptions);
try {
    //work with the presentation
    //CustomFont1, CustomFont2 as well as fonts from assets\fonts & global\fonts folders and their subfolders are available to the presentation
} finally {
    if ($pres != null) $pres->dispose();
}
```



