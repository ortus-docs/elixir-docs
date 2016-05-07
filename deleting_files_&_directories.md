# Deleting Files & Directories

You might want to delete some files before, during or after running your build. Since deleting files doesn't work on the file contents, there's no reason to use a gulp plugin within Elixir. You can use the [`del`](https://github.com/sindresorhus/del) module which is included in ColdBox Elixir and it supports multiple files and [globbing](https://github.com/sindresorhus/multimatch#globbing-patterns):


Imagine the following file structure:

```
.
├── dist
│   ├── report.csv
│   ├── desktop
│   └── mobile
│       ├── app.js
│       ├── deploy.json
│       └── index.html
└── src
```

In the gulpfile we want to clean out the contents of the `mobile` folder before running our build:

```js
var del 	= require( 'del' );
var elixir 	= require( 'coldbox-elixir' );

elixir( function( mix ){
	
	del( [
	    'dist/report.csv',
	    // here we use a globbing pattern to match everything inside the `mobile` folder
	    'dist/mobile/**/*',
	    // we don't want to clean this file though so we negate the pattern
	    '!dist/mobile/deploy.json'
	] );
	
} );
```
