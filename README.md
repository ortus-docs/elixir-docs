# Introduction

ColdBox Elixir provides a clean, fluent API for defining basic [Gulp](http://gulpjs.com/) tasks for your ColdBox applications.  This project was forked from the [Laravel Elixir](https://github.com/laravel/elixir) project, so many many thanks for all their hard work and ideas.

## How it works
Elixir supports several common CSS, JavaScript pre-processors, and TestBox runner integrations. By leveraging your familiar `Gulpfile.js` configuration file, you can use method chaining and Elixir will allow you to fluently define your asset pipeline using conventions. For example:

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