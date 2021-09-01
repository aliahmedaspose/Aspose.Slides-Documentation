---
title: Presentation Comments
type: docs
weight: 100
url: /java/presentation-comments/
keywords: "PowerPoint presentation comments"
description: "Add PowerPoint comments and reply presentation comments in Java."
---

Slide comment is like an annotation in PDF file or a note that one can attach with a slide. Slide comments are generally used while reviewing the slides in PowerPoint. However, they can also serve as a useful utility for highlighting something important in the presentation slide and giving the needed explanation for that.
## **Add Slide Comment**
In Aspose.Slides for Java, the presentation slide comment are associated with a particular author. The [Presentation](https://apireference.aspose.com/slides/java/com.aspose.slides/Presentation) class holds the collection of authors in [**ICommentAuthorCollection**](https://apireference.aspose.com/slides/java/com.aspose.slides/ICommentAuthorCollection) that are responsible for adding slide comments. For each author, there is a collection of comments in [**ICommentCollection**](https://apireference.aspose.com/slides/java/com.aspose.slides/ICommentCollection). The [**IComment**](https://apireference.aspose.com/slides/java/com.aspose.slides/IComment) class includes information like an author who added slide comment, time of creation, slide where a comment is added, the position of slide comment on the selected slide and the comment text. The [**CommentAuthor**](https://apireference.aspose.com/slides/java/com.aspose.slides/CommentAuthor) class includes the author's name, his initials and list of associated comments. In the following example, we have added the code snippet for adding the slide comments.

```php
// Instantiate Presentation class
$presentation = new Java("com.aspose.slides.Presentation");
try {
    // Adding Empty slide
    $presentation->getSlides()->addEmptySlide(presentation->getLayoutSlides()->get_Item(0));

    // Adding Author
    $author = $presentation->getCommentAuthors()->addAuthor("Jawad", "MF");

    // Position of comments
    $point = Java("java.awt.geom.Point2D")->Float(0.2f, 0.2f);

    // Adding slide comment for an author on slide 1
    $author->getComments()->addComment("Hello Jawad, this is slide comment", $presentation->getSlides()->get_Item(0), point, new Java("java.util.Date"));

    // Adding slide comment for an author on slide 1
    $author->getComments()->addComment("Hello Jawad, this is second slide comment", $presentation->getSlides()->get_Item(1), point, new Java("java.util.Date"));

    // Accessing ISlide 1
    $slide = $presentation->getSlides()->get_Item(0);

    // if null is passed as an argument then it will bring comments from all authors on selected slide
    $comments = $slide->getSlideComments(author);

    // Accessin the comment at index 0 for slide 1
    $str = comments[0]->getText();

    $presentation->save("Comments_out.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);

    if ($comments->length > 0)
    {
        // Select comments collection of Author at index 0
        $commentCollection = comments[0]->getAuthor()->getComments();
        $comment = commentCollection->get_Item(0)->getText();
    }
} finally {
    $presentation->dispose();
}
```

## **Access Slide Comments**
In the following example, we will learn how to access the existing slide comments and can even modify the comments as well.

```php
// Instantiate a Presentation class that represents the presentation file
$presentation = new Java("com.aspose.slides.Presentation"), "Comments1.pptx");
try {
    for ($commentAuthor : $presentation->getCommentAuthors())
    {
        $author = commentAuthor;
        for ($comment1 : $author->getComments())
        {
            $comment = comment1;
            echo("ISlide :" + $comment->getSlide()->getSlideNumber() + " has comment: " + $comment->getText() + 
                    " with Author: " + $comment->getAuthor()->getName() + " posted on time :" + $comment->getCreatedTime() + "\n");
        }
    }
} finally {
    $presentation->dispose();
}
```

## **Reply Comments**
New methods [**getParentComment**](https://apireference.aspose.com/slides/java/com.aspose.slides/IComment#getParentComment--) and [**setParentComment**](https://apireference.aspose.com/slides/java/com.aspose.slides/IComment#setParentComment-com.aspose.slides.IComment-) have been added to [**IComment**](https://apireference.aspose.com/slides/java/com.aspose.slides/IComment) interface and [**Comment**](https://apireference.aspose.com/slides/java/com.aspose.slides/Comment) class in Aspose.Slides for Java. It allows to get or set the parent comment, thus creating a dialog in the form of a hierarchy of comments and replies.

The code snippet below shows a sample of adding some comments and some replies to them:

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    // Add comment
    $author1 = $pres->getCommentAuthors()->addAuthor("Author_1", "A.A.");
    $comment1 = $author1->getComments()->addComment("comment1", $pres->getSlides()->get_Item(0), Java("java.awt.geom.Point2D")->Float(10, 10), new Java("java.util.Date"));

    // Add reply for comment1
    $author2 = $pres->getCommentAuthors()->addAuthor("Autror_2", "B.B.");
    $reply1 = $author2->getComments()->addComment("reply 1 for comment 1", $pres->getSlides()->get_Item(0), Java("java.awt.geom.Point2D")->Float(10, 10), new Java("java.util.Date"));
    $reply1->setParentComment($comment1);

    // Add reply for comment1
    $reply2 = $author2->getComments()->addComment("reply 2 for comment 1", $pres->getSlides()->get_Item(0),  Java("java.awt.geom.Point2D")->Float(10, 10), new Java("java.util.Date"));
    reply2->setParentComment($comment1);

    // Add reply to reply
    $subReply = $author1->getComments()->addComment("subreply 3 for reply 2", $pres->getSlides()->get_Item(0),  Java("java.awt.geom.Point2D")->Float(10, 10), new Java("java.util.Date"));
    $subReply->setParentComment($reply2);

    $comment2 = $author2->getComments()->addComment("comment 2", $pres->getSlides()->get_Item(0), Java("java.awt.geom.Point2D")->Float(10, 10), new Java("java.util.Date"));
    $comment3 = $author2->getComments()->addComment("comment 3", $pres->getSlides()->get_Item(0), Java("java.awt.geom.Point2D")->Float(10, 10), new Java("java.util.Date"));

    $reply3 = $author1->getComments()->addComment("reply 4 for comment 3", $pres->getSlides()->get_Item(0), Java("java.awt.geom.Point2D")->Float(10, 10), new Java("java.util.Date"));
    reply3->setParentComment(comment3);

    // Display hierarchy on console
    $slide = $pres->getSlides()->get_Item(0);
    $comments = $slide->getSlideComments(null);
    for ($i = 0; i < $comments->length; i++)
    {
        $comment = comments[i];
        while ($comment->getParentComment() != null)
        {
            echo("\t");
            $comment = $comment->getParentComment();
        }

        echo($comments[i]->getAuthor()->getName() +  " : " + $comments[i]->getText());
        echo();
    }
    $pres->save("parent_comment.pptx",Java("com.aspose.slides.SaveFormat")->Pptx);
    // Remove comment1 and all its replies
    $comment1->remove();

    $pres->save("remove_comment.pptx",Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
```

**Attention: remove** method of [**IComment**](https://apireference.aspose.com/slides/java/com.aspose.slides/IComment) interface removes the comment with all its replies.

**NOTE:** If setting [**setParentComment**](https://apireference.aspose.com/slides/java/com.aspose.slides/IComment#setParentComment-com.aspose.slides.IComment-) leads to a circular reference, the exception of type [**PptxEditException**](https://apireference.aspose.com/slides/java/com.aspose.slides/PptxEditException) will be thrown.
