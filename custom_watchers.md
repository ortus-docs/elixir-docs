# Custom Watchers

If you would like your custom task to be re-triggered while running `gulp watch`, you may register a watcher:

```js
new Task( 'speak', function(){
	return gulp.src( '' ).pipe( shell( 'say ' + message ) );
})
.watch( './app/**' );

```


