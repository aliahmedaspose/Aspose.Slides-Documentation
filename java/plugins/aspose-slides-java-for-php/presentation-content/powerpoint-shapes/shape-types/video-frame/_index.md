---
title: Video Frame
type: docs
weight: 10
url: /java/video-frame/
---

## **Create Embedded Video Frame**
Developers can also add and play video files in slides to enrich their presentations. Aspose.Slides for Java supports addition of Video Frames into slides—and this means you get to add videos to your presentations. In this topic, we will describe operations to add video frames to slides using examples and simple steps.

To add a Video Frame in a slide using Aspose.Slides for Java, do this:

1. Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain the reference of a slide by using its Index.
1. [Add the Video Frame](https://apireference.aspose.com/slides/java/com.aspose.slides/IShapeCollection#addVideoFrame-float-float-float-float-com.aspose.slides.IVideo-) (containing the video file name) into the slide.
1. Write the modified presentation as a PPTX file.

In the example below, we added a Video Frame to the slide.

```php
// Instantiate Presentation class that represents the PPTX
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Get the first slide
    $sld = $pres->getSlides()->get_Item(0);
    
    // Embed video inside presentation
    $vid = $pres->getVideos()->addVideo(new FileInputStream(new Java("java.io.File", "Wildlife.mp4")));

    // Add Video Frame
    $vf = $sld->getShapes()->addVideoFrame(50, 150, 300, 350, $vid);

    // Set video to Video Frame
    $vf->setEmbeddedVideo($vid);

    // Set Play Mode and Volume of the Video
    $vf->setPlayMode(Java("com.aspose.slides.VideoPlayModePreset")->Auto);
    $vf->setVolume(Java("com.aspose.slides.AudioVolumeMode")->Loud);

    // Write the PPTX file to disk
    $pres->save("VideoFrame.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} catch (Exception e) {
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Create Video Frame with Video from Web Source**
PowerPoint 2010 and newer versions support YouTube videos. To play such videos in PowerPoint, verify that your [environment meet the requirements](https://support.office.com/en-us/article/Requirements-for-using-the-PowerPoint-YouTube-feature-2a0e184d-af50-4da9-b530-e4355ac436a9?ui=en-US&rs=en-US&ad=US) for embedding videos from web sources.

To add video from YouTube with Aspose.Slides, do this:

1. Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain the reference of a slide by using its Index.
1. [Add the Video Frame](https://apireference.aspose.com/slides/java/com.aspose.slides/IShapeCollection#addVideoFrame-float-float-float-float-java.lang.String-) by passing video URL.
1. Set Image for Video Frame.
1. Save presentation as a PPTX file.

This sample code shows you how to add a video from YouTube to a slide:

```php
// Instantiate Presentation class that represents the PPTX
$pres = new Java("com.aspose.slides.Presentation");
try {
    addVideoFromYouTube($pres, "Tj75Arhq5ho");
    $pres->save("out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```
```php
private static void addVideoFromYouTube(Presentation pres, String videoID)
{
    // add videoFrame
    $videoFrame = $pres->getSlides()->get_Item(0)->getShapes()->addVideoFrame(
            10, 10, 427, 240, "https://www.youtube.com/embed/" + videoID);
    $videoFrame->setPlayMode(Java("com.aspose.slides.VideoPlayModePreset")->Auto);

    // load thumbnail
    $thumbnailUri = "http://img.youtube.com/vi/" + videoID + "/hqdefault.jpg";
    URL url;

    try {
        $url = new URL($thumbnailUri);
        $videoFrame->getPictureFormat()->getPicture()->setImage($pres->getImages()->addImage($url->openStream()));
    } catch (JavaException $ex) {
    }
}
```

## **Create Video Frame**
Developers can also embed and play video files in slides to enrich their presentations. Aspose.Slides for Java supports addition of Embedded Video Frames to slides—and this means you get to add videos to your presentations. 

To add an Embedded Video Frame in a slide using Aspose.Slides for Java, do this:

1. Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class.
1. Obtain the reference of a slide by using its Index.
1. [Add the Video Frame](https://apireference.aspose.com/slides/java/com.aspose.slides/IShapeCollection#addVideoFrame-float-float-float-float-java.lang.String-) (containing the video file name) into the slide.
1. Add the video to be embedded inside presentation Video collection using Video.
1. Set embedded video to Video frame.
1. Write the modified presentation as a PPTX file.

In the example below, we added a Video Frame to the slide.

```php
// Instantiate Presentation class that represents the PPTX
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Get the first slide
    $sld = $pres->getSlides()->get_Item(0);

    // Add Video Frame
    $vf = $sld->getShapes()->addVideoFrame(50, 150, 300, 150, "Wildlife.mp4");

    // Set Play Mode and Volume of the Video
    $vf->setPlayMode(Java("com.aspose.slides.VideoPlayModePreset")->Auto);
    $vf->setVolume(Java("com.aspose.slides.AudioVolumeMode")->Loud);

    // Write the PPTX file to disk
    $pres->save("VideoFrame.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Extract Video From Slide**
Aspose.Slides for Java supports extraction of videos from slides. To extract a video from a slide, do this:

- Load a [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) containing a video.
- Loop through all the slides of the [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation).
- Search for Video Frame.
- Save the Video to disk.

In the example given below, we saved the video file from a slide.

```php
$pres = new Java("com.aspose.slides.Presentation", "VideoSample.pptx");
try {
    for ($slide : $pres->getSlides()) 
    {
        for ($shape : $slide->getShapes()) 
        {
            if ($shape instanceof VideoFrame) 
            {
                $vf = shape;
                $type = $vf->getEmbeddedVideo()->getContentType();
                $ss = type.lastIndexOf('-');
                $buffer = $vf->getEmbeddedVideo()->getBinaryData();

                //Get File Extension
                $charIndex = $type->indexOf("/");
                $type = $type->substring($charIndex + 1);

                $fop = new Java("java.io.FileOutputStream", "testing2." + $type);
                $fop->write($buffer);
                $fop->flush();
                $fop->close();
            }
        }
    }
} catch (JavaException $e) {
} finally {
    if ($pres != null) $pres->dispose();
}
```