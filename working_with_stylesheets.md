# Working With Stylesheets

The `Gulpfile.js` file in your project's root directory contains all of your Elixir tasks. Elixir tasks can be chained together to define exactly how your assets should be compiled.  Please note that when working with any form of CSS, Elixir automatically runs your file through a CSS [autoprefixer](https://www.npmjs.com/package/gulp-autoprefixer), which automatically adds or removes vendor-specific CSS3 prefixes.

> **Tip**: Please remember you can use any valid [file globbing](https://github.com/isaacs/node-glob) pattern as well.

# Less

To compile [Less](http://lesscss.org/) into CSS, you may use the `less` method. The `less` method assumes that your Less files are stored in `resources/assets/less`. By default, the task will place the compiled CSS for this example in `includes/css/app.css`:

```js
elixir( function( mix ){
    mix.less( 'app.less' );
} );
```

You may also combine multiple Less files into a single CSS file. Again, the resulting CSS will be placed in `includes/css/app.css`:

```js
elixir( function( mix ){
    mix.less( [
        'app.less',
        'controllers.less'
    ] );
} );
```

If you wish to customize the output location and/or name of the compiled CSS, you may pass a second argument to the `less` method:

```js
elixir( function( mix ){
    mix.less( 'app.less', 'includes/stylesheets' );
} );

// Specifying a specific custom output filename...
elixir( function( mix ){
    mix.less( 'app.less', 'includes/stylesheets/style.css' );
} );
```

The third optional argument is the base directory override, you can use it to override the `resources/assets/less` convention.

# Sass

The `sass` method allows you to compile [Sass](http://sass-lang.com/) into CSS. Assuming your Sass files are stored at `resources/assets/sass`, you may use the method like so:

```js
elixir( function( mix ){
    mix.sass( 'app.scss' );
} );
```

Again, like the `less` method, you may compile multiple Sass files into a single CSS file, and even customize the output directory of the resulting CSS:

```
elixir( function( mix ){
    mix.sass( 
    	[
       	'app.scss',
       	'controllers.scss'
    	], 
   		'public/assets/css' 
   );
} );
```

The third optional argument is the base directory override, you can use it to override the `resources/assets/sass` convention.

# Combine CSS

If you would just like to combine and minify CSS stylesheets into a single file, you may use the `styles` method. Paths passed to this method are relative to the `resources/assets/css` directory and the resulting CSS will be placed in `includes/css/all.css` by convention:

```js
elixir( function( mix ){
    mix.styles( [
        'normalize.css',
        'main.css'
    ] );
} );
```

Of course, you may also output the resulting file to a custom location by passing a second argument to the `styles` method:

```js
elixir( function( mix ){
    mix.styles(
    	[
        	'normalize.css',
        	'main.css'
    	], 
    	'public/assets/css'
   );
} );
```

The third optional argument is the base directory override, you can use it to override the `resources/assets/css` convention.

## Combine Folders

If you need to combine all of the css in a given directory, you may use the `stylesIn` method or globbing patterns. The resulting css will be placed in `includes/css/all.css`:

elixir( function( mix ){
    mix.stylesIn( 'resources/css/some/directory' );
} );


## Combine CSS From Anywhere

If you have multiple css files that you would like to combine into a single file, you may use the `combine` method as well.  Please note that the `combine` method does NOT do any type of compilation or minification.  It is a plain 'ol combination or concatenation of files.

The method assumes the starting place of all paths from the `root` of your application, so not the `resources` folder.  The first argument is a single location or an array of locations, the second argument is the output combo file.

```js
elixir( function( mix ){
    mix.combine( 
    	[
        	'resources/assets/vendor/date.css',
        	'resources/assets/vendor/app.css',
    	],
    	"includes/css/combined.css"
    );
    
    mix.combine( 
    	[
            'resources/assets/vendor/*.css'
    	],
    	"includes/css/combined.css"
    );
} );
```

# Source Maps

Source maps are enabled out of the box. So, for each file that is compiled you will find a companion `*.css.map` file in the same directory. This mapping allows you to trace your compiled stylesheet selectors back to your original Sass or Less while debugging in your browser.

If you do not want source maps generated for your CSS, you may disable them using a simple configuration option:

```
// No more source maps ma!
elixir.config.sourcemaps = false;

elixir( function( mix ){
    mix.sass( 'app.scss' );
} );
```


