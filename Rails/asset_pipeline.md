# Rails Asset Pipeline

> Reference: [Rails Asset Pipeline](http://guides.rubyonrails.org/asset_pipeline.html)

The asset pipeline provides a framework to concatenate and minify or compress JavaScript and CSS assets. It also adds the ability to write these assets in other languages and pre-processors such as CoffeeScript, Sass and ERB.

## Features
The first feature of the pipeline is to concatenate assets, which can reduce the number of requests that a browser makes to render a web page. Web browsers are limited in the number of requests that they can make in parallel, so fewer requests can mean faster loading for your application.

Sprockets concatenates all JavaScript files into one master .js file and all CSS files into one master .css file. As you'll learn later in this guide, you can customize this strategy to group files any way you like. In production, Rails inserts an MD5 fingerprint into each filename so that the file is cached by the web browser. You can invalidate the cache by altering this fingerprint, which happens automatically whenever you change the file contents.

The second feature of the asset pipeline is asset minification or compression. For CSS files, this is done by removing whitespace and comments. For JavaScript, more complex processes can be applied. You can choose from a set of built in options or specify your own.

The third feature of the asset pipeline is it allows coding assets via a higher-level language, with precompilation down to the actual assets. Supported languages include Sass for CSS, CoffeeScript for JavaScript, and ERB for both by default.

The fourth feature of the asset pipeline is providing absolute paths to other assets such as images and fonts

## Usage

In previous versions of Rails, all assets were located in subdirectories of public such as images, javascripts and stylesheets. With the asset pipeline, the preferred location for these assets is now the app/assets directory. Files in this directory are served by the Sprockets middleware.

Assets can still be placed in the public hierarchy. Any assets under public will be served as static files by the application or web server when config.serve_static_files is set to true. You should use app/assets for files that must undergo some pre-processing before they are served.

In production, Rails precompiles these files to public/assets by default. The precompiled copies are then served as static assets by the web server. The files in app/assets are never served directly in production.

Pipeline assets can be placed inside an application in one of three locations: app/assets, lib/assets or vendor/assets.

* **app/assets** is for assets that are owned by the application, such as custom images, JavaScript files or stylesheets.

* **lib/assets** is for your own libraries' code that doesn't really fit into the scope of the application or those libraries which are shared across applications.

* **vendor/assets** is for assets that are owned by outside entities, such as code for JavaScript plugins and CSS frameworks. Keep in mind that third party code with references to other files also processed by the asset Pipeline (images, stylesheets, etc.), will need to be rewritten to use helpers like asset_path.

## Paths to CSS and JS resources

Files are loaded into the asset pipeline by referencing their file name in their respective **manifest files**: `application.js` and `application.css`.

As an example, these files:

    app/assets/javascripts/home.js
    lib/assets/javascripts/moovinator.js
    vendor/assets/javascripts/slider.js
    vendor/assets/somepackage/phonebox.js

would be referenced in a manifest like this:

    //= require home
    //= require moovinator
    //= require slider
    //= require phonebox

but generally you load all sundry files with the `require_tree .` method.

application.js

    // ...
    //= require jquery
    //= require jquery_ujs
    //= require_tree .

application.css

    /* ...
    *= require_self
    *= require_tree .
    */

## Images

In regular views you can access images in the public/assets/images directory like this:

    <%= image_tag "rails.png" %>

Inside of css files you can access them like this:

    .class { background-image: url(<%= asset_path 'image.png' %>) }