jQuery Boxfit v1.01
======

Boxfit is a jQuery plugin for resizing text. It will scale text to fit inside a fixed width div. Boxfit respects padding settings for the div. While boxfit will not scale images, it *will* handle text with other visual entities mixed in.

Usage
=====

```html
<div id="my-big-box" style="width: 500px; height: 500px">
  This is some text
</div>
```

```javascript
$('#my-big-box').boxfit();
```

This will make the text appear very large to take up the entire 500x500 area as best it can.

By default, the script will fit text in a single line and vertically and horizontally center it like this:

```
---------------------------
|                         |
|          hello          | <= this text would be very large
|                         |    and fill up the whole box
---------------------------
```

Long strings are shrunk down to fit in the box. This may not always be desired. You can pass in arguments to make the text wrap across lines to try to fill out as much of the box as possible:

```javascript
$('#my-big-box').boxfit({multiline: true});
```

```
---------------------------
|         hello           |
|        this is          |
|         hello           |
---------------------------
```

What it's actually doing under the hood is converting 

```html
<div id="my-big-box" style="width: 500px; height: 500px">
  This is some text
</div>
```

Into:

```html
<div id="my-big-box" style="width: 500px; height: 500px">
  <span style="font-size: ##">
    This is some text
  </span>
</div>
```

Then it applies styles to the span to center and align it. This span is EXTREMELY important as it is used to resize the inner text. The text is resized in a loop by changing the font-size attribute on the span tag. Therefor, for now, content inside the target DIV should be text only. If after 200 iterations, the script fails to find a suitable font-size, it will give up and spit out whatever the current state is. This can happen if you have wacky CSS or lack text inside the div.

Valid parameters:

- *align_middle*: (default true) set to false to disable vertical alignment behavior
- *align_center*: (default true) set to false to disable centering behavior (horizontal)
- *step_size*: (default 1) the amount to change each time - bigger numbers are faster but fit less perfectly
- *step_limit*: (default 200) the number of font size iterations we should step through until we give up
- *multiline*: (default false) set to true to allow the text to wrap
- *width*: manually set a width if you haven't set one explicitly via CSS
- *height*: manually set a height if you haven't set one explicitly via CSS
- *minimum_font_size*: (default 5) minimum font size (changing this may cause some "shrink" scenarios to overflow instead)
- *maximum_font_size*: (default null) set to the max font size you want for the element, if none is given there is no maximum

Notice
======
This source code will be maintained in coffeescript and compiled over to JavaScript (just a personal preference). Patches can be submitted in either and I'll just re-write it.


License
=======
Boxfit uses the MIT license. More info here: http://www.opensource.org/licenses/mit-license.php
