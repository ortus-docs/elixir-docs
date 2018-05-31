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
