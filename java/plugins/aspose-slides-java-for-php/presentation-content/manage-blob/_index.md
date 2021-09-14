---
title: Manage Blob
type: docs
weight: 80
url: /java/manage-blob/
---

## **Add Blob in Presentations**
Aspose.Slides for Java provides a facility to add large files (video file in that case) and prevent a high memory consumption. An example is given below that shows how to add Blob in presentations using Java.

```php
// create a new presentation which will contain this video
$pres = new Java("com.aspose.slides.Presentation");
try {
    $fileStream = new Java("java.io.FileInputStream", new Java("java.io.File", "veryLargeVideo.avi"));
    try {
        // let's add the video to the presentation - we choose KeepLocked behavior, because we not
        // have an intent to access the "veryLargeVideo.avi" file.
        $video = $pres->getVideos()->addVideo($fileStream, Java("com.aspose.slides.LoadingStreamBehavior")->KeepLocked);
        $pres->getSlides()->get_Item(0)->getShapes()->addVideoFrame(0, 0, 480, 270, $video);

        // save the presentation. Despite that the output presentation will be very large, the memory
        // consumption will be low the whole lifetime of the pres object
        $pres->save("presentationWithLargeVideo.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
    } finally {
        $fileStream->close();
    }
} catch (JavaException $e) {
} finally {
    $pres->dispose();
}
```

## **Export Blob from Presentations**
Aspose.Slides for Java provides a facility to Export large files (audio and video file in that case). We want to extract these files from the presentation and do not want to load this presentation into memory to keep our memory consumption low. Here is an example is given below how we can export Blob from presentations in Java.

```php
$loadOptions = new Java("com.aspose.slides.LoadOptions");
// lock the source file and don't load it into memory
$loadOptions->getBlobManagementOptions()->setPresentationLockingBehavior(Java("com.aspose.slides.PresentationLockingBehavior")->KeepLocked);

// create the Presentation's instance, lock the "hugePresentationWithAudiosAndVideos.pptx" file.
$pres = new Java("com.aspose.slides.Presentation", "Large_Video_File_Test.pptx", $loadOptions);
try {
    // let's save each video to a file. to prevent memory usage we need a buffer which will be used
    // to exchange tha data from the presentation's video stream to a stream for newly created video file.
    $Array = new JavaClass("java.lang.reflect.Array");
    $Byte = new JavaClass("java.lang.Byte");
    $buffer = $Array->newInstance($Byte, 8 * 1024);
    
    // iterate through the videos
    for ($index = 0; $index < $pres->getVideos()->size(); $index++) {
        $video = $pres->getVideos()->get_Item($index);

        // open the presentation video stream. Please note that we intentionally avoid accessing properties
        // like video.BinaryData - this property returns a byte array containing full video, and that means
        // this bytes will be loaded into memory. We will use video.GetStream, which will return Stream and
        // that allows us to not load the whole video into memory.
        $presVideoStream = video->getStream();
        try {
            $outputFileStream = new Java("java.io.FileOutputStream", "video" + $index + ".avi");
            try {
                $bytesRead;
                while (($bytesRead = $presVideoStream->read($buffer, 0, $buffer->length)) > 0) {
                    $outputFileStream->write($buffer, 0, $bytesRead);
                }
            } finally {
                $outputFileStream->close();
            }
        } finally {
            $presVideoStream->close();
        }
        // memory consumption will stay low no matter what size the videos or presentation is.
    }
    // do the same for audios if needed.
} catch (JavaException $e) {
} finally {
    $pres->dispose();
}
```

## **Add Image as Blob in Presentation**
Aspose.Slides for Java added a new method to [**IImageCollection**](https://apireference.aspose.com/java/slides/com.aspose.slides/IImageCollection) interface and [**ImageCollection**](https://apireference.aspose.com/java/slides/com.aspose.slides/ImageCollection) class to support adding a large images as streams to treat them as BLOBs.

This example demonstrates how to include the large Blob ($image) and prevent a high memory consumption.

```php
// create a new presentation which will contain this image
$pres = new Java("com.aspose.slides.Presentation");
try {
    $fip = new Java("java.io.FileInputStream", new Java("java.io.File", "large_image.jpg"));
    try {
        // let's add the image to the presentation - we choose KeepLocked behavior, because we not
        // have an intent to access the "largeImage.png" file.
        $img = $pres->getImages()->addImage($fip, Java("com.aspose.slides.LoadingStreamBehavior")->KeepLocked);
        $pres->getSlides()->get_Item(0)->getShapes()->addPictureFrame(Java("com.aspose.slides.ShapeType")->Rectangle, 0, 0, 300, 200, $img);

        // save the presentation. Despite that the output presentation will be
        // large, the memory consumption will be low the whole lifetime of the pres object
        $pres->save("presentationWithLargeImage.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
    } finally {
        $fip->close();
    }
} catch (JavaException $e) {
} finally {
    $pres->dispose();
}
```


