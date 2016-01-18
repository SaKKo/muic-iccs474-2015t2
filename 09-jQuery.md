# ICCS474
## Internet Programming

## Javascript - jQuery

http://jquery.com/

Download latest version

Create a new project

Import it to your project

```js
<!DOCTYPE html>
<html>
  <head>
  </head>
  <body>
    <script src="vendors/jquery/jquery-2.1.3.min.js"></script>
  </body>
</html>
```


## Introduction

jQuery is a fast, small, and feature-rich JavaScript library. It makes things like HTML document traversal and manipulation, event handling, animation, and Ajax much simpler with an easy-to-use API that works across a multitude of browsers. With a combination of versatility and extensibility, jQuery has changed the way that millions of people write JavaScript.

You can use jQuery simply by using this command

```js
jQuery
//or
$
```

## Simple usage

Listening to events

```js
$(document).ready(function(){
  console.log('executes when HTML-Document is
  loaded and DOM is ready')
});

$(window).load(function(){
  console.log('executes when complete page is fully loaded,
  including all frames, objects and images')
});
```

> DOM - Document Object Model - is a cross-platform and language-independent convention for representing and interacting with objects in HTML, XHTML, and XML documents

## Why jQuery?

There are lots of other JavaScript frameworks out there, but jQuery seems to be the most popular, and also the most extendable.

Though there are many people who's against using jQuery these days. It's still provide a lot of good example with clean code.

Many of the biggest companies on the Web use jQuery, such as:

- Google
- Microsoft
- IBM
- Netflix

jQuery also works on almost all browsers. The jQuery team knows all about cross-browser issues, and they have written this knowledge into the jQuery library. jQuery will run exactly the same in all major browsers. Read jQuery documentation first!


## Where to import jQuery?

In many older tutorials, jQuery are usually loaded in HEAD. But the new convention is to load it before `</body>`

Quoting from Yahoo article linked above:

> The problem caused by scripts is that they block parallel downloads. The HTTP/1.1 specification suggests that browsers download no more than two components in parallel per hostname. If you serve your images from multiple hostnames, you can get more than two downloads to occur in parallel. `While a script is downloading, however, the browser won't start any other downloads, even on different hostnames.`

> Why is this important?

### Aren't we all using the same jQuery? same file?

Then why do we need to host it ourself?

- In development, you might want to put everything on your computer. It's faster to load file locally.

> CDN - A content delivery network or content distribution network - a large distributed system of servers deployed in multiple data centers across the Internet. The goal of a CDN is to serve content to end-users with high availability and high performance.

Though there are many providers, I would suggest using Google CDN.

```html
<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.11.2/jquery.min.js"></script>
```
```html
<script src="http://ajax.googleapis.com/ajax/libs/jquery/2.1.3/jquery.min.js"></script>
```

## Javascript special import syntax

Most of the time, when you are hosting your static content website. You wouldn't be using `https` or an SSL protocal.

So you you code would look like this.
```html
<script src="`http`://ajax.googleapis.com/ajax/libs/jquery/2.1.3/jquery.min.js"></script>
```

But if one day you've decided to implement SSL. You will need to change every line of code to be https
```html
<script src="`https`://ajax.googleapis.com/ajax/libs/jquery/2.1.3/jquery.min.js"></script>
```

You can omit `http` or `https` and let the browser choose the appropriate one for you.
```html
<script src="//ajax.googleapis.com/ajax/libs/jquery/2.1.3/jquery.min.js"></script>
```


## jQuery usage

jQuery can be used to query DOM element with css selector.

```js
$("p").hide() // hides all <p> elements.
$(".test").hide() // hides all elements with class="test".
$("#test").hide() // hides the element with id="test".
$("#test").attr("attribute-name") // get attribute from jQuery object
```

`.` represent class, where jquery will query `all` elements with this class name.

`#` represent id, where jqeury will only return the first query that it found from the document.

HTML attribute example
```html
<p attribute-name="test"></p>
```

## jQuery vs JS Query

What are the differences between these 2 query code.

given

```
<p id="test-id"></p>
```

```js
document.getElementById("test-id")
```

```js
$('#test-id')
```

## Exercise

Create a project with this body html.

```html
<body>
  <p id="test-id" class="test-class" my-personal-data="sakko">EL 1</p>
  <p id="test-id" class="test-class">EL 2</p>
  <div id="test-id" class="test-class test-class-1">
    <p id="test-id" class="test-class test-class-2">EL 3</p>
  </div>
  <p id="test-id test-id2" my-personal-data="sakko">EL 4</p>
</body>
```

use jQuery

1. query `EL 1` using id `then` class
1. query `EL 2` using id `then` class
1. query `EL 3` using id `then` class
1. query `EL 4` using id `then` class
1. query `EL 3` using id `and` class
1. query `EL 3` then from `EL 3` `then` query its ancestor `div` by using `.closest()`
1. query `EL 3` then from `EL 3` `then` query its ancestor `body` by using `.closest()`
1. query `div` tag `then` query its child by using `.find()`
1. query `EL 1` `then` get `my-personal-data` attribute


![Image](https://raw.githubusercontent.com/SaKKo/muic-iccs474-2015t2/master/assets/jQuery-cheatsheet.png)

## Other jQuery usage

There are many other useful features from jQuery, for example

```js
var elements = $('.test-class')
$.each(elements,function(i,element){
  console.log(i,element)
});
```

`$.each` can be more useful than normal `for loop`

Read more on jQuery, these functions are very useful.

```js
$.map
$.filter
$.sort
$.join
$.merge
$.split
```

#### Exercise

```js
var arr1 = [1,3,2,3,1,3,2,5,4,3,2]
var arr2 = [4,1,5]
```

1. sort `arr1` (ascending and descending)
1. join `arr1` as csv (after sorted)
1. join `arr1` as csv and split it back to array
1. merge `arr1` and `arr2`
1. add all values in `arr1`

#### Exercise

```js
var arr3 = [{a:10,b:10,c:10},{a:20,b:20,c:20},{a:15,b:15,c:15},{a:40,b:40,c:40},{a:50,b:50,c:50},{a:21,b:21,c:21},{a:25,b:25,c:25}]
```

1. map all `b` values
1. filter `a > 20` and return all hashes
1. map all `c` values from hashes with `b > 20`


## Retrieving data from other sites

Most of the time when you are writing applications. You would want to retrieve data from server after page is loaded.

jQuery provide a way to retrieve data from a URL. For example,

Create a file called `/api/profile.json`
My `/api/profile.json` is hosted with this content.

```js
{"first_name":"SaKKo","last_name":"Sama"}
```

Using AJAX

```js
$.ajax({
  type: "GET",
  url: "/api/profile.json",
  success: function(data){
    console.log(data);
  }
});
```

## AJAX

Asynchronous JavaScript and XML (AJAX) - is not a new programming language, but a new way to use existing standards. It's just a way to exchange data with server.

We will go through the methods of exchanging data with server later when we are working on rails.

From the previous slide, you should see this result in the console.

```js
Object {first_name: "SaKKo", last_name: "Sama"}
```

The result is `Object` not a `string`. Why?


## JSON

Pay attention to the api path

```js
/api/profile.`json`
// {"first_name":"SaKKo","last_name":"Sama"}
```

>Javascript Object Notation (JSON) - a lightweight data-interchange format. It is easy for humans to read and write. It is easy for machines to parse and generate. It is based on a subset of the JavaScript Programming Language, Standard ECMA-262 3rd Edition - December 1999. JSON is a text format that is completely language independent but uses conventions that are familiar to programmers of the C-family of languages, including C, C++, C#, Java, JavaScript, Perl, Python, and many others. These properties make JSON an ideal data-interchange language.


## XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<data>
  <first_name>SaKKo</first_name>
  <last_name>Sama</last_name>
</data>
```

XML stands for EXtensible Markup Language.

It is a markup language so the format looks like `HTML`.


## JSON vs XML

- JSON is a fat free version to exchange data.

- JSON is more human readable.

- JSON is easier to write

- JSON is easier to intregate to Object Oriented Programming.

- XML provide any display capabilities in browser (such as RSS)


## JSON String

Normally, JSON is transported over internet as a `String`

```js
var json_string = "{key1: 'value', key2: ['value1','value2']}"
```

Javascript provides a native way to parse JSON String

```js
var json_object = JSON.parse(json_string)
```

You can convert JSON object back to string by

```js
var json_string_1 = JSON.stringify(json_object)
```

#### Additional topic on JS

When you want to store something in browsers.

```js
if(typeof(Storage) !== "undefined") {
    // Code for localStorage/sessionStorage.
} else {
    // Sorry! No Web Storage support..
}
```

```js
//To save data
localStorage.lastname = "Smith";

//To read data
localStorage.lastname
```

Be warn, you can only store as String. And most browsers only provide `5MB` of local storage.


## To store object or array

saving
```js
var data = {first_name: "Sakko", last_name: "sama"}
localStorage.name = JSON.stringify(data) // will work
```

reading
```js
var data = localStorage.name // you will only get Sting
name = JSON.parse(data) // parse name to object and assign to name again
```
check all local storage data by
```js
console.log(localStorage)
```


## Session Storage

Like Local Storage, you can store any string in Session Storage. However, the sessionStorage object is equal to the localStorage object, except that it stores the data for only one session. The data is deleted when the user closes the browser window.

saving
```js
var data = {first_name: "Sakko", last_name: "sama"}
sessionStorage.name = JSON.stringify(data) // will work
```

reading
```js
var data = sessionStorage.name // you will only get Sting
name = JSON.parse(data) // parse name to object and assign to name again
```
check all session storage data by
```js
console.log(sessionStorage)
```
## Importing jQuery via console

```js
var jq = document.createElement('script');
jq.src = "http://ajax.googleapis.com/ajax/libs/jquery/2.1.3/jquery.min.js";
document.getElementsByTagName('head')[0].appendChild(jq);
jQuery.noConflict();
```
