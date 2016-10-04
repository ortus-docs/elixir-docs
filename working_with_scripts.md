# Working With Scripts

Elixir also provides several functions to help you work with your JavaScript files, such as compiling future versions of JavaScript, using module bundlers, minification, and simply concatenating plain JavaScript files:

* `scripts`
* `scriptsIn`
* `webpack`
* `browserify`
* `rollup`



<br />

> **Tip**: Please remember you can use any valid [file globbing](https://github.com/isaacs/node-glob) pattern as well.

## Babel

> **Deprecation**: `mix.babel()` has been deprecated in ColdBox Elixir 2.0.0 in favor of using one of the module bundlers ([`browserify`](https://github.com/coldbox-elixir/extension-browserify), [`rollup`](https://github.com/coldbox-elixir/extension-rollup) or [`webpack`](https://github.com/coldbox-elixir/extension-webpack))


## Combining Compiled Scripts

If you have multiple JavaScript files (non babelified) that you would like to combine into a single file, you may use the `scripts` method.

The `scripts` method assumes all paths are relative to the `resources/assets/js` directory, and will place the resulting JavaScript in `includes/js/all.js` by default:

```js
elixir( function( mix ){
    mix.scripts( [
        'jquery.js',
        'app.js'
    ] );
} );
```

If you need to combine multiple sets of scripts into different files, you may make multiple calls to the `scripts` method. The second argument given to the method determines the resulting file name for each concatenation. You can also use the third optional argument to override the base directory of `resources/assets/js`

```
elixir( function( mix ){
    mix.scripts( ['app.js', 'controllers.js' ], 'public/js/app.js' )
       .scripts( ['forum.js', 'threads.js' ], 'public/js/forum.js' );
});
```

If you need to combine all of the scripts in a given directory, you may use the `scriptsIn` method or globbing patterns. The resulting JavaScript will be placed in `includes/js/all.js`:

```js
elixir( function( mix ){
    mix.scriptsIn( 'resources/js/some/directory' );
} );
```

## Combining Scripts

If you have multiple JavaScript files that you would like to combine into a single file, you may use the `combine` method.  Please note that the `combine` method does NOT do any type of compilation or minification.  It is a plain 'ole combination or concatenation of files.

The method assumes the starting place of all paths from the `root` of your application, so not the `resources` folder.  The first argument is a single location or an array of locations, the second argument is the output combo file.

```js
elixir( function( mix ){
    mix.combine( 
    	[
        	'resources/assets/vendor/jquery.js',
        	'resources/assets/vendor/app.js',
    	],
    	"includes/js/combined.js"
    );
    
    mix.combine( 
    	[
        	'resources/assets/vendor/*.js'
    	],
    	"includes/js/combined.js"
    );
} );
```

## Module Bundlers

There is official support for three module bundlers:

* [Browserify](https://github.com/coldbox-elixir/extension-browserify)
* [Rollup](https://github.com/coldbox-elixir/extension-rollup)
* [Webpack](https://github.com/coldbox-elixir/extension-webpack)

See each individual repository for their specific API.





## Browserify



Elixir ships with a [browserify](http://browserify.org/) method, which gives you all the benefits of requiring modules in the browser and using [ECMAScript 6](https://babeljs.io/docs/learn-es2015/) and [JSX](https://facebook.github.io/react/docs/jsx-in-depth.html).



This task assumes that your scripts are stored in `resources/assets/js` and will place the resulting file in `includes/js/main.js`. You may pass a custom output location as an optional second argument and an optional third argument to override the base directory of `resources/assets/js`:



```

elixir( function( mix ){

 mix.browserify( 'main.js' );

} );



// Specifying a specific output filename...

elixir( function( mix ){

 mix.browserify( 'main.js', 'includes/javascripts/main.js' );

} );



// Specifying a specific output filename + basedir

elixir( function( mix ){

 mix.browserify( 'main.js', 'includes/javascripts/main.js', 'public/js' );

} );

```



