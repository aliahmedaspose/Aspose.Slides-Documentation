---
title: Manage OLE
type: docs
weight: 232
url: /java/manage-ole/
---

{{% alert color="primary" %}} 

OLE  (Object Linking & Embedding) is a Microsoft technology that allows data and objects created in one application to be placed in another application through linking or embedding. 

{{% /alert %}} 

Consider a chart created in MS Excel. The chart is then placed inside a PowerPoint slide. That Excel chart is considered an OLE object. 

- An OLE object may appear as an icon. In this case, when you double-click the icon, the chart gets opened in its associated application (Excel), or you are asked to select an application for object opening or editing. 
- An OLE object may display actual contents—for example, the contents of a $chart-> In this case, the chart is activated in PowerPoint, the chart interface loads, and you get to modify the chart's data within the PowerPoint app. 

Aspose.Slides for Java allows you to insert OLE Objects into slides as OLE Object Frames. In this topic, we will show you how to work with OLE Object Frames. You will learn how to add and manipulate OLE objects. 

## **Adding OLE Object Frames to Slides**
Assuming you already created a chart in Microsoft Excel and want to embed that chart in a slide as an OLE Object Frame using Aspose.Slides for Java, you can do it this way:

1. Create an instance of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain the reference of the slide by using its index.
1. Open the Excel file containing the Excel chart object and save it to MemoryStream.
1. Add the OLE Object Frame to the slide containing the array of bytes and other information about the OLE object.
1. Write the modified presentation as a PPTX file.

In the example below, we added a chart from an Excel file to a slide as an OLE Object Frame using Aspose.Slides for Java.  
**Note** that the [IOleEmbeddedDataInfo](https://apireference.aspose.com/slides/java/com.aspose.slides/IOleEmbeddedDataInfo) constructor takes an embeddable object extension as a second parameter. This extension allows PowerPoint to correctly interpret the file type and choose the right application to open this OLE object.

```php 
// Instantiate Prseetation class that represents the PPTX
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Access the first slide
    $sld = $pres->getSlides()->get_Item(0);

    // Load an cel file to stream
    $fs = new Java("java.io.FileInputStream", new Java("java.io.File", "book1.xlsx");
    try {
    $mstream = new Java("java.io.ByteArrayOutputStream");
    $Array = new JavaClass("java.lang.reflect.Array");
    $Byte = new JavaClass("java.lang.Byte");
    $buf = $Array->newInstance($Byte, 4096);
    while (true)
    {
        $bytesRead = $fs->read($buf, 0, $buf->length);
        if ($bytesRead <= 0)
            break;
        $mstream->write($buf, 0, $bytesRead);
    }
    } finally {
        if ($fs != null) $fs->close();
    }

    // Create data object for embedding
    $dataInfo = new Java("com.aspose.slides.OleEmbeddedDataInfo", $mstream->toByteArray(), "xlsx");
    $mstream->close();

    // Add an Ole Object Frame shape
    $oleObjectFrame = $sld->getShapes()->addOleObjectFrame(0, 0,
            $pres->getSlideSize()->getSize()->getWidth(),
            $pres->getSlideSize()->getSize()->getHeight(),
            $dataInfo);

    //Write the PPTX to disk
    $pres->save("OleEmbed_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} catch (JavaException $e) {
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Accessing OLE Object Frames**
If an OLE object is already embedded in a slide, you can find or access that object easily using Aspose.Slides for Java this way:

1. Create an instance of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain the reference of the slide by using its index.
1. Access the OLE Object Frame shape.

   In our example, we used the previously created PPTX, which has only one shape on the first slide.  We then *cast* that object as an [OleObjectFrame](https://apireference.aspose.com/slides/java/com.aspose.slides/OleObjectFrame). This was the desired OLE Object Frame to be accessed.
1. Once the OLE Object Frame is accessed, you can perform any operation on it.

In the example below, an OLE Object Frame (an Excel chart object embedded in a slide) is accessed—and then its file data gets written to an Excel file.

```php 
// Load the PPTX to Presentation object
$pres = new Java("com.aspose.slides.Presentation", "AccessingOLEObjectFrame.pptx");
try {
    // Access the first slide
    $sld = $pres->getSlides()->get_Item(0);

    // Cast the shape to OleObjectFrame
    $oleObjectFrame = $sld->getShapes()->get_Item(0);

    // Read the OLE Object and write it to disk
    if ($oleObjectFrame != null) {
        // Get embedded file data
        $data = $oleObjectFrame->getEmbeddedData()->getEmbeddedFileData();

        // Get embedded file extention
        $fileExtention = $oleObjectFrame->getEmbeddedData()->getEmbeddedFileExtension();

        // Create path for saving the extracted file
        $extractedPath = "excelFromOLE_out" + fileExtention;

        // Save extracted data
        $fstr = new Java("java.io.FileOutputStream", extractedPath);
        try {
            $fstr->write($data, 0, $data->length);
        } finally {
            $fstr->close();
        }
    }
} catch (JavaException $e) {
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Changing OLE Object Data**

If an OLE object is already embedded in a slide, you can easily access that object with Aspose.Slides for Java and modify its data this way:

1. Open the desired presentation with the embedded OLE Object by creating an instance of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain the reference of the slide by using its Index.
1. Access the OLE Object Frame shape.

   In our example, we used the previously created PPTX, which has only one shape on the first slide. We then *cast* that object as an [OleObjectFrame](https://apireference.aspose.com/slides/java/com.aspose.slides/OleObjectFrame). This was the desired OLE Object Frame to be accessed.
1. Once the OLE Object Frame is accessed, you can perform any operation on it.
1. Create the Workbook object and access the OLE Data.
1. Access the desired Worksheet and amend the data.
1. Save the updated Workbook in streams.
1. Change the OLE object data from stream data.

In the example below, an OLE Object Frame (an Excel chart object embedded in a slide) is accessed—and then its file data is modified to change the chart data.

```php 
$pres = new Java("com.aspose.slides.Presentation", "ChangeOLEObjectData.pptx");
try {
    $slide = $pres->getSlides()->get_Item(0);
	
    $ole = null;

    // Traversing all shapes for Ole frame
    foreach( $slide->getShapes() as $shape ) 
    {
        if ($shape instanceof OleObjectFrame) 
        {
            $ole = $shape;
        }
    }

    if ($ole != null) {
        $msln = new Java("java.io.ByteArrayOutputStream", $ole->getEmbeddedData()->getEmbeddedFileData());
        try {
            // Reading object data in Workbook
            $Wb = new Java("com.aspose.slides.Workbook", $msln);

            $msout = new Java("java.io.ByteArrayOutputStream");
            try {
                // Modifying the workbook data
                $Wb->getWorksheets()->get(0)->getCells()->get(0, 4).putValue("E");
                $Wb->getWorksheets()->get(0)->getCells()->get(1, 4).putValue(12);
                $Wb->getWorksheets()->get(0)->getCells()->get(2, 4).putValue(14);
                $Wb->getWorksheets()->get(0)->getCells()->get(3, 4).putValue(15);

                $so1 = new OoxmlSaveOptions(Java("com.aspose.cells.SaveFormat")->XLSX);
                $Wb->save($msout, $so1);

                // Changing Ole frame object data
                $newData = new Java("com.aspose.slides.OleEmbeddedDataInfo", $msout->toByteArray(), $ole->getEmbeddedData()->getEmbeddedFileExtension());
                $ole->setEmbeddedData($newData);
            } finally {
                if ($msout != null) $msout->close();
            }
        } finally {
            if ($msln != null) $msln->close();
        }
    }

    $pres->save("OleEdit_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} catch (JavaException $e) {
} finally {
    if ($pres != null) $pres->dispose();
}
```

## Embedding Other File Types in Slides

Besides Excel charts, Aspose.Slides for Java allows you to embed other types of files in slides. For example, you can insert HTML, PDF, and ZIP files as objects into a slide. When a user double-clicks the inserted object, the object automatically gets launched in the relevant program, or the user gets directed to select an appropriate program to open the object. 

This sample code shows you how to embed HTML and ZIP in a slide:

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $slide = $pres->getSlides()->get_Item(0);

    $file = new Java("java.io.File", "embedOle.html");
    $Array = new JavaClass("java.lang.reflect.Array");
    $Byte = new JavaClass("java.lang.Byte");
    $htmlBytes = $Array->newInstance($Byte, $file->length());
    $dis = new Java("java.io.DataInputStream", new Java("java.io.FileInputStream", $file));
    try {
    $dis->readFully($htmlBytes);
    } finally {
            if ($dis != null) $dis->close();
        }
    $dataInfoHtml = new Java("com.aspose.slides.OleEmbeddedDataInfo", $htmlBytes, "html");
    $oleFrameHtml = $slide->getShapes()->addOleObjectFrame(150, 120, 50, 50, $dataInfoHtml);
    $oleFrameHtml->setObjectIcon(true);
    
    $zipFile = new Java("java.io.File", "embedOle.zip");
    $zipBytes = $Array->newInstance($Byte, $zipFile->length());
    $zDis = new Java("java.io.DataInputStream", new Java("java.io.FileInputStream", $zipFile));
    try {
    $zDis->readFully($zipBytes);
    } finally {
                if ($zDis != null) $zDis->close();
            }
    $dataInfoZip = new Java("com.aspose.slides.OleEmbeddedDataInfo", $zipBytes, "zip");
    $oleFrameZip = $slide->getShapes()->addOleObjectFrame(150, 220, 50, 50, $dataInfoZip);
    $oleFrameZip->setObjectIcon(true);

    $pres->save("embeddedOle.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} catch (JavaException $e) {
} finally {
    if ($pres != null) $pres->dispose();
}
```

## Setting File Types for Embedded Objects

When working on presentations, you may need to replace old OLE objects with new ones. Or you may need to replace an unsupported OLE object with a supported one. 

Aspose.Slides for Java allows you to set the file type for an embedded object. This way, you get to change the OLE frame data or its extension. 

This sample code shows you how to set the file type for an embedded OLE object:

```php
$pres = new Java("com.aspose.slides.Presentation", "embeddedOle.pptx");
try {
    $slide = $pres->getSlides()->get_Item(0);
    $oleObjectFrame = $slide->getShapes()->get_Item(0);
    echo("Current embedded data extension is: " + $oleObjectFrame->getEmbeddedData()->getEmbeddedFileExtension());

    $oleObjectFrame->setEmbeddedData(new Java("com.aspose.slides.OleEmbeddedDataInfo", Files->readAllBytes(Paths->get("embedOle.zip")), "zip"));

    $pres->save("embeddedChanged.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} catch (JavaException $e) {
} finally {
    if ($pres != null) $pres->dispose();
}
```

## Setting Icon Images and Titles for Embedded Objects

After you embed an OLE object, a preview consisting of an icon image and title gets added automatically. The preview is what users see before they access or open the OLE object. 

If you want to use a specific image and text as elements in the preview, you can set the icon image and title using Aspose.Slides for Java. 

This Java code shows you how to set the icon image and title for an embedded object: 

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $slide = $pres->getSlides()->get_Item(0);
    $oleObjectFrame = $slide->getShapes()->get_Item(0);
	$fis = new Java("java.io.FileInputStream", new Java("java.io.File", "watermark.png"));
	try {
    $oleImage = $pres->getImages()->addImage($fis);
    } finally {
    if ($fis != null) $fis->close();
    }
    $oleObjectFrame->setSubstitutePictureTitle("My title");
    $oleObjectFrame->getSubstitutePictureFormat()->getPicture()->setImage($oleImage);
    $oleObjectFrame->setObjectIcon(false);

    $pres->save("embeddedOle-newImage.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} catch (JavaException $e) {
} finally {
    if ($pres != null) $pres->dispose();
}
```

## Extracting Embedded Files

Aspose.Slides for Java allows you to extract the files embedded in slides as OLE objects this way:

1. Create an instance of the Presentation class containing the OLE object you intend to extract.
2. Loop through all the shapes in the presentation and access the OLE Object Frame shape.
3. Access the embedded file's data from the OLE Object Frame and write it to disk. 

This sample code shows you how to extract a file embedded in a slide as an OLE object:

```php
$pres = new Java("com.aspose.slides.Presentation", "embeddedOle.pptx");
try {
    $slide = $pres->getSlides()->get_Item(0);

    for ($index = 0; index < $slide->getShapes()->size(); index++)
    {
        $shape = $slide->getShapes()->get_Item($index);
        $oleFrame = $shape;

        if ($oleFrame != null) 
		{
            $data = $oleFrame->getEmbeddedData()->getEmbeddedFileData();
            $extension = $oleFrame->getEmbeddedData()->getEmbeddedFileExtension();

            // Save extracted data
            $fstr = new Java("java.io.FileOutputStream", "oleFrame" + $index + $extension);
            try {
                $fstr->write($data, 0, $data->length);
            } finally {
                $fstr->close();
            }
        }
    }
} catch (JavaException $e) {
} finally {
    if ($pres != null) $pres->dispose();
}
```