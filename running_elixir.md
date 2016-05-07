# Running Elixir

Elixir is built on top of Gulp, so to run your Elixir tasks you only need to run the `gulp` command in your terminal, as you will already have a `Gulpfile.js` in your project root that will resemble the following:

```js
var elixir = require( 'coldbox-elixir' );

/*
 |--------------------------------------------------------------------------
 | Elixir Asset Management
 |--------------------------------------------------------------------------
 |
 | Elixir provides a clean, fluent API for defining some basic Gulp tasks
 | for your ColdBox application. By default, we are compiling the Sass
 | file for our application, as well as publishing vendor resources.
 |
 */

elixir( function( mix ){
	
} );
```


Please note that by adding the `--production` flag to the command will instruct Elixir to minify your CSS and JavaScript files:

```bash
// Run all tasks...
gulp

// Run all tasks and minify all CSS and JavaScript...
gulp --production
```

You can also programmatically add a production flag into your `Gulpfile.js` by using the configuration option: `elixir.config.production` boolean flag.

## Watching Assets For Changes

Since it is inconvenient to run the gulp command on your terminal after every change to your assets, you may use the `gulp watch` command. This command will continue running in your terminal and watch your assets for any changes. When changes occur, new files will automatically be compiled or tested:

```
gulp watch
```