---
title: Redacting Texts
type: docs
weight: 30
url: /net/redacting-texts/

---

# Redacting Texts in Slides

Aspose.Slides for .NET allows you to hide texts in slides through the redact function. For example, when you have sensitive or confidential details in a presentation you plan to show an audience, you can redact the details to prevent people from seeing them. 

{{% alert color="primary" %}} 

You can use our [online Text Redaction App](https://products.aspose.app/slides/redaction) to see how Aspose.Slides redacts texts in slides. 

{{% /alert %}} 

This sample code shows you how to redact a text in a slide:

```c#
using (Presentation pres = new Presentation("pres.pptx"))
{
    const string toRedact = "bKIM";
    string stub = new string(' ', toRedact.Length);

    foreach (ISlide slide in pres.Slides)
    {
        ITextFrame[] textFrames = SlideUtil.GetAllTextBoxes(slide);
        foreach (ITextFrame textFrame in textFrames)
        {
            textFrame.Text = textFrame.Text.Replace(toRedact, stub);
            textFrame.HighlightText(stub, Color.Black);
        }
    }

    pres.Save("pres-edited.pptx", SaveFormat.Pptx);
}
```





