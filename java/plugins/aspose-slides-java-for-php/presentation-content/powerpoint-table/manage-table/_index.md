---
title: Manage Table
type: docs
weight: 10
url: /java/manage-table/
---

## **Create Table from Scratch**
Aspose.Slides for Java has provided the simplest API to create tables in an easiest way. To create a table in a slide and perform some basic operations on the table, please follow the steps below:

- Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
- Obtain the reference of a slide by using its Index.
- Define Array of Columns with Width.
- Define Array of Rows with Height.
- Add a Table to the slide using [addTable](https://apireference.aspose.com/slides/java/com.aspose.slides/IShapeCollection#addTable-float-float-double:A-double:A-) method exposed by [IShapeCollection](https://apireference.aspose.com/slides/java/com.aspose.slides/IShapeCollection) object.
- Iterate through each Cell to apply formatting to the Top, Bottom, Right, Left Borders.
- Merge first two cells of the first row of the table.
- Access the Text Frame of a Cell.
- Add some text to the Text Frame.
- Save the modified presentation as a PPTX file.

```php
// Instantiate Presentation class that represents PPTX file
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Access first slide
    $sld = $pres->getSlides()->get_Item(0);

    // Define columns with widths and rows with heights
    $Array = new JavaClass("java.lang.reflect.Array");
    $Double = new JavaClass("java.lang.Double");
    $dblCols = $Array->newInstance($Double, 3);
    $dblCols[0] = 50;
    $dblCols[1] = 50;
    $dblCols[2] = 50;
    $dblRows = $Array->newInstance($Double, 5);
    $dblRows[0] = 50;
    $dblRows[1] = 30;
    $dblRows[2] = 30;
    $dblRows[3] = 30;
    $dblRows[4] = 30;
    // Add table shape to slide
    $tbl = $sld->getShapes()->addTable(100, 50, $dblCols, $dblRows);

    // Set border format for each cell
    for ($row = 0; row < $tbl->getRows()->size(); row++)
    {
        for ($cell = 0; cell < $tbl->getRows()->get_Item($row)->size(); cell++)
        {
            $cellFormat = $tbl->getRows()->get_Item($row)->get_Item($cell)->getCellFormat();
            
            $cellFormat->getBorderTop()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
            $cellFormat->getBorderTop()->getFillFormat()->getSolidFillColor()->setColor(Java("java.awt.Color")->RED);
            $cellFormat->getBorderTop()->setWidth(5);

            $cellFormat->getBorderBottom()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
            $cellFormat->getBorderBottom()->getFillFormat()->getSolidFillColor()->setColor(Java("java.awt.Color")->RED);
            $cellFormat->getBorderBottom()->setWidth(5);

            $cellFormat->getBorderLeft()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
            $cellFormat->getBorderLeft()->getFillFormat()->getSolidFillColor()->setColor(Java("java.awt.Color")->RED);
            $cellFormat->getBorderLeft()->setWidth(5);

            $cellFormat->getBorderRight()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
            $cellFormat->getBorderRight()->getFillFormat()->getSolidFillColor()->setColor(Java("java.awt.Color")->RED);
            $cellFormat->getBorderRight()->setWidth(5);
        }
    }
    // Merge cells 1 & 2 of row 1
    $tbl->mergeCells($tbl->getRows()->get_Item(0)->get_Item(0), $tbl->getRows()->get_Item(1)->get_Item(1), false);

    // Add text to the merged cell
    $tbl->getRows()->get_Item(0)->get_Item(0)->getTextFrame()->setText("Merged Cells");

    // Save PPTX to Disk
    $pres->save("table.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Access Existing Table**
To access a table that already exists in a slide, please follow the steps below:

- Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
- Obtain the reference of a slide (that contains the table) by using its Position.
- Create an [ITable](https://apireference.aspose.com/slides/java/com.aspose.slides/ITable) object and set it to null.
- Iterate through all Shapes until you find the Table. If a slide contains only one table then you can simply check a shape and if it is found to be a Table then just typecast it as a [Table](https://apireference.aspose.com/slides/java/com.aspose.slides/Table) object. But, if the slide contains more than one tables then it's better to find your desired table using its Alternative Text.
- After the Table is found, you can use [ITable](https://apireference.aspose.com/slides/java/com.aspose.slides/ITable) object to control the table. For example, in our case, we have added a new row in the desired table.
- Save the modified presentation as a PPT file.

```php
// Instantiate Presentation class that represents PPTX// Instantiate Presentation class that represents PPTX
$pres = new Java("com.aspose.slides.Presentation", "UpdateExistingTable.pptx");
try {

    // Access the first slide
    $sld = $pres->getSlides()->get_Item(0);

    // Initialize null TableEx
    $tbl = null;

    // Iterate through the shapes and set a reference to the table found
    foreach( $sld->getShapes() as $shp ) 
    {
        if ($shp instanceof ITable) 
        {
            $tbl = $shp;
            // Set the text of the first column of second row
            $tbl->get_Item(0, 1)->getTextFrame()->setText("New");
        }
    }
    
    //Write the PPTX to Disk
    $pres->save("table1_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Align Text in Table**
Aspose.Slides for Java has provided the simplest API to work with tables in an easiest way. To clone a table row or column in a slide, please follow the steps below:

- Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
- Obtain the reference of a slide by using its Index.
- Insert table in the slide.
- Access text frame.
- Access paragraph.
- Align text vertically.
- Save the presentation as a PPTX file.

```php
// Create an instance of Presentation class
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Get the first slide 
    $slide = $pres->getSlides()->get_Item(0);
    
    // Define columns with widths and rows with heights
    $Array = new JavaClass("java.lang.reflect.Array");
    $Double = new JavaClass("java.lang.Double");
    $dblCols = $Array->newInstance($Double, 4);
    $dblCols[0] = 120;
    $dblCols[1] = 120;
    $dblCols[2] = 120;
    $dblCols[3] = 120;
    $dblRows = $Array->newInstance($Double, 4);
    $dblRows[0] = 100;
    $dblRows[1] = 100;
    $dblRows[2] = 100;
    $dblRows[3] = 100;     
    // Add table shape to slide
    $tbl = $slide->getShapes()->addTable(100, 50, $dblCols, $dblRows);
    $tbl->get_Item(1, 0)->getTextFrame()->setText("10");
    $tbl->get_Item(2, 0)->getTextFrame()->setText("20");
    $tbl->get_Item(3, 0)->getTextFrame()->setText("30");
    
    // Accessing the text frame
    $txtFrame = $tbl->get_Item(0, 0)->getTextFrame();
    
    // Create the Paragraph object for text frame
    $paragraph = $txtFrame->getParagraphs()->get_Item(0);
    
    // Create Portion object for paragraph
    $portion = $paragraph->getPortions()->get_Item(0);
    $portion->setText("Text here");
    $portion->getPortionFormat()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
    $portion->getPortionFormat()->getFillFormat()->getSolidFillColor()->setColor(Java("java.awt.Color")->BLACK);
    
    // Aligning the text vertically
    $cell = $tbl->get_Item(0, 0);
    $cell->setTextAnchorType(Java("com.aspose.slides.TextAnchorType")->Center);
    $cell->setTextVerticalType(Java("com.aspose.slides.TextVerticalType")->Vertical270);
    
    // Save Presentation
    $pres->save("Vertical_Align_Text_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Set Text Formatting on Table Level**
Aspose.Slides for Java has provided the simplest API to create tables in an easiest way. In order to remove Text Formatting from table cells, please follow the steps below:

- Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
- Obtain the reference of a slide by using its Index.
- Access Table from Slide.
- Set Table Cells Font Height.
- Set Table Cells Text Alignment and right Margin in one Call.
- Set Table Cells Vertical Type.
- Save the modified presentation as a PPTX file.

```php
// Create an instance of Presentation class
$pres = new Java("com.aspose.slides.Presentation", "simpletable.pptx");
try {
    // the first shape on the first slide is a table
    $someTable = $pres->getSlides()->get_Item(0)->getShapes()->get_Item(0);
    
    // setting table cells' font height
    $portionFormat = new Java("com.aspose.slides.PortionFormat");
    $portionFormat->setFontHeight(25);
    $someTable->setTextFormat($portionFormat);
    
    // setting table cells' text alignment and right margin in one call
    $paragraphFormat = new Java("com.aspose.slides.ParagraphFormat");
    $paragraphFormat->setAlignment(Java("com.aspose.slides.TextAlignment")->Right);
    $paragraphFormat->setMarginRight(20);
    $someTable->setTextFormat($paragraphFormat);
    
    // setting table cells' text vertical type
    $textFrameFormat = new Java("com.aspose.slides.TextFrameFormat");
    $textFrameFormat->setTextVerticalType(Java("com.aspose.slides.TextVerticalType")->Vertical);
    $someTable->setTextFormat($textFrameFormat);
    
    $pres->save("result.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Numbering in Standard Table**
In a standard table numeration of cells is straightforward and zero-based. The first cell in a table is indexed as 0,0 (column 0, row 0). For example, the cells in a table with 4 columns and 4 rows will be numbered accordingly:

|(0, 0)|(1, 0)|(2, 0)|(3, 0)|
| :- | :- | :- | :- |
|(0, 1)|(1, 1)|(2, 1)|(3, 1)|
|(0, 2)|(1, 2)|(2, 2)|(3, 2)|
|(0, 3)|(1, 3)|(2, 3)|(3, 3)|

```php
// Instantiate Presentation class that represents PPTX file
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Access first slide
    $sld = $pres->getSlides()->get_Item(0);

    // Define columns with widths and rows with heights
    $Array = new JavaClass("java.lang.reflect.Array");
    $Double = new JavaClass("java.lang.Double");
    $dblCols = $Array->newInstance($Double, 4);
    $dblCols[0] = 70;
    $dblCols[1] = 70;
    $dblCols[2] = 70;
    $dblCols[3] = 70;
    $dblRows = $Array->newInstance($Double, 4);
    $dblRows[0] = 70;
    $dblRows[1] = 70;
    $dblRows[2] = 70;
    $dblRows[3] = 70; 
    // Add table shape to slide
    $tbl = $sld->getShapes()->addTable(100, 50, $dblCols, $dblRows);

    // Set border format for each cell
    foreach( $tbl->getRows() as $row )
    {
        foreach( $row as $cell )
        {
            $cell->getCellFormat()->getBorderTop()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
            $cell->getCellFormat()->getBorderTop()->getFillFormat()->getSolidFillColor()->setColor(Java("java.awt.Color")->RED);
            $cell->getCellFormat()->getBorderTop()->setWidth(5);

            $cell->getCellFormat()->getBorderBottom()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
            $cell->getCellFormat()->getBorderBottom()->getFillFormat()->getSolidFillColor()->setColor(Java("java.awt.Color")->RED);
            $cell->getCellFormat()->getBorderBottom()->setWidth(5);

            $cell->getCellFormat()->getBorderLeft()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
            $cell->getCellFormat()->getBorderLeft()->getFillFormat()->getSolidFillColor()->setColor(Java("java.awt.Color")->RED);
            $cell->getCellFormat()->getBorderLeft()->setWidth(5);

            $cell->getCellFormat()->getBorderRight()->getFillFormat()->setFillType(Java("com.aspose.slides.FillType")->Solid);
            $cell->getCellFormat()->getBorderRight()->getFillFormat()->getSolidFillColor()->setColor(Java("java.awt.Color")->RED);
            $cell->getCellFormat()->getBorderRight()->setWidth(5);
        }
    }

    //Write PPTX to Disk
    $pres->save("StandardTables_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Lock Aspect Ratio of Table**
The aspect ratio of a geometric shape is the ratio of its sizes in different dimensions. You can lock aspect ratio of table using [**setAspectRatioLocked**](https://apireference.aspose.com/slides/java/com.aspose.slides/GraphicalObjectLock#setAspectRatioLocked-boolean-) method. Below code example shows how to use this method.

```php
$pres = new Java("com.aspose.slides.Presentation", "pres.pptx");
try {
    $table = $pres->getSlides()->get_Item(0)->getShapes()->get_Item(0);
    echo("Lock aspect ratio set: " . $table->getGraphicalObjectLock()->getAspectRatioLocked());

    $table->getGraphicalObjectLock()->setAspectRatioLocked(!$table->getGraphicalObjectLock()->getAspectRatioLocked()); // invert

    echo("Lock aspect ratio set: " . $table->getGraphicalObjectLock()->getAspectRatioLocked());

    $pres->save("pres-out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```
