# Vue.js Integration

ColdBox Elixir has an optional installation package to provide you with [Vue.js](vuejs.org) and [Vueify component](https://github.com/vuejs/vueify) compilation out of the box.  This will allow you to create `.vue` extension components, integrate with Vue.js and Browserify will compile them for you.

You will begin by installing Vue.js via npm: `npm install vue --save`.  This will add `Vue` as a dependency for your project in your project's `package.json` and into the `node_modules` directory.  The following is the `package.json` you should use when integrating with Vue.js:

**package.json**

```js
{
  "private": true,
  "devDependencies": {
    "gulp": "^3.9.1"
  },
  "dependencies": {
    "coldbox-elixir": "1.1.0",
    "vue": "^1.0.21"
  }
}
```

Then create your normal JavaScript and Vue components in your `resources/assets/js` folder.  You can even use the new (EcmaScript6)[https://babeljs.io/docs/learn-es2015/] syntax if you like, then just mix them up using the `browserify` method:

**Gulpfile.js**

```js
var elixir = require( 'coldbox-elixir' );


elixir( function( mix ){
    mix.browserify( 'App.js' );
});
```

Your `App.js` can look like this:

**resources/assets/js/App.js**

```js
import Vue from 'vue';
import Profile from './components/Profile.vue';

new Vue({
  el: '#app',
  components: { Profile }
});
```

And you can import any components following the same relative path of the `resources/assets/js` folder:

_(This example uses the optional `.vue` syntax which allows you to co-locate your template, styles, and scripts.  Read more about the `.vue` syntax [here](https://github.com/vuejs/vueify).)_

**resources/assets/js/components/Profile.vue**

```js
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

You would then use this in your page like so:

```html
<div id="app">
	<profile></profile>
</div>
<script src="/includes/js/App.js"></script>
```
