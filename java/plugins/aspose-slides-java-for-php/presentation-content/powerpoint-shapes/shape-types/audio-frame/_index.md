---
title: Audio Frame
type: docs
weight: 10
url: /java/audio-frame/
---

## **Create Audio Frame**
Aspose.Slides for Java allows developers to add audio files in their slides. These audio files are embedded in the slides as Audio Frames . An Audio Frame contains the embedded audio file. In this topic, we will discuss that how can developers embed audio frames in their slides using Aspose.Slides for Java . To add an Embedded Audio Frame in a slide using Aspose.Slides for Java , please follow the steps below:

- Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class
- Obtain the reference of a slide by using its Index
- Open the Audio File Stream to be embedded in the slide
- Add the Embedded Audio Frame (containing audio file) into the slide
- Set [PlayMode](https://apireference.aspose.com/slides/java/com.aspose.slides/AudioPlayModePreset) and [Volume](https://apireference.aspose.com/slides/java/com.aspose.slides/AudioVolumeMode) exposed by [IAudioFrame](https://apireference.aspose.com/slides/java/com.aspose.slides/IAudioFrame) object
- Write the modified presentation as a PPTX file

In the example given below, we have added an Embedded Audio Frame into the slide.

```php
// Instantiate Prseetation class that represents the PPTX
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Get the first slide
    $sld = $pres->getSlides()->get_Item(0);

    // Load the wav sound file to stram
    $fstr = new Java("java.io.FileInputStream", new Java("java.io.File", "audio.wav"));

    // Add Audio Frame
    $af = $sld->getShapes()->addAudioFrameEmbedded(50, 150, 100, 100, $fstr);

    // Set Play Mode and Volume of the Audio
    $af->setPlayMode(Java("com.aspose.slides.AudioPlayModePreset")->Auto);
    $af->setVolume(Java("com.aspose.slides.AudioVolumeMode")->Loud);

    //Write the PPTX file to disk
    $pres->save("AudioFrameEmbed_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} catch (JavaException $e) {
} finally {
    if ($pres != null) $pres->dispose();
}
```

## **Extract Audio**
Aspose.Slides for Java allows developers to extract the sound that is used in slide show transitions associated with slides. To extract the audio, please follow the steps below:

- Create an instance of [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class and load the presentation with slide transitions
- Access the desired slide
- Access the [slideshow transitions](https://apireference.aspose.com/slides/java/com.aspose.slides/IBaseSlide#getSlideShowTransition--) for slide
- Extract the sound in byte data

```php
// Instantiate Presentation class that represents the presentation file
$pres = new Java("com.aspose.slides.Presentation", "AudioSlide.pptx");
try {
    // Access the desired slide
    $slide = $pres->getSlides()->get_Item(0);
    
    // Get the slideshow transition effects for slide
    $transition = $slide->getSlideShowTransition();
    
    //Extract sound in byte array
    $audio = $transition->getSound()->getBinaryData();
    echo("Length: " . $audio->length);
} finally {
    if ($pres != null) $pres->dispose();
}
```