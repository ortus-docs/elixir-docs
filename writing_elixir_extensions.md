# Writing Elixir Extensions

> **Tip:** Looking at the code for the official ColdBox Elixir extensions will help immensely as you begin writing your own extensions.  You can find them in the at [ColdBox Elixir](https://github.com/coldbox-elixir) GitHub organization prefixed with `extension-`.

If you need more flexibility than Elixir's `task` method can provide, you may create custom Elixir extensions. Elixir extensions allow you to pass arguments to your custom tasks. For example, you could write an extension like so:

```js
// File: elixir-extensions.js

var gulp 	= require( 'gulp' );
var shell 	= require( 'gulp-shell' );
var elixir	= require( 'coldbox-elixir' );

var Task = elixir.Task;

elixir.extend( 'speak', function( message ){

    new Task( 'speak', function(){
		return gulp.src( '' ).pipe( shell( 'say ' + message ) );
    });

});

// Then we can call it
mix.speak( 'Hello World' );

```

That's it! Notice that your Gulp-specific logic should be placed within the function passed as the second argument to the `Task` constructor. You may either place this at the top of your Gulpfile, or instead extract it to a custom tasks file. For example, if you place your extensions in `elixir-extensions.js`, you may require the file from your main Gulpfile like so:

```
// File: Gulpfile.js

var elixir = require( 'coldbox-elixir' );

require( './elixir-extensions' )

elixir( function( mix ){
    mix.speak( 'Tea, Earl Grey, Hot' );
});
```
