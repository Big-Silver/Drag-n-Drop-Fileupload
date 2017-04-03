# Drag-n-Drop-Fileupload

<img width="900" src="img/dropzone.png" border="0" />

## About
This project is the Drag and Drop Fileupload using Dropzone.js.
This Dropzone(Drag and Drop Fileupload) example is written by [Big Silver].

## Quick Start

```bash
# clone our repository
$ git clone https://github.com/Big-Silver/Drag-n-Drop-Fileupload.git dropzone

# change directory to your project
$ cd dropzone

# Run the index.html file at the browser.

```

## Installation

You probably only need to look at the simple example (source) to get started. Continue reading for step by step instructions and different installation approaches.

Download the standalone dropzone.js and include it like this:
```html
<script src="./path/to/dropzone.js"></script>
```
Dropzone is now activated and available as window.Dropzone.

Dropzone does not handle your file uploads on the server. You have to implement the code to receive and store the file yourself. See the section Server side implementation for more information.

This is all you need to get dropzone up and running, but if you want it to look like the dropzone on this page, you’ll need to download dropzone.css from the dist folder.

With component

If you use component you can just add dropzone as a dependency:

```bash
"enyo/dropzone": "*"
```
Then include it like this:

```html
var Dropzone = require("dropzone");
```
so it is activated and scans the document.

The basic CSS markup is also included with component, but if you want it to look the same as on this page, you have to download the CSS (see below).

With RequireJS

Dropzone is also available as an AMD module for RequireJS.

You can find the dropzone-amd-module in the downloads folder.

## Usage

The typical way of using dropzone is by creating a form element with the class dropzone:

```html
<form action="/file-upload"
      class="dropzone"
      id="my-awesome-dropzone">
</form>
```
That’s it. Dropzone will find all form elements with the class dropzone, automatically attach itself to it, and upload files dropped into it to the specified action attribute. The uploaded files can be handled just as if there would have been a html input like this:

```html
<input type="file" name="file" />
```
If you want another name than file you can configure dropzone with the option paramName.

If you’re using component don’t forget to require("dropzone"); otherwise it won’t be activated.

If you want your file uploads to work even without JavaScript, you can include an element with the class fallback that dropzone will remove if the browser is supported. If the browser isn’t supported, Dropzone will not create fallback elements if there is a fallback element already provided. (Obviously, if the browser doesn’t support JavaScript, the form will stay as is)

Typically this will look like this:

```html
<form action="/file-upload" class="dropzone">
  <div class="fallback">
    <input name="file" type="file" multiple />
  </div>
</form>
```
Create dropzones programmatically

Alternatively you can create dropzones programmaticaly (even on non form elements) by instantiating the Dropzone class

```javascript
// Dropzone class:
var myDropzone = new Dropzone("div#myId", { url: "/file/post"});
```
or if you use jQuery, you can use the jQuery plugin Dropzone ships with:

```javascript
// jQuery
$("div#myId").dropzone({ url: "/file/post" });
```
Don’t forget to specify an url option if you’re not using a form element, since Dropzone doesn’t know where to post to without an action attribute.

Server side implementation

Dropzone does not provide the server side implementation of handling the files, but the way files are uploaded is identical to simple file upload forms like this:

```html
<form action="" method="post" enctype="multipart/form-data">
  <input type="file" name="file" />
</form>
```

## Configuration

```javascript
Dropzone.options.myAwesomeDropzone = {
  paramName: "file", // The name that will be used to transfer the file
  maxFilesize: 2, // MB
  accept: function(file, done) {
    if (file.name == "justinbieber.jpg") {
      done("Naha, you don't.");
    }
    else { done(); }
  }
};
```

## Events

The recommended way from within the init configuration:
```javascript
Dropzone.options.myAwesomeDropzone = {
  init: function() {
    this.on("addedfile", function(file) { alert("Added file."); });
  }
};
```
This example uses jQuery so it creates the Dropzone, only when the DOM has loaded
```javascript
// Disabling autoDiscover, otherwise Dropzone will try to attach twice.
Dropzone.autoDiscover = false;
// or disable for specific dropzone:
// Dropzone.options.myDropzone = false;

$(function() {
    // Now that the DOM is fully loaded, create the dropzone, and setup the
    // event listeners
    var myDropzone = new Dropzone("#my-dropzone");
    myDropzone.on("addedfile", function(file) {
        /* Maybe display some more file information on your page */
    });
})
```
