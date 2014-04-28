#Front-end developer basics


##HTML


###1. What's a doctype do, and how many can you name?

DOCTYPE describes the HTML that will be used in your page. Browsers also use the DOCTYPE to determine how to render a page. Not including a DOCTYPE or including an incorrect DOCTYPE can trigger quirks mode. The kicker here is that quirks mode in IE is quite different from quirks mode in other browsers, meaning that you'll have a much harder job trying to ensure your page works consistently in all browsers if pages are rendered in quirks mode than you will if they are rendered in standards mode.

HTML doctypes:

- `<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">`
- `<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 3.0//EN//">`
- `<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">`
- `<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN">`
- `<!DOCTYPE html>` --> html5

XHTML doctype:

- `<?xml version="1.0" encoding="UTF-8"?>`
- `<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">`

Content type `text/html` gets parsed as HTML, `application/xhtml+xml` gets parsed as XHTML.


###2. HTML vs. XHTML
**HTML** (HyperText Markup Language) is the main markup language for developing web pages and other information that can be displayed in a web browser. The history of HTML at W3C starts with HTML 3.2, code named Wilbur, which was followed a few years later by HTML 4.0, then HTML 4.01. HTML 4.01 is the last version of HTML, and is also the final W3C specification to define the semantics of markup. `Media type: text/html`.

**XHTML** (Extensible HyperText Markup Language) is a family of XML markup languages that mirror or extend versions of the widely used HTML, the language in which web pages are written. XHTML 1.0 was created shortly after HTML 4.01 to help the transition of hypertext to a new generation of mark-up languages for text. XHTML 1.1 is an additional step toward a more flexible version of hypertext with the full benefits of XML architecture and integration of different technologies. `Media type: application/xhtml+xml`.

**Differences in Syntax Rules**:

- XHTML is case-sensitive, HTML is not. All tags and attributes must be lowercase in XHTML.
- XHTML, being XML, must be well-formed. Every element must have an end tag, or use the self-closing tag syntax. HTML allows some end tags and even some start tags to be omitted.
- If an XML parser encounters a well-formedness error, it must abort. An HTML parser is expected to try to salvage what it can and keep going.
- All attributes must have a value in XHTML. HTML allows some attributes (e.g., selected) to be minimised.
- All attribute values must be surrounded by double or single quotes. HTML allows quotes to be omitted if the value contains only alphanumeric characters.
- The comment syntax is more limited in XHTML, but that's rarely an issue for most designers/developers.

**Things You Can Do in XHTML But Not In HTML**:

- Use CDATA sections (`<![CDATA[...]]>`). That's useful if you have content with lots of literal characters that otherwise need to be escaped.
- Use processing instructions, e.g., to link to a style sheet: `<?xml-stylesheet type="text/css" href="style.css" media="screen"?>`
- Include elements from other XML namespaces.
- Use the `&apos;` character entity.

**Things You Can Do in HTML But Cannot Do in XHTML**:

- 'Hide' the contents of `style` or `script` elements with comments (`<!--...-->`).
- Create parts of the page dynamically with JavaScript while the document is still loading (`document.write()`).
- Use named character entities (e.g., `&nbsp;`) other than the four predefined ones: `&lt;`, `&gt;`, `&amp;` and `&quot;`.
- Use the `.innerHTML` property with JavaScript (technically this is non-standard even in HTML).


###3. Strict vs. quirks modes
Modern browsers generally try to render HTML content according to the W3C recommendations. However, to provide compatibility with older web pages, and to provide additional "intuitive" functionality, all browsers support an alternative **quirks mode**. Quirks mode is not, however, a standard. The rendering of any page in quirks mode in different browsers may be different.

In other words, all browsers needed two modes: quirks mode for the old rules, strict mode for the standard.

Choosing which mode to use requires a trigger, and this trigger was found in 'doctype switching'. According to the standards, any (X)HTML document should have a doctype which tells the world at large which flavour of (X)HTML the document is using. Quirks mode is turned on when there is no correct DOCTYPE declaration, and turned off when there is a DOCTYPE definition.

Side note: **JavaScript Strict mode** makes several changes to normal JavaScript semantics. First, strict mode eliminates some JavaScript silent errors by changing them to throw errors. Second, strict mode fixes mistakes that make it difficult for JavaScript engines to perform optimizations: strict mode code can sometimes be made to run faster than identical code that's not strict mode. Third, strict mode prohibits some syntax likely to be defined in future versions of ECMAScript. Strict mode applies to *entire scripts* or to *individual functions* using `"use strict"`.


###4. How do you serve a page with content in multiple languages?

According to the W3C best practices document, the best way to define the language of your HTML and XHTML documents is with an attribute on the html tag.

- HTML: `<html lang="en-US">`
- XHTML: `<html lang="en-US" xml:lang="en-US" xmlns ="http://www.w3.org/1999/xhtml">`


###5. HTML5 structural elements

- `<header>` Used to contain the header content of a site.
- `<footer>` Contains the footer content of a site.
- `<nav>` Contains the navigation menu, or other navigation functionality for the page.
- `<article>` Contains a standalone piece of content that would make sense if syndicated as an RSS item, for example a news item.
- `<section>` Used to either group different articles into different purposes or subjects, or to define the different sections of a single article.
- `<aside>` Defines a block of content that is related to the main content around it, but not central to the flow of it.


###6. DOM structure

- How nodes are related to one another:
```
- window
    - document
        - root element (html)
            - element (head)
                - element (title)
                    - text "Title"
                - ...
            - element (body)
                - element (a)
                    - text "Link"
                - ...
```

- How to traverse from one to the next:
```
    - parentNode
    - childNodes[nodenumber]
    - firstChild
    - lastChild
    - nextSibling
    - previousSibling
```


----------


##JavaScript


###1. What are undefined and undeclared variables?

**Undeclared** variables are those that are not declared in the program (do not exist at all), trying to read their values gives runtime error. **Undefined** variables are those that are not assigned any value but are declared in the program. Trying to read such variables gives special value called undefined value.


###2. DOM manipulation
- How to create and add nodes:
```
    document.createElement('tag')
    document.createTextNode('text') // creates <p>
    document.getElementById('parent-id').appendChild(node)
    document.getElementById('parent-id').insertBefore(pivotNode, node)
```
- Find nodes:
```
    document.getElementById('id')
    document.getElementsByClassName('class')[idx]
    document.getElementsByTagName('tag')[idx]
```
- Remove nodes:
```
    var parent = document.getElementById('parent-id');
    var nodeToRemove = document.getElementById('remove-id');
    parent.removeChild(nodeToRemove);
```
- Copy nodes:
```
    var clone = document.getElementById('id').cloneNode(true) // true means deep copy
```
- Replace nodes:
```
    var parent = document.getElementById('parent-id');
    var nodeToReplace = document.getElementById('replacing-id');
    var newNode = document.createTextNode('I\'m a new node.');
    parent.replaceChild(nodeToReplace, newNode);
```


###3. Events
Events are things that happen to DOM elements in your page, such as mouse clicks or errors when an image fails to load. When an event happens, the browser sends the event to the related element. If you've set a handler (a function) on that element, it gets called with related event info which means you "handled" the event. When a handler gets called, it gets an Event object as its first argument, which has lots of fields that describe about the event, such as which keystroke was hit, what the mouse coordinates were, the time at which the event happened, and so on.

*Only Internet Explorer versions lower than 9 uses the global window.event object instead of an argument.*

The classy way to set a handler is to use `addEventListener()` on the target. You then can remove them with `removeEventListener()`. If `useCapture` is true then handler will be executed at the capturing phase.
```
document.getElementById('id').addEventListener('click', handlerFunction, useCapture)
document.getElementById('id').removeEventListener('click', handlerFunction, useCapture)
```
Unfortunately, Internet Explorer works differently from other browsers. There is no `addEventListener()` function and there is an `attachEvent()` function instead:
```
document.getElementById('id').attachEvent('onclick', handlerFunction);
```


###4. XMLHttpRequest

AJAX is Asynchronous JavaScript and XML. AJAX is a technique for creating fast and dynamic web pages. AJAX allows web pages to be updated asynchronously by exchanging small amounts of data with the server behind the scenes. This means that it is possible to update parts of a web page, without reloading the whole page.

AJAX flow:

- Client: Create an XMLHttpRequest object
- Client: Send HttpRequest
- Server: Process HttpRequest
- Server: Create a response and send data back
- Client: Process the returned data and update page content

XMLHttpRequest is a JavaScript object that was designed by Microsoft. It provides an easy way to retrieve data from a URL without having to do a full page refresh. A Web page can update just a part of the page without disrupting what the user is doing. Despite its name, XMLHttpRequest can be used to retrieve any type of data, not just XML, and it supports protocols other than HTTP.

To create an instance of XMLHttpRequest, simply do this:

```
var myRequest = new XMLHttpRequest();
```

The simplest GET request is:

```
var xmlhttp = new XMLHttpRequest();
xmlhttp.onreadystatechange = function () {
    if (xmlhttp.readyState === 4 && xmlhttp.status === 200) {
        /* xmlhttp.responseText; */
    }
}
xmlhttp.open("GET", "/api/giveMeData?id=123", true); // (method, url, async)
xmlhttp.send();
```

`onreadystatechange` a function to be called automatically each time the readyState property changes. `readyState` holds the status of the XMLHttpRequest. Changes from 0 to 4:

- 0: request not initialized;
- 1: server connection established;
- 2: request received;
- 3: processing request;
- 4: request finished and response is ready.

`status`:

- 200: OK;
- 404: Page not found.


###5. JSON

JSON stands for JavaScript Object Notation. It is used primarily to transmit data between a server and web application, as an alternative to XML. Although originally derived from the JavaScript scripting language, JSON is a language-independent data format, and code for parsing and generating JSON data is readily available in a large variety of programming languages.

JSON's basic types are:

- Number (double-precision floating-point format in JavaScript, generally depends on implementation)
- String (double-quoted Unicode, with backslash escaping)
- Boolean (true or false)
- Array (an ordered, comma-separated sequence of values enclosed in square brackets; the values do not need to be of the same type)
- Object (an unordered, comma-separated collection of key:value pairs enclosed in curly braces, with the ':' character separating the key and the value; the keys must be strings and should be distinct from each other)
- null (empty)


###6. Difference between .call and .apply

The main difference is that `apply` lets you invoke the function with arguments as an array; `call` requires the parameters be listed explicitly.
```
function abc(a, b, c) { ... } // define a function

abc.apply(undefined /* thisArg */, ['A', 'B', 'C'])
abc.call(undefined /* thisArg */, 'A', 'B', 'C')
```


###7. Function.prototype.bind

The `bind` method creates a new function that, when called, has its this keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.
```
function abc(a, b, c) { ... } // define a function

var abcBind = abc.bind(undefined /* thisArg */, 'A', 'B', 'C');
abcBind(); // keeps values from bind for execution
```


###8. Closures

A closure is an inner function that has access to the outer (enclosing) function's variables—scope chain. The closure has three scope chains: it has access to its own scope (variables defined between its curly brackets), it has access to the outer function's variables, and it has access to the global variables. **Simply accessing variables outside of your immediate lexical scope creates a closure.**

```
function sayHello(name) {
    var hello = 'Hello '; // local variable
    var sayAlert = function() {
        alert(hello + name);
    };
    return sayAlert;
}

var say = sayHello('Alex');
say();
```

**The most important thing closures do is allow functions to keep on working even if their environment drastically changes or disappears**. Any variables that were in scope when the function was created are enclosed and protected to ensure the function still works.


###9. Hoisting

Within its current scope, regardless of where a variable is declared, it will be, behind the scenes, hoisted to the top. However, only the declaration will be hoisted. If the variable is also initialized, the current value, at the top of the scope, will initially be set to undefined.

```
function () {
    alert(myvar); // myvar is declared but undefined
    var myvar = 'local value';
}
```


###10. defer vs async

- **defer** - wider browser support; puts them in a queue and executes in order once document is loaded;
- **async** - not as wide as defer support; loads and executes immediately;

If you use both *defer* and *async* then async overrides defer in browsers that support both.


###11. Module pattern
```
(function selfExecutedModule(app, window, $, undefined) {
    // ...
    // module logic goes here
    // ...
})(window.app, window, jQuery);

var module = function executedOnDemandModule(app, window, $, undefined) {
    var obj = {};
    
    // ...
    // module logic goes here
    // ...
    
    return obj;
};

(function nodeJsModule(module) {
    'use strict';

    module.exports = {
        // ...
        // module logic goes here
        // ...
    };
})(module);
```


###12. Same-origin policy

The same-origin policy restricts how a document or script loaded from one origin can interact with a resource from another origin. Two pages have the same origin if the protocol, port (if one is specified), and host are the same for both pages.


###13. FOUC

A flash of unstyled content (FOUC) is an instance where a web page appears briefly with the browser's default styles prior to loading an external CSS stylesheet, due to the web browser engine rendering the page before all information is retrieved. The page corrects itself as soon as the style rules are loaded and applied; however, the shift is quite visible and distracting.

To avoid FOUC try to place js self-executed function in a head of a document. See IE HTML5 shiv for example: `<!--[if IE]><script src="//c.mfcreative.com/js/html5shiv.js"></script><![endif]-->`


----------


##CSS


###1. The box model
`box-sizing` allows you to switch box models:

- `border-box` - it causes the box sizes to be applied to the border and everything inside it (traditional model);
- `content-box` - it causes the box sizes to be applied to the content only (W3C model).


###2. Block vs. Inline elements
**Block**:

- If no width is set, will expand naturally to fill its parent container
- Can have margins and/or padding
- If no height is set, will expand naturally to fit its child elements (assuming they are not floated or positioned)
- By default, will be placed below previous elements in the markup (assuming no floats or positioning on surrounding elements)
- Ignores the `vertical-align` property

**Inline**:

- Flows along with text content
- Will not clear previous content to drop to the next line like block elements
- Is subject to white-space settings in CSS
- Will ignore top and bottom margin settings, but will apply left and right margins, and any padding
- Will ignore the width and height properties
- If floated left or right, will automatically become a block-level element, subject to all block characteristics
- Is subject to the `vertical-align` property


###3. Floating elements
Aside from the simple example of wrapping text around images, floats can be used to create entire web layouts.

**Clearing the Float** - An element that has the clear property set on, it will not move up adjacent to the float like the float desires, but will move itself down past the float.

**The Great Collapse** - One of the interesting things about working with floats is how they can affect the element that contains them. If this parent element contained nothing but floated elements, the height of it would literally collapse to nothing. This isn't always obvious if the parent doesn't contain any visually noticeable background, but it is important to be aware of. Collapsing almost always needs to be dealt with to prevent strange layout and cross-browser problems. We fix it by clearing the float after the floated elements in the container but before the close of the container.

**Techniques for Clearing Floats**:

- *The Empty Div Method* is, quite literally, an empty div: `<div style="clear: both;"></div>`.
- *The Overflow Method* relies on setting the overflow CSS property on a parent element. If this property is set to auto or hidden on the parent element, the parent will expand to contain the floats, effectively clearing it for succeeding elements.
- *The Easy Clearing Method* uses a clever CSS pseudo selector `:after` to clear floats. Rather than setting the overflow on the parent, you apply an additional class like `clearfix` to it.

**Problems with Floats**:

- *Pushdown* is a symptom of an element inside a floated item being wider than the float itself (typically an image). Most browsers will render the image outside the float, but not have the part sticking out affect other layout. IE will expand the float to contain the image, often drastically affecting layout. *Quick fix*: Make sure you don't have any images that do this, use `overflow: hidden` to cut off excess.
- *Double Margin Bug*. Another thing to remember when dealing with IE6 is that if you apply a margin in the same direction as the float, it will double the margin. *Quick fix*: set `display: inline` on the float, and don't worry it will remain a block-level element.
- The *3px Jog* is when text that is up next to a floated element is mysteriously kicked away by 3px like a weird forcefield around the float. *Quick fix*: set a width or height on the affected text.
- In IE7, the *Bottom Margin Bug* is when if a floated parent has floated children inside it, bottom margin on those children is ignored by the parent. *Quick fix*: using bottom padding on the parent instead.


###4. CSS font-size
One of the most confusing aspects of CSS styling is the application of the font-size attribute for text scaling. In CSS, you're given four different units by which you can measure the size of text as it's displayed in the web browser. It's easy to understand the difference between font-size units when you see them in action. Generally, `1em = 12pt = 16px = 100%`.

- **Ems (em)**: The em is a scalable unit that is used in web document media. An em is equal to the current font-size, for instance, if the font-size of the document is 12pt, 1em is equal to 12pt. Ems are scalable in nature, so 2em would equal 24pt, .5em would equal 6pt, etc. Ems are becoming increasingly popular in web documents due to scalability and their mobile-device-friendly nature.
- **Pixels (px)**: Pixels are fixed-size units that are used in screen media. One pixel is equal to one dot on the computer screen. Many web designers use pixel units in web documents in order to produce a pixel-perfect representation of their site as it is rendered in the browser. One problem with the pixel unit is that it does not scale upward for visually-impaired readers or downward to fit mobile devices.
- **Points (pt)**: Points are traditionally used in print media. One point is equal to 1/72 of an inch. Points are much like pixels, in that they are fixed-size units and cannot scale in size.
- **Percent (%)**: The percent unit is much like the em unit, save for a few fundamental differences. First and foremost, the current font-size is equal to 100% (i.e. 12pt = 100%). While using the percent unit, your text remains fully scalable for mobile devices and for accessibility.

In theory, the em unit is the new and upcoming standard for font sizes on the web, but in practice, the percent unit seems to provide a more consistent and accessible display for users. When client settings have changed, percent text scales at a reasonable rate, allowing designers to preserve readability, accessibility, and visual design. In the same time when it comes to the responsive design em is a today's winner.


###5. CSS Attribute selectors

- `[att]` - Represents an element with the `att` attribute, whatever the value of the attribute.
- `[att=val]` - Represents an element with the `att` attribute whose value is exactly "val".
- `[att^=val]` - Represents an element with the `att` attribute whose value begins with the prefix "val". If "val" is the empty string then the selector does not represent anything.
- `[att$=val]` - Represents an element with the `att` attribute whose value ends with the suffix "val". If "val" is the empty string then the selector does not represent anything.
- `[att*=val]` - Represents an element with the `att` attribute whose value contains at least one instance of the substring "val". If "val" is the empty string then the selector does not represent anything.
- `[att~=val]` - Represents an element with the `att` attribute whose value is a whitespace-separated list of words, one of which is exactly "val". If "val" contains whitespace, it will never represent anything (since the words are separated by spaces). Also if "val" is the empty string, it will never represent anything.
- `[att|=val]` - Represents an element with the `att` attribute, its value either being exactly "val" or beginning with "val" immediately followed by "-". This is primarily intended to allow language subcode matches (e.g., the hreflang attribute on the a element in HTML).


##6. PNG vs. JPEG

You can save an image in PNG, JPEG, GIF and dozen other formats.

**GIF format** is limited to 256 colors and is a lossless compression file format, a common choice for use on the Web. GIF is a good choice for storing line drawings, text, and iconic graphics at a small file size.

**PNG format** is a lossless compression file format, which makes it a common choice for use on the Web. PNG is a good choice for storing line drawings, text, and iconic graphics at a small file size.

**JPG format** is a lossy compressed file format. This makes it useful for storing photographs at a smaller size than a BMP. JPG is a common choice for use on the Web because it is compressed.

*For storing line drawings, text, and iconic graphics at a smaller file size, GIF or PNG are better choices because they are lossless*.


###7. Differences between browsers

That's a pretty standard process, and the various internet browsers around don't differ much in how they do all of that stuff. But when the web server gives the browser the web page you asked for, it isn't usually in a nice format the browser can immediately display. It's in something like HTML and CSS, which need to be processed by the browser before they can be displayed. That's where browsers start to get different.

Each browser contains what is called a rendering engine (or a layout engine). The rendering engine is the part of the browser that processes code and turns it into something displayable. Currently there are four main rendering engines: Webkit, Gecko, Trident, and Blink. Their usage is as follows:

- Webkit: Safari and Opera
- Gecko: Firefox
- Trident: Internet Explorer
- Blink: Chrome

Each of these rendering engines handles the rendering of web pages differently, and so results may vary between different engines.


###8. CSS Specificity

**The CSS Specificity is one of the most difficult concepts to grasp in CSS**. The different weight of selectors is usually the reason why your CSS-rules don’t apply to some elements, although you think they should have. In order to minimize the time for bug hunting you need to understand, how browsers interpret your code. And to understand that, you need to have a firm understanding on how specificity works. In most cases such problems are caused by the simple fact that somewhere among your CSS-rules you’ve defined a more specific selector.

- Specificity determines, which CSS rule is applied by browsers.
- Selector specificity is a process used to determine which rules take precedence in CSS when several rules could be applied to the same element in markup.
- Every selector has its specificity.
- If two selectors apply to the same element, the one with higher specificity wins.


**Specificity hierarchy:**

- *Inline styles*. An inline style lives within your XHTML document. It is attached directly to the element to be styled. E.g. `<h1 style="color: #fff;">`
- *IDs*. ID is an identifier for your page elements, such as `#div`.
- *Classes, attributes and pseudo-classes*. This group includes .classes, [attributes] and pseudo-classes such as `:hover`, `:focus` etc.
- *Elements and pseudo-elements*. Including for instance `:before` and `:after`.


**How to measure specificity?**

Start at 0, add 1000 for style attribute, add 100 for each ID, add 10 for each attribute, class or pseudo-class, add 1 for each element name or pseudo-element. So in

```
body #content .data img:hover
```

the specificity value would be 122 (0,1,2,2 or 0122): 100 for #content, 10 for .data, 10 for :hover, 1 for body and 1 for img.


**Specificity: Basic Principles**

- Equal specificity: the latest rule is the one that counts.
- Unequal specificity: the more specific rule is the one that counts.


**Specificity Examples:**

- `div p` - 2 (two HTML selectors)
- `div:after` - 2 (one element, one pseudo-element)
- `h1 + *[rel=up]` - 11 (one attribute, one element)
- `.red` - 10 (one class selector)
- `body #blue .yellow p` - 112 (HTML selector, id selector, class selector, HTML selector; 1+100+10+1)
- `#green` - 100 (one id selector)
- `a:hover` - 11 (one element, one pseudo-class)