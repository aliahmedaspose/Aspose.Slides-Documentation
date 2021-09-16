---
title: Convert Powerpoint PPT(X) to HTML
type: docs
weight: 30
url: /java/convert-powerpoint-ppt-and-pptx-to-html/
keywords: "convert pptx to html, ppt to html, powerpoint to html, save pptx as html"
description: "Convert PowerPoint to HTML of any format: PPTX to HTML, PPT to HTML. Save PPTX to HTML and use PowerPoint HTML export."
---

## **About PowerPoint to HTML Conversion**
[**Aspose.Slides for Java**](https://products.aspose.com/slides/java) provides support for converting a PowerPoint presentation to HTML. With Aspose.Slides API you may set up the conversion process to enhance the resulting HTML. Both PPT to HTML and PPTX to HTML conversions are available.

There are many ways to convert PPT(X) to HTML. You could use PowerPoint native tools or online web tools to do that, however, they will cover only the basic scenarios to convert PPT(X) to HTML. If you need to built-in an HTML result to your website or integrate it into an enterprise-level solution - you would rather need to have more flexibility in PPT(X) to HTML conversion.

With Aspose.Slides API you may set up the conversion process to enhance the resulting HTML. It is possible to create your own PPT to HTML or PPTX to HTML converter, and integrate it into any desktop or web software.

Here are just some possibilities to set up PPT(X) to HTML conversion with Aspose.Slides:

1. Convert the whole PowerPoint presentation to HTML.
1. Convert a separate presentation slide to HTML. Choose separate slides from different presentations, combine them on the fly and convert presentation slides to one HTML file.
1. Convert presentation media (images, video, etc) to HTML.
1. Convert PowerPoint presentation to a responsive HTML. It's a powerful feature to create a responsive HTML document from the presentation, when you need the resulting HTML to be properly shown on various devices and sizes. You do not need to define all the responsive styles, the API will do that instead of you.
1. Convert PPT(X) to HTML with included or excluded speaker notes. It's possible to set the position of the notes.
1. Convert PPT(X) to HTML with included or excluded comments. It's possible to set the position of the comments, area color and width.
1. Convert PPT(X) to HTML with its original or embedded fonts. You can upload the original or embedded fonts used in presentation to make it applied in the resulting HTML.
1. Use new CSS while converting PPT(X) to HTML. You can change the styles of the resulting HTML by applying new CSS styles while converting presentation.

In Aspose.Slides PowerPoint to HTML conversion is implemented with [**Save**](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation#save-java.lang.String-int-com.aspose.slides.ISaveOptions-) method exposed by the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class. Conversion settings are not limited with the described above and are represented in [**HtmlOptions**](https://apireference.aspose.com/slides/java/com.aspose.slides/HtmlOptions) class.


{{% alert color="primary" %}} 

Aspose.Slides proposes **online demo apps** to see alive the [**PPT to HTML**](https://products.aspose.app/slides/conversion/ppt-to-html)**,** [**PPTX to HTML**](https://products.aspose.app/slides/conversion/pptx-to-html), [**ODP to HTML**](https://products.aspose.app/slides/conversion/odp-to-html) conversion features supported:

[](https://products.aspose.app/slides/conversion/ppt-to-html)

[![todo:image_alt_text](ppt-to-html.png)](https://products.aspose.app/slides/conversion/ppt-to-html)

Find other live [**Aspose.Slides Conversion**](https://products.aspose.app/slides/conversion/) examples.

{{% /alert %}} 


## **Convert Powerpoint to HTML**
Convert PPT or PPTX presentation to HTML file using Aspose.Slides. For that, save a PowerPoint presentation to HTML in two-lines:

1. Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Call [**Save**](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation#save-java.lang.String-int-com.aspose.slides.ISaveOptions-) method from it specifying the resulting file as an HTML file:

```php
// Instantiate a Presentation object that represents a presentation file
$pres = new Java("com.aspose.slides.Presentation", "Convert_HTML.pptx");
try {
    $htmlOpt = new Java("com.aspose.slides.HtmlOptions");
    $htmlOpt->getNotesCommentsLayouting()->setNotesPosition(Java("com.aspose.slides.NotesPositions")->BottomFull);
    $htmlOpt->setHtmlFormatter(Java("com.aspose.slides.HtmlFormatter")->createDocumentFormatter("", false));

    // Saving the presentation to HTML
    $pres->save("ConvertWholePresentationToHTML_out.html", Java("com.aspose.slides.SaveFormat")->Html, $htmlOpt);
} finally {
    if ($pres != null) $pres->dispose();
}

```

## **Convert Powerpoint to Responsive HTML**
Convert PPT(X) presentation to Responsive HTML, which will ensure the generated HTML will be displayed properly across all browsers and devices. [**ResponsiveHtmlController**](https://apireference.aspose.com/slides/java/com.aspose.slides/ResponsiveHtmlController) class provides the possibility to generate responsive HTML files. This controller can be used in the same manner as other HTML controllers:

```php
// Instantiate a Presentation object that represents a presentation file
$pres = new Java("com.aspose.slides.Presentation", "Convert_HTML.pptx");
try {
    $controller = new Java("com.aspose.slides.ResponsiveHtmlController");
    $htmlOptions = new Java("com.aspose.slides.HtmlOptions");
    $htmlOptions->setHtmlFormatter(Java("com.aspose.slides.HtmlFormatter")->createCustomFormatter($controller));

    // Saving the presentation to HTML
    $pres->save("ConvertPresentationToResponsiveHTML_out.html", Java("com.aspose.slides.SaveFormat")->Html, $htmlOptions);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Convert Powerpoint to HTML with Notes**
The following example shows how to convert PPT(X) presentation to HTML with the rendered speaker notes. Using the options of [**HtmlOptions**](https://apireference.aspose.com/slides/java/com.aspose.slides/HtmlOptions) class and [**INotesCommentsLayoutingOptions**](https://apireference.aspose.com/slides/java/com.aspose.slides/INotesCommentsLayoutingOptions) interface you can render speaker notes to HTML:

```php
$pres = new Java("com.aspose.slides.Presentation", "Presentation.pptx");
try {
    $opt = new Java("com.aspose.slides.HtmlOptions");
    $options = $opt->getNotesCommentsLayouting();
    $options->setNotesPosition(Java("com.aspose.slides.NotesPositions")->BottomFull);

    // Saving notes pages
    $pres->save("Output.html", Java("com.aspose.slides.SaveFormat")->Html, $opt);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Convert Powerpoint to HTML with Original Fonts**
Preserve original fonts that are used in presentation while converting PPT(X) to HTML. [**EmbedAllFontsHtmlController**](https://apireference.aspose.com/slides/java/com.aspose.slides/EmbedAllFontsHtmlController) class preserves the original fonts in generated HTML:

```php
$pres = new Java("com.aspose.slides.Presentation", "input.pptx");
try {
    // exclude default presentation fonts
    $Array = new JavaClass("java.lang.reflect.Array");
    $String = new JavaClass("java.lang.String");
    $fontNameExcludeList = $Array->newInstance($String, 2);
    $fontNameExcludeList[0] = "Calibri";
    $fontNameExcludeList[1] = "Arial";

    $embedFontsController = new Java("com.aspose.slides.EmbedAllFontsHtmlController", $fontNameExcludeList);

    $htmlOptionsEmbed = new Java("com.aspose.slides.HtmlOptions");
    $htmlOptionsEmbed->setHtmlFormatter(Java("com.aspose.slides.HtmlFormatter")->createCustomFormatter($embedFontsController));

    $pres->save("input-PFDinDisplayPro-Regular-installed.html", Java("com.aspose.slides.SaveFormat")->Html, $htmlOptionsEmbed);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Convert Slide to HTML**
Convert a separate presentation slide to HTML. Fo that use the same [**Save**](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation#save-java.lang.String-int-com.aspose.slides.ISaveOptions-) method exposed by the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class that is used to convert the whole PPT(X) presentation into a HTML document. The [**HtmlOptions**](https://apireference.aspose.com/slides/java/com.aspose.slides/HtmlOptions) class can be also used to set the additional conversion options:

```php
$pres = new Java("com.aspose.slides.Presentation", "Individual-Slide.pptx");
try {
    $htmlOptions = new Java("com.aspose.slides.HtmlOptions");
    $htmlOptions->getNotesCommentsLayouting()->setNotesPosition(Java("com.aspose.slides.NotesPositions")->BottomFull);
    $htmlOptions->setHtmlFormatter(Java("com.aspose.slides.HtmlFormatter")->createCustomFormatter(new Java("com.aspose.slides.CustomFormattingController")));
    
    $Array = new JavaClass("java.lang.reflect.Array");
    $Integer = new JavaClass("java.lang.Integer");
    
    // Saving File
    for ($i = 0; $i < $pres->getSlides()->size(); $i++)
        $pres->save("Individual Slide" . ($i+ 1) . "_out.html", $Array->newInstance($Integer, $i + 1),Java("com.aspose.slides.SaveFormat")->Html, $htmlOptions);
} finally {
    if ($pres != null) $pres->dispose();
}
```
```java
public class CustomFormattingController implements IHtmlFormattingController
{
    @Override
    public void writeDocumentStart(IHtmlGenerator generator, IPresentation presentation) { }

    @Override
    public void writeDocumentEnd(IHtmlGenerator generator, IPresentation presentation) { }

    @Override
    public void writeSlideStart(IHtmlGenerator generator, ISlide slide) 
	{
        generator.addHtml(String.format(SlideHeader, generator.getSlideIndex() + 1));
    }

    @Override
    public void writeSlideEnd(IHtmlGenerator generator, ISlide slide) 
	{
        generator.addHtml(SlideFooter);
    }

    @Override
    public void writeShapeStart(IHtmlGenerator generator, IShape shape) { }

    @Override
    public void writeShapeEnd(IHtmlGenerator generator, IShape shape) { }

    private final String SlideHeader = "<div class=\"slide\" name=\"slide\" id=\"slide%d\">";
    private final String SlideFooter = "</div>";
}
```

## **Save CSS and Images when Exporting To HTML**
Use new CSS styles file to change the resulting styles of the HTML file while PPT(X) to HTML conversion with Aspose.Slides. Please review the example below how to use overridable methods to create a custom HTML document with a link to CSS file:

```php
$pres = new Java("com.aspose.slides.Presentation", "pres.pptx");
try {
    $htmlController = new Java("com.aspose.slides.CustomHeaderAndFontsController", "styles.css");
    $options = new Java("com.aspose.slides.HtmlOptions");
    $options->setHtmlFormatter(Java("com.aspose.slides.HtmlFormatter")->createCustomFormatter($htmlController));

    $pres->save("pres.html", Java("com.aspose.slides.SaveFormat")->Html, $options);
} finally {
    if ($pres != null) $pres->dispose();
}

```
```java
public class CustomHeaderAndFontsController extends EmbedAllFontsHtmlController
{
    private final int m_basePath = 0;

    // Custom header template
    final static String Header = "<!DOCTYPE html>\n" +
            "<html>\n" +
            "<head>\n" +
            "<meta http-equiv=\"Content-Type\" content=\"text/html; charset=UTF-8\">\n" +
            "<meta http-equiv=\"X-UA-Compatible\" content=\"IE=9\">\n" +
            "<link rel=\"stylesheet\" type=\"text/css\" href=\"%s\">\n" +
            "</head>";

    private final String m_cssFileName;

    public CustomHeaderAndFontsController(String cssFileName) 
    {
        m_cssFileName = cssFileName;
    }

    public void writeDocumentStart(IHtmlGenerator generator, IPresentation presentation) 
    {
        generator.addHtml(String.format(Header, m_cssFileName));
        writeAllFonts(generator, presentation);
    }

    public void writeAllFonts(IHtmlGenerator generator, IPresentation presentation) 
    {
        generator.addHtml("<!-- Embedded fonts -->");
        super.writeAllFonts(generator, presentation);
    }
}
```
## **Embed All Fonts When Converting Presentation to HTML**
Convert PPT(X) presentation to HTML with all its embedded fonts. [**EmbedAllFontsHtmlController**](https://apireference.aspose.com/slides/java/com.aspose.slides/EmbedAllFontsHtmlController) class is used to embed all presentation fonts into HTML document. [**EmbedAllFontsHtmlController**](https://apireference.aspose.com/slides/java/com.aspose.slides/EmbedAllFontsHtmlController) has a parameterized constructor where an array of font names can be passed to prevent them from embedding. Some fonts, like Calibri or Arial, used in the presentation are not needed to be embedded (which leads the resulting HTML document to become larger) because almost every system already has them installed. The [**EmbedAllFontsHtmlController**](https://apireference.aspose.com/slides/java/com.aspose.slides/EmbedAllFontsHtmlController) also supports inheritance and WriteFont method that is intended to be overridden:

```php
$pres = new Java("com.aspose.slides.Presentation", "pres.pptx");
try
{
    //Exclude default presentation fonts
    $Array = new JavaClass("java.lang.reflect.Array");
    $String = new JavaClass("java.lang.String");
    $fontNameExcludeList = $Array->newInstance($String, 2);
    $fontNameExcludeList[0] = "Calibri";
    $fontNameExcludeList[1] = "Arial";
    
    $linkcont = new Java("com.aspose.slides.LinkAllFontsHtmlController", $fontNameExcludeList,"C:/Windows/Fonts/");

    $htmlOptionsEmbed = new Java("com.aspose.slides.HtmlOptions");
    $htmlOptionsEmbed->setHtmlFormatter(Java("com.aspose.slides.HtmlFormatter")->createCustomFormatter(($linkcont));

    $pres->save("pres.html", Java("com.aspose.slides.SaveFormat")->Html, $htmlOptionsEmbed);
}
finally {
    if ($pres != null) $pres->dispose();
}
```

```java
public class LinkAllFontsHtmlController extends EmbedAllFontsHtmlController
{
    private final String m_basePath;

    public LinkAllFontsHtmlController(String[] fontNameExcludeList, String basePath)
    {
        super(fontNameExcludeList);
        m_basePath = basePath;
    }

    public void writeFont
    (
            IHtmlGenerator generator,
            IFontData originalFont,
            IFontData substitutedFont,
            String fontStyle,
            String fontWeight,
            byte[] fontData)
    {
        try {
            String fontName = substitutedFont == null ? originalFont.getFontName() : substitutedFont.getFontName();
            String path = fontName + ".woff"; // some path sanitaze may be needed
            Files.write(new File(m_basePath + path).toPath(), fontData, StandardOpenOption.CREATE);

            generator.addHtml("<style>");
            generator.addHtml("@font-face { ");
            generator.addHtml("font-family: '" + fontName + "'; ");
            generator.addHtml("src: url('" + path + "')");

            generator.addHtml(" }");
            generator.addHtml("</style>");
        } catch (IOException ex) {
            ex.printStackTrace();
        }
    }
}
```

## **Support of SVG Responsive Property**
The code sample below shows how to export a PPT(X) presentation to HTML with the responsive layout:

```php
$pres = new Java("com.aspose.slides.Presentation", "SomePresentation.pptx");
try {
    $saveOptions = new Java("com.aspose.slides.HtmlOptions");
    $saveOptions->setSvgResponsiveLayout(true);
    $pres->save("SomePresentation-out.html", Java("com.aspose.slides.SaveFormat")->Html, $saveOptions);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Exporting Media Files to HTML file**
In order to export media files from PPT(X) presentation to HTML. Please follow the steps below:

1. Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Get reference of the slide.
1. Setting the transition effect.
1. Write the presentation as a PPTX file.

In the example given below, we have exported the media files to HTML.

```php
// Loading a presentation
$pres = new Java("com.aspose.slides.Presentation", "Media File.pptx");
try {
    $path = ".";
    $fileName = "ExportMediaFiles_out.html";
    $baseUri = "http://www.example.com/";

    $controller = new Java("com.aspose.slides.VideoPlayerHtmlController", $path, $fileName, $baseUri);

    // Setting HTML options
    $htmlOptions = new Java("com.aspose.slides.HtmlOptions", $controller);
    $svgOptions = new Java("com.aspose.slides.SVGOptions", $controller);

    $htmlOptions->setHtmlFormatter(Java("com.aspose.slides.HtmlFormatter")->createCustomFormatter($controller));
    $htmlOptions->setSlideImageFormat(Java("com.aspose.slides.SlideImageFormat")->svg($svgOptions));

    // Saving the file
    $pres->save($fileName, Java("com.aspose.slides.SaveFormat")->Html, $htmlOptions);
} finally {
    if ($pres != null) $pres->dispose();
}
```
