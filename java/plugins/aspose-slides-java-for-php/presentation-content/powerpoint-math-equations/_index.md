---
title: PowerPoint Math Equations
type: docs
weight: 60
url: /java/powerpoint-math-equations/
keywords: " PowerPoint Math Equations, PowerPoint Math Symbols, PowerPoint Formula, PowerPoint Math Text"
description: "PowerPoint Math Equations, PowerPoint Math Symbols, PowerPoint Formula, PowerPoint Math Text"
---

## **Overview**
In PowerPoint, it is possible to write a math equation or formula and display it in the presentation. To do that, various mathematical symbols are represented in PowerPoint and can be added to the text or equation. For that, the math equations constructor is used in PowerPoint, which helps to create complex formulas like:

- Math Fraction
- Math Radical
- Math Function
- Limits and log functions
- N-ary operations
- Matrix
- Large operators
- Sin, cos functions

To add a mathematical equation in PowerPoint, the *Insert -> Equation* menu is used:

![todo:image_alt_text](powerpoint-math-equations_1.png)

This will create a mathematical text in XML that can be displayed in PowerPoint as following: 

![todo:image_alt_text](powerpoint-math-equations_2.png)

PowerPoint supports plenty of mathematical symbols to create math equations. However, creating complicated math equations in PowerPoint often does not bring a good and professional-looking result. Users, who need to create mathematical presentations frequently, resort to the use of third-party solutions to create good-looking math formulas.

Using [**Aspose.Slide API**](https://products.aspose.com/slides/java), you can work with math equations in the PowerPoint presentations programmatically in C#. Create new math expressions or edit previously created ones. The export of mathematical structures into images is also partially supported.


## **How to Create a Mathematical Equation**
Mathematical elements are used for building any mathematical constructions with any level of nesting. A linear collection of mathematical elements forms a mathematical block represented by the [**MathBlock**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathBlock) class. [**MathBlock**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathBlock) class essentially is a separated mathematical expression, formula, or equation. [**MathPortion**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathPortion) is a mathematical portion, used to hold mathematical text (do not mix with [**Portion**](https://apireference.aspose.com/slides/java/com.aspose.slides/Portion)). [**MathParagraph**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathParagraph) allows manipulating a set of math blocks. The abovementioned classes are the key to work with PowerPoint math equations via Aspose.Slides API.

Let's see how we can create the following mathematical equation via Aspose.Slides API:

![todo:image_alt_text](powerpoint-math-equations_3.png)

To add a mathematical expression on the slide, first, add a shape that will contain the mathematical text:

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $mathShape = $pres->getSlides()->get_Item(0)->getShapes()->addMathShape(0, 0, 720, 150);
} finally {
    if ($pres != null) $pres->dispose();
}
``` 

After creating, the shape will already contain one paragraph with a mathematical portion by default. The [**MathPortion**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathPortion) class is a portion that contains a mathematical text inside. To access mathematical content inside [**MathPortion**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathPortion), refer to the [**MathParagraph** ](https://apireference.aspose.com/slides/java/com.aspose.slides/MathParagraph)variable:

```php
$mathParagraph = ($mathShape->getTextFrame()->getParagraphs()->get_Item(0)->getPortions()->get_Item(0))->getMathJava("com.aspose.slides.Paragraph");
``` 

The [**MathParagraph**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathParagraph) class allows to read, add, edit and delete math blocks ([**MathBlock**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathBlock)), that consist of a combination of mathematical elements. For example, create a fraction and place it in the presentation:

```php
$fraction = new Java("com.aspose.slides.MathematicalText", "x")->divide("y");

$mathParagraph->add(new Java("com.aspose.slides.MathBlock", $fraction));
``` 

Each mathematical element is represented by some class that implements the [**IMathElement**](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement) interface. This interface provides a lot of methods for easily creating mathematical expressions. You can create a fairly complex mathematical expression with a single line of code. For example, the Pythagorean theorem would look like this:

```php
$mathBlock = new Java("com.aspose.slides.MathematicalText", "c")
        ->setSuperscript("2")
        ->join("=")
        ->join(new Java("com.aspose.slides.MathematicalText", "a")->setSuperscript("2"))
        ->join("+")
        ->join(new Java("com.aspose.slides.MathematicalText", "b")->setSuperscript("2"));
``` 

Operations of the interface [**IMathElement**](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement) are implemented in any type of element, including the [**MathBlock**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathBlock).

The full source code sample:

```php
$pres = new Java("com.aspose.slides.Presentation");
try {
    $mathShape = $pres->getSlides()->get_Item(0)->getShapes()->addMathShape(0, 0, 720, 150);

    $mathParagraph = ($mathShape->getTextFrame()->getParagraphs()->get_Item(0)->getPortions()->get_Item(0))->getMathJava("com.aspose.slides.Paragraph");
    
    $fraction = new Java("com.aspose.slides.MathematicalText", "x")->divide("y");

    $mathParagraph->add(new Java("com.aspose.slides.MathBlock", $fraction));

    $mathBlock = new Java("com.aspose.slides.MathematicalText", "c")
            ->setSuperscript("2")
            ->join("=")
            ->join(new Java("com.aspose.slides.MathematicalText", "a")->setSuperscript("2"))
            ->join("+")
            ->join(new Java("com.aspose.slides.MathematicalText", "b")->setSuperscript("2"));
    $mathParagraph->add($mathBlock);

    $pres->save("math.pptx", Java("com.aspose.slides.SaveFormat")->Pptx);
} finally {
    if ($pres != null) $pres->dispose();
}
``` 

## **Mathematical Element Types**
Mathematical expressions are formed from sequences of mathematical elements. The sequence of mathematical elements is represented by a mathematical block, and arguments of mathematical elements form a tree-like nesting.

There are a lot of mathematical element types that can be used to construct a mathematical block. Each of these elements can be included (aggregated) in another element. That is, elements are actually containers for others, forming a tree-like structure. The simplest type of element that does not contain other elements of the mathematical text.

Each type of math element implements the [**IMathElement** ](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement)interface, allowing the use of the common set of math operations on different types of math elements.
### **MathematicalText class**
The [**MathematicalText**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathematicalText) class represents a mathematical text - the underlying element of all mathematical constructions. Mathematical text may represent operands and operators, variables, and any other linear text.

Example: 𝑎=𝑏+𝑐
### **MathFraction class**
[**MathFraction**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathFraction) class specifies the fraction object, consisting of a numerator and denominator separated by a fraction bar. The fraction bar can be horizontal or diagonal, depending on the fraction properties. The fraction object is also used to represent the stack function, which places one element above another, with no fraction bar.

Example:

![todo:image_alt_text](powerpoint-math-equations_4.png)
### **MathRadical class**
[**MathRadical**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathRadical) class specifies the radical function (mathematical root), consisting of a base, and an optional degree.

Example:

![todo:image_alt_text](powerpoint-math-equations_5.png)
### **MathFunction class**
[**MathFunction**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathFunction) class specifies a function of an argument. Contains properties: [getName](https://apireference.aspose.com/slides/java/com.aspose.slides/MathFunction#getName--) - function name and [getBase](https://apireference.aspose.com/slides/java/com.aspose.slides/MathFunction#getBase--) - function argument.

Example:

![todo:image_alt_text](powerpoint-math-equations_6.png)
### **MathNaryOperator class**
[**MathNaryOperator**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathNaryOperator) class specifies an N-ary mathematical object, such as Summation and Integral. It consists of an operator, a base (or operand), and optional upper and lower limits. Examples of N-ary operators are Summation, Union, Intersection, Integral.

This class does not include simple operators such as addition, subtraction, and so on. They are represented by a single text element - [MathematicalText](https://apireference.aspose.com/slides/java/com.aspose.slides/MathematicalText).

Example:

![todo:image_alt_text](powerpoint-math-equations_7.png)
### **MathLimit class**
[**MathLimit**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathLimit) class creates the upper or lower limit. It specifies the limit object, consisting of text on the baseline and reduced-size text immediately above or below it. This element does not include the word “lim", but allows you to place text at the top or at the bottom of the expression. So, the expression 

![todo:image_alt_text](powerpoint-math-equations_8.png)

is created using a combination of [**MathFunction**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathFunction) and [**MathLimit**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathLimit) elements this way:

```php
$funcName = new Java("com.aspose.slides.MathLimit")->new Java("com.aspose.slides.MathematicalText", "lim"), new Java("com.aspose.slides.MathematicalText", "𝑥→∞"));

$mathFunc = new Java("com.aspose.slides.MathFunction")->$funcName, new Java("com.aspose.slides.MathematicalText", "𝑥"));
``` 


### **MathSubscriptElement, MathSuperscriptElement, MathRightSubSuperscriptElement, MathLeftSubSuperscriptElement classes**
- [MathSubscriptElement](https://apireference.aspose.com/slides/java/com.aspose.slides/MathSubscriptElement)
- [MathSuperscriptElement](https://apireference.aspose.com/slides/java/com.aspose.slides/MathSuperscriptElement)
- [MathRightSubSuperscriptElement](https://apireference.aspose.com/slides/java/com.aspose.slides/MathRightSubSuperscriptElement)
- [MathLeftSubSuperscriptElement](https://apireference.aspose.com/slides/java/com.aspose.slides/MathLeftSubSuperscriptElement)

The following classes specify a lower index or an upper index. You can set subscript and superscript at the same time on the left or on the right side of an argument, but single subscript or superscript is supported on the right side only. The [MathSubscriptElement](https://apireference.aspose.com/slides/java/com.aspose.slides/MathSubscriptElement) can also be used to set the mathematical degree of a number.

Example: 

![todo:image_alt_text](powerpoint-math-equations_9.png)
### **MathMatrix class**
[**MathMatrix**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathMatrix) class specifies the Matrix object, consisting of child elements laid out in one or more rows and columns. It is important to note that matrixes do not have built-in delimiters. To place the matrix in the brackets you should use the delimiter object - [**IMathDelimiter**](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathDelimiter). Null arguments can be used to create gaps in matrices.

Example: 

![todo:image_alt_text](powerpoint-math-equations_10.png)
### **MathArray class**
[**MathArray**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathArray) class specifies a vertical array of equations or any mathematical objects.

Example: 

![todo:image_alt_text](powerpoint-math-equations_11.png)
### **Formatting Mathematical Elements**
- [**MathBorderBox**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathBorderBox) class: draws a rectangular or some other border around the [**IMathElement**](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement).
  
  Example: ![todo:image_alt_text](powerpoint-math-equations_12.png)

- [**MathBox**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathBox) class: specifies the logical boxing (packaging) of the mathematical element. For example, a boxed object can serve as an operator emulator with or without an alignment point, serve as a line breakpoint, or be grouped such as not to allow line breaks within. For example, the "==" operator should be boxed to prevent line breaks.
- [**MathDelimiter**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathDelimiter) class: specifies the delimiter object, consisting of opening and closing characters (such as parentheses, braces, brackets, and vertical bars), and one or more mathematical elements inside, separated by a specified character. Examples: (𝑥2); [𝑥2|𝑦2].
  
  Example: ![todo:image_alt_text](powerpoint-math-equations_13.png)

- [**MathAccent**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathAccent) class: specifies the accent function, consisting of a base and a combining diacritical mark. 

  Example: 𝑎́.

- [**MathBar**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathBar) class: specifies the bar function, consisting of a base argument and an overbar or underbar.
  
  Example: ![todo:image_alt_text](powerpoint-math-equations_14.png)

- [**MathGroupingCharacter**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathGroupingCharacter) class: specifies a grouping symbol above or below an expression, usually to highlight the relationships between elements.
  
  Example: ![todo:image_alt_text](powerpoint-math-equations_15.png)


## **Mathematical Operations**
Each mathematical element and mathematical expression (via [**MathBlock**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathBlock)) implements the [**IMathElement** ](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement)interface. It allows you to use operations on the existing structure and form more complex mathematical expressions. All operations have two parameter sets: either [**IMathElement** ](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement)or string as arguments. Instances of the [**MathematicalText** ](https://apireference.aspose.com/slides/java/com.aspose.slides/MathematicalText)class are implicitly created from specified strings when string arguments are used. Math operations available in Aspose.Slides are listed below.
### **Join method**
- [join(String)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#join-java.lang.String-)
- [join(IMathElement)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#join-com.aspose.slides.IMathElement-)

Joins a mathematical element and forms a mathematical block. For example:

```php
$element1 = new Java("com.aspose.slides.MathematicalText", "x");

$element2 = new Java("com.aspose.slides.MathematicalText", "y");

$block = element1->join($element2);
``` 

### **Divide method**
- [divide(String)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#divide-java.lang.String-)
- [divide(IMathElement)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#divide-com.aspose.slides.IMathElement-)
- [divide(String, MathFractionTypes)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#divide-java.lang.String-int-)
- [divide(IMathElement, MathFractionTypes)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#divide-com.aspose.slides.IMathElement-int-)

Creates a fraction of the specified type with this numerator and specified denominator. For example:

```php
$numerator = new Java("com.aspose.slides.MathematicalText", "x");

$fraction = $numerator->divide("y", Java("com.aspose.slides.MathFractionTypes")->Linear);
``` 

### **Enclose method**
- [enclose()](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#enclose--)
- [enclose(Char, Char)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#enclose-char-char-)

Encloses the element in specified characters such as parenthesis or another character as framing.

```php
/**
 * <p>
 * Enclose a math element in parenthesis
 * </p>
 */
public $enclose();

/**
 * <p>
 * Encloses this element in specified characters such as parenthesis or another characters as framing
 * </p>
 */
public $enclose($beginningCharacter, $endingCharacter);
``` 


For example:

```php
$delimiter = new Java("com.aspose.slides.MathematicalText", "x")->enclose('[', ']');

$delimiter2 = new Java("com.aspose.slides.MathematicalText", "elem1")->join("elem2")->enclose();
``` 

### **Function method**
- [function(String)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#function-java.lang.String-)
- [function(IMathElement)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#function-com.aspose.slides.IMathElement-)

Takes a function of an argument using the current object as the function name.

```php
/**
 * <p>
 * Takes a function of an argument using this instance as the function name
 * </p>
 */
public $function($functionArgument);

/**
 * <p>
 * Takes a function of an argument using this instance as the function name
 * </p>
 */
public $function($functionArgument);
``` 


For example:

```php
$func = new Java("com.aspose.slides.MathematicalText", "sin")->function("x");
``` 

### **AsArgumentOfFunction method**
- [asArgumentOfFunction(String)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#asArgumentOfFunction-java.lang.String-)
- [asArgumentOfFunction(IMathElement)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#asArgumentOfFunction-com.aspose.slides.IMathElement-)
- [asArgumentOfFunction(MathFunctionsOfOneArgument)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#asArgumentOfFunction-int-)
- [asArgumentOfFunction(MathFunctionsOfTwoArguments, IMathElement)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#asArgumentOfFunction-int-com.aspose.slides.IMathElement-)
- [asArgumentOfFunction(MathFunctionsOfTwoArguments, String)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#asArgumentOfFunction-int-java.lang.String-)

Takes the specified function using the current instance as the argument. You can:

- specify a string as the function name, for example “cos”.
- select one of the predefined values of the enumerations [**MathFunctionsOfOneArgument**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathFunctionsOfOneArgument) or [**MathFunctionsOfTwoArguments**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathFunctionsOfTwoArguments), for example [**MathFunctionsOfOneArgument**](MathFunctionsOfOneArgument).[**ArcSin**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathFunctionsOfOneArgument#ArcSin).
- select the instance of the [**IMathElement**](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement).

For example:

```php
$funcName = new Java("com.aspose.slides.MathLimit")->new Java("com.aspose.slides.MathematicalText", "lim"), new Java("com.aspose.slides.MathematicalText", "𝑛→∞"));

$func1 = new Java("com.aspose.slides.MathematicalText", "2x")->asArgumentOfFunction($funcName);

$func2 = new Java("com.aspose.slides.MathematicalText", "x")->asArgumentOfFunction("sin");

$func3 = new Java("com.aspose.slides.MathematicalText", "x")->asArgumentOfFunction(Java("com.aspose.slides.MathFunctionsOfOneArgument")->Sin);

$func4 = new Java("com.aspose.slides.MathematicalText", "x")->asArgumentOfFunction(Java("com.aspose.slides.MathFunctionsOfTwoArguments")->Log, "3");
``` 

### **SetSubscript, SetSuperscript, SetSubSuperscriptOnTheRight, SetSubSuperscriptOnTheLeft methods**
- [setSubscript(String)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#setSubscript-java.lang.String-)
- [setSubscript(IMathElement)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#setSubscript-com.aspose.slides.IMathElement-)
- [setSuperscript(String)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#setSuperscript-java.lang.String-)
- [setSuperscript(IMathElement)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#setSuperscript-com.aspose.slides.IMathElement-)
- [setSubSuperscriptOnTheRight(String, String)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#setSubSuperscriptOnTheRight-java.lang.String-java.lang.String-)
- [setSubSuperscriptOnTheRight(IMathElement, IMathElement)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#setSubSuperscriptOnTheRight-com.aspose.slides.IMathElement-com.aspose.slides.IMathElement-)
- [setSubSuperscriptOnTheLeft(String, String)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#setSubSuperscriptOnTheLeft-java.lang.String-java.lang.String-)
- [setSubSuperscriptOnTheLeft(IMathElement, IMathElement)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#setSubSuperscriptOnTheLeft-com.aspose.slides.IMathElement-com.aspose.slides.IMathElement-)

Sets subscript and superscript. You can set subscript and superscript at the same time on the left or on the right side of the argument, but single subscript or superscript is supported only on the right side. The **Superscript** can also be used to set the mathematical degree of a number.

Example:

```php
$script = new Java("com.aspose.slides.MathematicalText", "y")->setSubSuperscriptOnTheLeft("2x", "3z");
``` 

### **Radical method**
- [radical(String)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#radical-java.lang.String-)
- [radical(IMathElement)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#radical-com.aspose.slides.IMathElement-)

Specifies the mathematical root of the given degree from the specified argument.

Example:

```php
$radical = new Java("com.aspose.slides.MathematicalText", "x")->radical("3");
``` 

### **SetUpperLimit and SetLowerLimit methods**
- [setUpperLimit(String)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#setUpperLimit-java.lang.String-)
- [setUpperLimit(IMathElement)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#setUpperLimit-com.aspose.slides.IMathElement-)
- [setLowerLimit(String)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#setLowerLimit-java.lang.String-)
- [setLowerLimit(IMathElement)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#setLowerLimit-com.aspose.slides.IMathElement-)

Takes the upper or lower limit. Here, the upper and bottom simply indicate the location of the argument relative to the base.

Let's consider an expression: 

![todo:image_alt_text](powerpoint-math-equations_8.png)

Such expressions can be created through a combination of classes [MathFunction](https://apireference.aspose.com/slides/java/com.aspose.slides/MathFunction) and [MathLimit](https://apireference.aspose.com/slides/java/com.aspose.slides/MathLimit), and operations of the [IMathElement](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement) as follows:

```php
$mathExpression = new Java("com.aspose.slides.MathematicalText", "lim")->setLowerLimit("x→∞")->function("x");
``` 

### **Nary and Integral methods**
- [nary(MathNaryOperatorTypes, IMathElement, IMathElement)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#nary-int-com.aspose.slides.IMathElement-com.aspose.slides.IMathElement-)
- [nary(MathNaryOperatorTypes, String, String)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#nary-int-java.lang.String-java.lang.String-)
- [integral(MathIntegralTypes)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#integral-int-)
- [integral(MathIntegralTypes, IMathElement, IMathElement)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#integral-int-com.aspose.slides.IMathElement-com.aspose.slides.IMathElement-)
- [integral(MathIntegralTypes, String, String)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#integral-int-java.lang.String-java.lang.String-)
- [integral(MathIntegralTypes, IMathElement, IMathElement, MathLimitLocations)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#integral-int-com.aspose.slides.IMathElement-com.aspose.slides.IMathElement-int-)
- [integral(MathIntegralTypes, String, String, MathLimitLocations)](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#integral-int-java.lang.String-java.lang.String-int-)

Both **nary** and **integral** methods create and return the N-ary operator represented by the [**IMathNaryOperator**](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathNaryOperator) type. In nary method, the [**MathNaryOperatorTypes**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathNaryOperatorTypes) enumeration specifies the type of operator: summation, union, etc., not including integrals. In Integral method, there is the specialized operation Integral with the enumeration of integral types [**MathIntegralTypes**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathIntegralTypes). 

Example:

```php
$baseArg = new Java("com.aspose.slides.MathematicalText", "x")->join(new Java("com.aspose.slides.MathematicalText", "dx")->toBox());

$integral = baseArg->integral(Java("com.aspose.slides.MathIntegralTypes")->Simple, "0", "1");
``` 

### **ToMathArray method**
[**toMathArray**](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#toMathArray--) puts elements in a vertical array. If this operation is called for a [**MathBlock**](https://apireference.aspose.com/slides/java/com.aspose.slides/MathBlock) instance, all child elements will be placed in the returned array.

Example:

```php
$arrayFunction = new Java("com.aspose.slides.MathematicalText", "x")->join("y")->toMathArray();
``` 

### **Formatting operations: Accent, Overbar, Underbar, Group, ToBorderBox, ToBox**
- [**accent**](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#accent-char-) method sets an accent mark (a character on the top of the element).
- [**overbar**](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#overbar--) and [**underbar**](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#underbar--) methods set a bar on the top or bottom.
- [**group**](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#group--) method places in a group using a grouping character such as a bottom curly bracket or another.
- [**toBorderBox**](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#toBorderBox--) method places in a border-box.
- [**toBox**](https://apireference.aspose.com/slides/java/com.aspose.slides/IMathElement#toBox--) method places in a non-visual box (logical grouping).

Examples:

```php
$accent = new Java("com.aspose.slides.MathematicalText", "x")->accent('\u0303');

$bar = new Java("com.aspose.slides.MathematicalText", "x")->overbar();

$groupChr = new Java("com.aspose.slides.MathematicalText", "x")->join("y")->join("z")->group('\u23E1', Java("com.aspose.slides.MathTopBotPositions")->Bottom, Java("com.aspose.slides.MathTopBotPositions")->Top);

$borderBox = new Java("com.aspose.slides.MathematicalText", "x+y+z")->toBorderBox();

$boxedOperator = new Java("com.aspose.slides.MathematicalText", ":=")->toBox();
``` 
