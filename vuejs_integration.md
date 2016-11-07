# Vue.js Integration

ColdBox Elixir has an optional installation package to provide you with [Vue.js](vuejs.org) and [Vueify component](https://github.com/vuejs/vueify) compilation out of the box.  This will allow you to create `.vue` extension components, integrate with Vue.js and Browserify will compile them for you.

You will begin by installing Vue.js via npm: `npm install vue --save`.  This will add `Vue` as a dependency for your project in your project's `package.json` and into the `node_modules` directory.  The following is the `package.json` you should use when integrating with Vue.js:

**package.json**

```js
{
  "private": true,
  "devDependencies": {
    "coldbox-elixir": "1.1.0",
    "gulp": "^3.9.1"
  },
  "dependencies": {
    "vue": "^2.0.0"
  }
}
```

Then create your normal JavaScript and Vue components in your `resources/assets/js` folder.  You can even use the new (EcmaScript6)[https://babeljs.io/docs/learn-es2015/] syntax if you like, then just mix them up using the `webpack`, `rollup`, or `browserify` method:

**Gulpfile.js**

```js
var elixir = require( "coldbox-elixir" );


elixir( function( mix ){
    mix.webpack( "app.js" );
});
```

Your `App.js` can look like this:

**resources/assets/js/App.js**

```js
import Vue from 'vue';
import Profile from './components/Profile.vue';

new Vue({
  el: '#app',
  data: {
    message: "Hello, world!"
  }
});
```

And you can import any components following the same relative path of the `resources/assets/js` folder.

You can also use the optional `.vue` syntax which allows you to co-locate your template, styles, and scripts.  Read more about the `.vue` syntax [here](https://github.com/vuejs/vueify).


**resources/assets/js/App.js**

```js
import Vue from 'vue';
import Profile from './components/Profile.vue';

new Vue({
  el: '#app',
  components: { Profile }
});
```

To use this syntax, you will need the [`coldbox-elixir-vue`](https://github.com/coldbox-elixir/extension-vue) or [`coldbox-elixir-vue-2`](https://github.com/coldbox-elixir/extension-vue-2) extension, depending on which version of Vue.js you are running. See the individual GitHub pages for installation instructions.

**resources/assets/js/components/Profile.vue**

```
<template>
  <div class="profile">
    {{ name }}
  </div>
</template>

<script>
export default {
  data () {
    return {
      name: 'Luis Majano'
    };
  }
};
</script>

<style>
.profile {
    background: #eee;
    border: 1px solid #aaa;
    border-radius: 2em;
    margin: 2em auto;
    min-height: 150px;
    padding: 2em;
    width: 300px;
}
</style>
```

You would then use this in your ColdBox layout or view like so:

```html
<div id="app">
	<profile></profile>
</div>
<script src="/includes/js/App.js"></script>
```
