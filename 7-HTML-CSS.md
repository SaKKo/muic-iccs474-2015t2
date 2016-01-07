# ICCS474
## Internet Programming

### HTML

- Hyper Text Markup Language.

    HTML is a markup language that is used to create a website.

    A Web browser can read HTML files and compose them into visible or audible Web pages. The browser does not display the HTML tags and scripts, but uses them to interpret the content of the page. HTML describes the structure of a Website semantically along with cues for presentation, making it a markup language, rather than a programming language.

    It uses a angle brackets `<>` and almost all the times come in pair.

    HTML Syntax example

    ```html
    <h1>Hello World</h1> <!-- h1 stands for HEADING 1 -->
    ```

#### Preview

> <h1>Hello World</h1>

- Is it sufficient by just typing `<h1>Hello World</h1>`?

#### Some other HTML tags example

    <h?> ... </h?>               <!-- Heading replace ? with 1 to 6 -->
    <p> ... </p>                 <!-- Paragraph of Text -->
    <b> ... </b>                 <!-- Bold Text -->
    <a href="url"> ... </a>      <!-- Basic Link -->
    <i> ... </i>                 <!-- Italic Text -->
    <u> ... </u>                 <!-- Underline Text -->
    <strike> ... </strike>       <!-- Strikeout -->
    <sup> ... </sup>             <!-- Superscript -->
    <sub> ... </sub>             <!-- Subscript -->
    <small> ... </small>         <!-- Small - Fineprint size text -->
    <blockquote> ... </blockquote>  <!-- Text Block Quote -->
    <strong> ... </strong>       <!-- Strong - Shown as Bold in most browsers -->
    <font> ... </font>           <!-- Font tag obsolete, use CSS. (*) -->
    <div> ... </div>             <!-- Division (or Section) of Page Content -->
    <br>                         <!-- Line Break -->
    <hr>                         <!-- Basic Horizontal Line -->

#### Full HTML file content should look like this.

    <!DOCTYPE html>
    <html>
      <head>
        <title>Page Title</title>
      </head>
      <body>

        <h1>Hello world</h1>

      </body>
    </html>

- The DOCTYPE declaration defines the document type to be HTML
- The text between `<html>` and `</html>` describes an HTML document
- The text between `<head>` and `</head>` provides information about the document
- The text between `<title>` and `</title>` provides a title for the document
- The text between `<body>` and `</body>` describes the visible page content
- The text between `<h1>` and `</h1>` describes a heading
- The text between `<p>` and `</p>` describes paragraph

> #### NOTE
> - We keep our HTML well formed. It means, whenever you started a `<TAG>` you always have to close it with `</TAG>`.
> - Browsers will always truncate spaces in HTML pages.

        `<h1>hello world</h1>`
        `<h1>hello        world</h1>`

> - Both will have the same results when it is shown on browsers.
>       - Is there a downside to this?
> - Browser will always predict `<` or `>` as a start or an end of an html tag.
>       - eg. This code is not well formed `<Hello World`
>       - If you ever need to render these special character. We use **Character Entities**
>               - `&entity_name;` or `&#entity_number;`
>               - Example, `&nbsp;` is equal to 1 blank space.
>       - These are some examples of HTML reserved characters in Character entities format.

|Result|Description|&amp+EntityName+;|&+EntityNumber+;|
|:---:|:---|:---:|:---:|
| |non breaking space|`&nbsp;`|`&#160;`|
|<|less than|`&lt;`|`&#60;`|
|>|greater than|`&gt;`|`&#62;`|
|&|ampersand|`&amp;`|`&#38;`|
|¢|cent|`&cent;`|`&#162;`|
|£|pound|`&pound;`|`&#163;`|
|¥|yen|`&yen;`|`&#165;`|
|€|euro|`&euro;`|`&#8364;`|
|©|copyright|`&copy;`|`&#169;`|
|®|registered trademark|`&reg;`|`&#174;`|

> - Is HTML a programming language? Why or why not?
>       - HTML is a tag based syntax which is used to hold contents and page information. It usually does not contain any calculation nor styling.

#### HTML Attributes

    <sakko firstname="tanasak" lastname="tantitarntong">I am awesome.</sakko>

- `sakko` is called `html tag`
- `firstname` and `lastname` are attributes.
- `tanasak` and `tantitarntong` are attribute values.
- `I am awesome.` is content or innerHTML of `sakko` tag.

#### CSS

CSS stands for Cascading Style Sheets

    - CSS describes how HTML elements are to be displayed on screen, paper, or in other media
    - CSS saves a lot of work. It can control the layout of multiple web pages all at once
    - External stylesheets are stored in CSS files

Why Use CSS?

CSS is used to define styles for your web pages, including the design, layout and variations in display for different devices and screen sizes.

CSS Solved a Big Problem

HTML was NEVER intended to contain tags for formatting a web page!

HTML was created to describe the content of a web page, like:

`<h1>This is a heading</h1>`

`<p>This is a paragraph.</p>`

When tags like `<font>`, and color attributes were added to the HTML 3.2 specification, it started a nightmare for web developers. Development of large websites, where fonts and color information were added to every single page, became a long and expensive process.

To solve this problem, the World Wide Web Consortium (W3C) created CSS.

> CSS removed the style formatting from the HTML page!

Here is how to use CSS

![Image](https://raw.githubusercontent.com/SaKKo/muic-iccs474-2015t2/master/assets/css-selector.png)

```css

/* <p>Hello</p> */
p {   
    color: red;
    text-align: center;
}

/* <p id='center'>Hello</p> */
#center {
    text-align: center;
    color: red;
}

/* <p class='center'>Hello</p> */
.center {
    text-align: center;
    color: red;
}

/* <h1 class='center'>Hello</h1> */
/* Will only select .center that is in tag h1 */
h1.center {
    text-align: center;
    color: red;
}

/* <h1><p class='center'>Hello</p></h1> */
/* Will only select .center that is inside of h1 */
h1 .center {
    text-align: center;
    color: red;
}
```

Let's checkout bootstrap which will make your life a lot easier.

http://getbootstrap.com/

#### HTML & CSS Exercise

https://github.com/SaKKo/muic-iccs474-2015t2-exercise-html
