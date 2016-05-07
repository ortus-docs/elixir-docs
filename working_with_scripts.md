# Working With Scripts

Elixir also provides several functions to help you work with your JavaScript files, such as compiling ECMAScript 6, Browserify, minification, and simply concatenating plain JavaScript files:

* `scripts`
* `scriptsIn`
* `babel`
* `browserify`

> **Tip**: Please remember you can use any valid [file globbing](https://github.com/isaacs/node-glob) pattern as well.


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

### Custom Options
The fourth argument to the `browserify` method is an `options` object that will be passed through to the browserify task.

```js
elixir( function( mix ){
    mix.browserify( 'main.js', 'includes/javascripts/main.js', 'public/js', {} );
} );
```

### Custom Transformers

While Browserify ships with the [Partialify](https://www.npmjs.com/package/partialify) and [Babelify](https://github.com/babel/babelify) transformers, you're free to install and add more if you wish by doing 2 simple steps:

1. Install the transformer
```
npm install aliasify --save-dev
```

2. update your `Gulpfile.js` by pushing the new transformer configuration via the `elixir.config.js.browserify.transformers` array:

```js
elixir.config.js.browserify.transformers.push( {
    name 		: 'aliasify',
    options 	: {}
} );

elixir( function( mix ){
    mix.browserify( 'main.js' );
} );
```

## Babel

The `babel` method may be used to compile [ECMAScript 6 and 7](https://babeljs.io/docs/learn-es2015/) and [JSX](https://facebook.github.io/react/docs/jsx-in-depth.html) into plain JavaScript. This function accepts an array of files relative to the `resources/assets/js` directory, and generates a single `all.js` file in the `includes/js` directory:

```js
elixir( function( mix ){
    mix.babel( [
        'order.js',
        'product.js',
        'react-component.jsx'
    ] );
} );
```

To choose a different output location, simply specify your desired path as the second argument.  You can also override the base directory by leveraging the third optional argument. The signature and functionality of this method are identical to `mix.scripts()`, excluding the Babel compilation.

### Custom Options

The `babel` method also takes in an optional fourth argument which is an object of `options`:

```js
elixir( function( mix ){
    mix.babel( [
        'order.js',
        'product.js',
        'react-component.jsx'
    ], "includes/all.js", "", {} );
} );
```


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

If you have multiple JavaScript files that you would like to combine into a single file, you may use the `combine` method.  Please note that the `combine` method does NOT do any type of compilation or minification.  It is a plain 'ol combination or concatenation of files.

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


