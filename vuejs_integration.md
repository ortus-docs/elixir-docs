# Vue.js Integration

ColdBox Elixir lets you work with `.vue` files out of the box.

You will begin by installing Vue.js via npm: `npm install vue`.  This will add `Vue` as a dependency for your project in your project's `package.json` and into the `node_modules` directory.  The following is the `package.json` you should use when integrating with Vue.js:

**package.json**

```js
{
  "private": true,
  "devDependencies": {
    "coldbox-elixir": "3.0.0",
  },
  "dependencies": {
    "vue": "^2.0.0"
  }
}
```

Then create your normal JavaScript and Vue components in your `resources/assets/js` folder.

```js
const elixir = require("coldbox-elixir");

module.exports = elixir(mix => {
    mix.vue("app.js");
});
```

`mix.vue` accepts a configuration object as the second parameter which has the following defaults:

```js
{
    name: this.withoutExtension(filename),
    outputDirectory: "includes/js/",
    entryDirectory: "resources/assets/js/"
}
```

Your `App.js` can look like this:

**resources/assets/js/App.js**

```js
import Vue from "vue";

new Vue({
  el: "#app",
  data: {
    message: "Hello, world!"
  }
});
```

And you can import any components following the same relative path of the `resources/assets/js` folder.

You can also use the optional `.vue` syntax which allows you to co-locate your template, styles, and scripts in a single-file component.

**resources/assets/js/App.js**

```js
import Vue from "vue";
import Profile from "./components/Profile.vue";

new Vue({
  el: "#app",
  components: { Profile }
});
```

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
      name: "Luis Majano"
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

Any style blocks in your `.vue` components will be extracted as well to the same directory as your javascript file as
a css file.  For example, if you were compiling `mix.vue( "app.js" )` Elixir would generate a `includes/js/app.css` file
containing the css for the style blocks used in that entrypoint.

> Note: there are some drawbacks with style blocks in Vue components and Elixir.
> if you are creating multiple entry points with multiple `mix.vue` calls, any
> style blocks in shared components will be duplicated in each of the css files.
> Additionally, because Elixir is already extracting other css files, style blocks
> in Vue components are always extracted.  For these reasons, we recommend using
> other approaches to managing your css with Vue components and Elixir.
