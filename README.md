# Introduction

ColdBox Elixir provides a clean, fluent API for defining basic [Gulp](http://gulpjs.com/) tasks for your ColdBox applications.  This project was forked from the [Laravel Elixir](https://github.com/laravel/elixir) project, so many many thanks for all their hard work and ideas.

## How it works
Elixir supports several common CSS, JavaScript pre-processors, and TestBox runner integrations. By leveraging Gulp and the `Gulpfile.js` configuration file, you can use method chaining and Elixir will allow you to fluently define your asset pipeline using conventions. 

## Conventions

All resources in your ColdBox application will be stored under the `resources/assets` folder.  Under this folder you can find several sub-sections:


* `css` - Where you can store your css
* `js` - Where you can store your js, vue.js and more
* `less` - Where you can store your less files
* `sass` - Where you can store your sass files

Depending on the formulas you mix up in the `Gulpfile.js` using Elixir, you will end up with all your assets linted, minified, etc in their appropriate destination in the `includes` folder:

* `css` - Destination for css
* `js` - Destination for js
* `build` - Destination for versioned assets


For example:

```js
var elixir = require( 'coldbox-elixir' );
elixir( function( mix ) {
	// Look in the 'resources/sass' folder
    mix.sass( 'app.scss' )
    	// Look in the 'resourcess/css` folder
       .styles( 'modules.css' );
       
   // Elixir will then output all assets to ColdBox 'includes' folder by convention.
});
```

If you've ever been confused about how to get started with Gulp and asset compilation, you will love ColdBox Elixir. However, you are not required to use it while developing your application. You are free to use any asset pipeline tool you wish, or even none at all.