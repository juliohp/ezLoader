ezLoader
===========

ezLoader is an asynchronous JavaScript and CSS loader that helps to improve performance with a very simple and unique implementation.

Built in pure JavaScript, ezLoader is dependency-free, allowing you to load any resources from both relative and absolute locations.

ezLoader **does not** implement the [Asynchronous Module Definition](https://github.com/amdjs/amdjs-api/wiki/AMD) (AMD) API. However, it is a powerful resource to load 'modules' defining dependencies and events that need to be loaded|triggered before loading a specific module. These defintions occur in a single configuration file.

Download
===========

* [ezLoader.js](https://github.com/fsevilla/ezLoader/raw/master/ezLoader.js) (full source)
* [ezLoader.min.js](https://github.com/fsevilla/ezLoader/raw/master/ezLoader.min.js) (minified)

Features
===========

* Custom (pseudo)modular approach
* Groups JS and CSS files into modules
* Built-in events for loading modules
* Define module dependencies
* Set base Url to load files
* Set base element to load files above a specific tag element
* All configuration occurs in a single JavaScript file
* Supports all major browsers

Getting started
===========

ezLoader consists of two JavaScript files. 
* ezLoader source file
* configuration script

These files can be loaded as follows:
```html
<!-- Load ezLoader source file -->
<script src="path/to/ezLoader.js"></script>
<!-- Load configuration script -->
<script src="path/to/config.js"></script>
```

or simply by adding the configuration file to the data-main attribute. 
```html
<!-- Load ezLoader source file with configuration script -->
<script src="path/to/ezLoader.js" data-main="config"></script>
```

The path to 'config' is relative to the path of ezLoader.js. **Note** how the extension .js is missing. ezLoader handles that so you save a few characters from the HTML.

Basic Usage
===========

The following shows a basic example of the configuration script:

```js
// Initialize the loader if you want to change the default settings. 
// Otherwise you can avoid this call and ezLoader will initialize itself on page load.
ezLoader.init();

// Load jquery & jquery UI after page load event
ezLoader.onLoad('jquery',{
  scripts: ['path/to/jquery.js','path/to/jquery-ui.js'],
  async: false, // make sure jquery loads before jquery ui
  onStart: function(){
    // Code to execute when module starts loading
  },
  onComplete: function(){
    // Code to execute after both scripts have loaded
  }
});

// Load the application script after jquery
ezLoader.loadModule('app',{
  scripts: 'path/to/app.js',
  dependency: 'jquery', // starts loading after module 'jquery' has been fully loaded
  onComplete: function(a){
    // Do something with scoped var 'a' defined in app.js
  }
});

// load lightbox JS & CSS after user has interacted with the page
ezLoader.onUserReady('lightbox',{
  scripts: 'path/to/lightbox.js',
  styles: 'path/to/lightbox.css'
});

// execute a function after both 'app' & 'lightbox' modules have loaded
ezLoader.onModuleReady(['app','lightbox'],'lightboxInit',function(){
  // Execute a JS function after both modules have loaded
  // e.g. initLightbox();
});

```

Browser support
===========

* IE 6+
* Firefox 11+
* Safari 5+
* Chrome 3+
* Opera 10+
