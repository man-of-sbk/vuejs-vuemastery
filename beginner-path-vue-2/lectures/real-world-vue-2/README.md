# Vue CLI (Command Line Interface)
1. allows us to select which libraries our project will be using Then automatically plugs them into the project.
2. It Configures Webpack When we build our app `with Webpack`, all of our JavaScript files, our CSS, and our dependencies get properly bundled together, minified and optimized.
3. allows us to write our HTML, CSS & JavaScript however we like. We can use single-file .vue components, TypeScript, SCSS, Pug, the latest versions of ECMAScript, etc.
4. enables Hot Module Replacement (HMR) So when you save your project, changes appear instantly in the browser. This configuration is based on [webpack-dev-server](https://github.com/webpack/webpack-dev-server).

## installation
1. install `npm`.
2. run `npm i -g @vue/cli`.

## Creating a Vue project using Vue CLI
There are two ways we can create our project. With the newer Vue UI, or directly from the command line, which we’ll do now with:

1. run the `create` command.

```shell
vue create real-world-vue
```

1. choose the `Manually select features` option, then hit `enter`.

```shell
Vue CLI v4.5.13
? Please pick a preset: (Use arrow keys)  
  Default ([Vue 2] babel, eslint)
  Default (Vue 3) ([Vue 3] babel, eslint) 
> Manually select features
```

2. hit `space` to select features for our project as below, then hit `enter` to go to the next step.

```shell
Vue CLI v4.5.13
? Please pick a preset: Manually select features
? Check the features needed for your project: 
 (*) Choose Vue version
 (*) Babel
 ( ) TypeScript
 ( ) Progressive Web App (PWA) Support        
 (*) Router
 (*) Vuex
 ( ) CSS Pre-processors
>(*) Linter / Formatter
 ( ) Unit Testing
 ( ) E2E Testing
```

3. choose the `Vue 2` option, then hit `enter`.

```shell
Vue CLI v4.5.13
? Please pick a preset: Manually select features
? Check the features needed for your project: Choose Vue version, Babel, Router, Vuex, Linter
? Choose a version of Vue.js that you want to start the project with (Use arrow keys)        
> 2.x
  3.x
```

4. use `history mode` for router, then hit `enter`.

```shell
Vue CLI v4.5.13
? Please pick a preset: Manually select features
? Check the features needed for your project: Choose Vue version, Babel, Router, Vuex, Linter
? Choose a version of Vue.js that you want to start the project with 2.x
? Use history mode for router? (Requires proper server setup for index fallback in production) (Y/n) Y
```

5. choose the `ESLint + Prettier` option.

```shell
Vue CLI v4.5.13
? Please pick a preset: Manually select features
? Check the features needed for your project: Choose Vue version, Babel, Router, Vuex, Linter
? Choose a version of Vue.js that you want to start the project with 2.x
? Use history mode for router? (Requires proper server setup for index fallback in production) Yes
? Pick a linter / formatter config: 
  ESLint with error prevention only 
  ESLint + Airbnb config
  ESLint + Standard config
> ESLint + Prettier
```

6. choose the `Lint on save` option, then hit `enter`.

```shell
Vue CLI v4.5.13
? Please pick a preset: Manually select features
? Check the features needed for your project: Choose Vue version, Babel, Router, Vuex, Linter
? Choose a version of Vue.js that you want to start the project with 2.x
? Use history mode for router? (Requires proper server setup for index fallback in production) Yes
? Pick a linter / formatter config: Prettier
? Pick additional lint features: (Press <space> to select, <a> to toggle all, <i> to invert selection)
>(*) Lint on save
 ( ) Lint and fix on commit
```

7. choose the `In dedicated config files`, then hit `enter`.

```shell
Vue CLI v4.5.13
? Please pick a preset: Manually select features
? Check the features needed for your project: Choose Vue version, Babel, Router, Vuex, Linter
? Choose a version of Vue.js that you want to start the project with 2.x
? Use history mode for router? (Requires proper server setup for index fallback in production) Yes
? Pick a linter / formatter config: Prettier
? Pick additional lint features: Lint on save
? Where do you prefer placing config for Babel, ESLint, etc.? (Use arrow keys)
> In dedicated config files
  In package.json
```

8. say `No` to the `Save this as a preset for future projects?` option, then hit `enter`.

```shell
Vue CLI v4.5.13
? Please pick a preset: Manually select features
? Check the features needed for your project: Choose Vue version, Babel, Router, Vuex, Linter
? Choose a version of Vue.js that you want to start the project with 2.x
? Use history mode for router? (Requires proper server setup for index fallback in production) Yes
? Pick a linter / formatter config: Prettier
? Pick additional lint features: Lint on save
? Where do you prefer placing config for Babel, ESLint, etc.? In dedicated config files
? Save this as a preset for future projects? (y/N) N
```

9. choose `npm` as the package manager of the project, then hit `enter`.

```shell
Vue CLI v4.5.13
? Please pick a preset: Manually select features
? Check the features needed for your project: Choose Vue version, Babel, Router, Vuex, Linter
? Choose a version of Vue.js that you want to start the project with 2.x
? Use history mode for router? (Requires proper server setup for index fallback in production) Yes
? Pick a linter / formatter config: Prettier
? Pick additional lint features: Lint on save
? Where do you prefer placing config for Babel, ESLint, etc.? In dedicated config files
? Save this as a preset for future projects? No
? Pick the package manager to use when installing dependencies: 
  Use Yarn
> Use NPM
```

## Create a Vue project using Vue UI
With `Vue UI`, it is also easier to alter our projects' configurations, shows more information about what is happening with a project when we serve/build it in a friendly UI and allows us to add, install plugins into our projects with a few clicks.

## Serve a project
use the following command:

```shell
npm run serve
```

# Touring our Vue Project
## directories
The `node_modules` directory is where all of the libraries we need to build Vue are stored.

In the `public` directory, you place any `static assets` you don’t want to be run through Webpack when we build our project.

## directories nested inside the `src` directory
You’ll want to put the majority of your assets, such as `images and fonts`, in the `assets` directory so they `can be optimized by Webpack`.

The `components` directory is where we store the components, or building blocks, of our Vue app.

The `views` directory is where we store files for the different `views`, or `pages`, of our app.

## files
The `App.vue` file is the `root component` that all other components are nested within.

The `main.js` file is what renders our App.vue component (and everything nested within it) and mounts it to the DOM.

Below that we have a `router.js` file is for `Vue Router`, and the `store.js` file is for `Vuex`.

Finally, we have a `.gitignore` file where we can specify what we want git to ignore, along with a `babel.config.js` file and our `package.json`, which helps npm identify the project and handle its dependencies.

# How the App is Loaded
```js
import Vue from "vue";
import App from "./App.vue";
import router from "./router";
import store from "./store";
Vue.config.productionTip = false;
new Vue({
  router,
  store,
  render: h => h(App)
}).$mount("#app");
```

In our `main.js` file, we see that we’re importing `Vue`, along with our root `App.js` component, as well as our `router` and `store`. We are then creating a `new Vue instance`, telling it to use the `router` and `store`, and to `render App` (our root component) and `mount it to the DOM`, where this id of `app` is.

peek inside our `public/index.html` file, we can see there’s a div with the id of "`app`", which means this is `where our App will be mounted`.

```html
<div id="app">Our App will be mounted here</div>
```

# The Build Process
If we take a closer look at our `public/index.html` file, we see this comment:

```html
<!-- built files will be auto injected -->
```

when ran, the command `npm run build` will build our project, and when it’s complete, it says, “The `dist` directory is ready to be deployed”.

Inside the `dist` directory there is a `js` directory, `Webpack` has packaged our app and given us these `new bundled JavaScript files`. If we open up our `index.html` inside the `dist` folder, we can see that there are now two `script` tags, which have been `auto injected`, where the comment `built files will be auto injected` used to be.

```html
<script src=/js/chunk-vendors.24971a46.js></script><script src=/js/app.5f694b83.js></script>
```

The `chunk-vendors.24971a46.js` file contains all of our `dependencies`.

The `App.5f694b83.js` file below it contains all of our application-specific code, including the code that was in our `main.js`, which renders and mounts our App.

`dist` means "`distributable`", the `compiled code/library`.

# Vscode Vue development-enhancing extentions
1. `Vetur`:
   1. syntax highlighting.
   2. `command + p` to search for vue files.
   3. snippets.
   4. the `emmet` feature supporting shortcuts for `html`, `css`, `scss`, ....
  
2. `Eslint`.
3. `Prettier`.

## Configuring ESLint
When we created our project by the `CLI`, we chose to create it with `dedicated config files`, giving us an `.eslintrc.js` file, where we can configure ESLint for this project. If we didn't opt to create dedicated files, we would find the ESLint configurations within our `package.json`.

in our `.eslintrc.js` file, we’ll add:

```json
'plugin:prettier/recommended'
```

This will enable `Prettier` support in `ESLint` with the default settings. So our file now looks like this:

```js
 module.exports = {
  root: true,
  env: {
    node: true
  },
  'extends': [
    'plugin:vue/essential',
    'plugin:prettier/recommended', // we added this line
    '@vue/prettier'
  ],
  rules: {
    'no-console': process.env.NODE_ENV === 'production' ? 'error' : 'off',
    'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off'
  },
  parserOptions: {
    parser: 'babel-eslint'
  }
}
```

## Configuring Prettier
Create a file, named `.prettierrc.js` to add some special settings and inside, we’ll type:

```js
module.exports = {
  singleQuote: true,
  semi: false
}
```

This will convert `double quotes` to `single quotes`, and make sure that `semicolons` are not automatically inserted.

## User Settings
click on `Code` in the top navigational bar, then `Preferences`, then `Settings`. This will bring up a `User Settings window` where you can add settings in json. First, we want to add:

```json
{
  "vetur.validation.template": false
}
```

This will `turn off` `Vetur’s linting feature`. We’ll be relying instead on `ESLint + Prettier`.

Now we want to tell `ESLint` what languages we want it to validate (`vue`, `html`, and `javascript`) and set `autoFix` to `true` on each:

```json
{
  "eslint.validate": [
    {
      "language": "vue",
      "autoFix": true
    },
    {
      "language": "html",
      "autoFix": true
    },
    {
      "language": "javascript",
      "autoFix": true
    }
  ]
}
```

If you get the following warning:

```txt
Auto Fix is enabled by default. Use the single string form.(2)

An array of language ids which should be validated by ESLint. If not installed ESLint will show an error.
```

Use the following syntax instead:

```json
{
  "eslint.validate": [
      "vue",
      "html",
      "javascript"
  ]
}
```

Then for good measure, we’ll tell `ESLint` to `autoFixOnSave`.

```json
{
  "eslint.autoFixOnSave": true,
}
```

If you get this warning: `he setting is deprecated. Use editor.codeActionsOnSave instead with a source.fixAll.eslint member.`, try the following syntax instead:

```json
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
}
```

And tell our editor itself to `formatOnSave`.

```json
"editor.formatOnSave": true,
```

## Additional Tools (Vscode extension)
1. `Copy Relative Path`
   1. In order to get a relative path of a file, right click on the file, then select `Copy Relative Path`.
   2. **Note**: `@` is an alias to the `src` folder.

2. If you’re interested in installing some `additional convenient code snippets`, get the `Vue VSCode Snippets` extension, created by Core Vue Team Member Sarah Drasner.
   1. **note**: if you’re using this Snippets extension, it is recommended to add the following line to your `User Settings`, making sure these snippets `aren’t conflicting` with `Vetur’s`.

```json
{
  "vetur.completion.useScaffoldSnippets": false
}
```

# Vue Router Basics
Vue has its own official routing solution, called `Vue Router`.

## How Vue Router gets loaded (by Vue CLI)
### router.js
here in the file `src/router/index.js`, we are telling Vue to use `Vue Router`, a `Vue plugin`. Learn more [here](https://vuejs.org/v2/guide/plugins.html).

```js
import Vue from "vue";
import VueRouter from "vue-router";
import Home from "../views/Home.vue";

Vue.use(VueRouter); // tell Vue to use Vue Router
```

then we are exporting an instance of Router with some routes defined:

```js
const routes = [
  {
    path: "/",
    name: "Home",
    component: Home,
  },
  {
    path: "/about",
    name: "About",
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    component: () =>
      import(/* webpackChunkName: "about" */ "../views/About.vue"),
  },
];

const router = new VueRouter({
  base: process.env.BASE_URL,
  routes,
});

export default router;

```

The `path` indicates the URL that the user will be taken to. In this first route, there’s only the `/`, meaning this is the `root`, the homepage of our application.

The `name` allows us to give this route a name so we can use that name throughout our application `to refer to this route`.

The `component` allows us to specify which component to render at that route.

####  Are About and Home “components” or “views”?
=> They are `components`. We place components in both the `/components` and `/views` folders. It’s a best practice to put the components that get loaded by `Vue Router` in the `/views` directory. You then keep the modular (`reusable`) components in your `/components` directory.

**Note**: If we wanted we could put all our components inside the /components directory. We could also rename the `/views` directory to `/pages`.

### main.js
notice that we tell our `Vue instance` to use the router we’ve imported:

```js
// ...
import router from "./router";

// ...

new Vue({
  router,
// ...
```

### App.vue
Looking within the `app.vue` file, there’s a div with the id of `nav` and inside of it there are some `router-links`, which are `global components` we have access to.

```html
<div id="nav">
  <router-link to="/">Home</router-link> |
  <router-link to="/about">About</router-link>
</div>
```

below them is:

```html
<router-view/>
```

`<router-link>` is a component (from the `vue-router` library) whose job is to link to a specific route. This component will eventually be replaced by an `a` tag when it is rendered on the browser. We can also add class to the `router-link` component and the class will be attached to its associated `a` element.

`<router-view/>` is essentially a placeholder where the contents of our component `will be rendered` onto the page.

## Using Named Routes
Another way we can create router links is by using `named routes`. Remember how in our `router.js` each of our routes has a name? We can use these names. So instead of:

```html
<router-link to="/">Home</router-link>
<router-link to="/about">About</router-link>
```

We can write:

```html
<router-link :to="{ name: 'home' }">Home</router-link> |
<router-link :to="{ name: 'about' }">About</router-link>
```

These have equivalent functionality, but Vue is using the `name` to look up the path that we want to use. Using named routes we’d only have to change that path in one place instead of everywhere in our app.

## Problem: Changing Routes
Sometimes in our applications, after we ship them to production we need to change their paths. Like from `/about` to `/about-us` . How might we deal with this?

### Solution #1: Redirect
the first step is to change our original route. `However`, there might be links around the internet to our `/about` page. Therefore, we will make a redirect from `/about` to `/about-us`.

```js
const routes = [
  // ...
  {
    path: '/about-us',
    name: 'About',
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    component: () =>
      import(/* webpackChunkName: 'about' */ '../views/About.vue'),
  },
  {
    path: '/about',
    redirect: { name: 'About' }
  },
];
```

**Note**:
1. we’re using the named route for the redirect. We could have also used `redirect: "/about-us"` to get the same functionality, but this is hard-coding a URL in one more place we’d have to change if the path changed.
2. creating a new `about-us` route and redirect to the existing `about` route does not solve the problem, since whenever a visit is made to the `about-us` route, it will be redirected to the `about` route.

### Solution #2: Alias
Instead of redirecting the old path we might just want to alias it, meaning just provide a `duplicate path` `to the same content`. We could update that path and provide an alias to the old path:

```js
const routes = [
  // ...
  {
    path: '/about-us',
    name: 'About',
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    component: () =>
      import(/* webpackChunkName: 'about' */ '../views/About.vue')
  }
];
```

Now the user can go to /about or /about-us and they’ll get the same content.

## dynamic routes (liek `/users/insert-name-here`)
```js
const routes = [
  {
    path: '/event/:id',
    name: 'event-show',
    component: EventShow
  },
]
```

`:id` is called a dynamic segment. In the template, we can access this parameter like so.

```html
<template>
  <h1>Showing event #{{ $route.params.id }}</h1>
</template>
```

**Note** that the dynamic segment is required, `router-link` elements, pointing to the above dynamic route `must` define a value for the dynamic segment, or else a warning will be thrown to the browser, and the `router-link` element will not work and is redirectd to the root route (`/`). The following code shows how we can define a paramater for a `dynamic route` in a `router-link` element.

```html
<router-link :to="{
  name: 'event-show',
  params: {
    id: '1'
  }
}">Show Event #1</router-link>
```

the `$route` object is a global one, added by the `Vue Router` Vue plugin. It represents the state of the `current active route` and contains data about the route including the `params`.

This is how `Vue Router` makes the `$route` object accessible globally. For information [here](https://github.com/vuejs/vue-router/blob/dev/src/install.js):

```js
Object.defineProperty(Vue.prototype, '$router', {
  get () { return this._routerRoot._router }
})
```

### Using Props for Routes
A better way to handle the value of a dynamic segment inside a dynamic route is to set `props: true` as we define the dynamic route. By doing so, the value of the dynamic segment will be passed to the component, rendered by the dynamic route as a `prop` of the component.

```js
const routes = [
  {
    path: '/event/:id',
    name: 'event-show',
    component: EventShow,
    props: true // <--
  }
]
```

```html
<!-- EventShow component -->
<template>
  <div>
    <h1>Showing event #{{ $route.params.id }}</h1> <!-- the "$route" object is still available anyway -->
    <h1>Showing event #{{ id }}</h1>
  </div>
</template>

<script>
export default {
  props: ['id'] // remember to define a prop associated to the ":id" dynamic segment
};
</script>
```

## Hash mode
the default `mode` of a `Vue Router` instance is `hash` meaning that it puts a `#` character after the base url of our app. For instance: `http://localhost:8080/#/event`.

### Hash mode explaination
URL can contain some data prepended with a `#` character. The `#` part of the URL is called the `hash fragment`.

It’s normally used so that people can link to a particular section in a HTML page, specifically anchor tags. Like so:

```html
<!-- http://somedomain.com/page#routing-strategies -->
<a name="routing-strategies"></a>
```

The browser would open `somedomain.com/page` and then scroll down so that the <a name="routing-strategies"></a> tag is at the top of the page. However it has another very important characteristic in that `anything` past the `#` in a URL `never gets sent to the server`.

So if your URL was `https://codecraft.tv/contact/#/foo/moo/loo` then the browser makes a GET request to `https://codecraft.tv/contact/` only. If you were to look at your logs on the server you would never see any reference to `#/foo/moo/loo`.

Another way to think about the hash fragment is that it’s for storing the state of your client application. It’s therefore an ideal solution for implementing `client side routing`.

1. It’s part of the URL so can be bookmarked and sent to other people.
2. It won’t confuse the server side since the hash fragment is never sent to the server.
3. It can be programmatically changed via JavaScript.

And that’s exactly why, for a number of years, the primary way of implementing `client-side routing` was via `hash fragments`.

```txt
localhost:4040/#/search
localhost:4040/#/artist/1234/tracks
```

According to the the server there is only ever one URL `localhost:4040`, the other hash fragment stuff is `ignored` by the server. This is why we call what we are building a `Single Page Application`, there is only `one page` requested from the server. In the above example it’s `localhost:4040` — the other pages are just changes to the hash fragment which the `client application` deals with.

## History mode + server configuration
most websites don’t use `hash mode`, you don’t want it either. In order to remove it we need to add some configuration to our `router/index.js`:

```js
const router = new VueRouter({
  mode: 'history', // <--
  base: process.env.BASE_URL,
  routes,
});
```

This tells Vue to use the `browser` `history.pushState` API to change the URL. This api allows us to change the URL and not have the browser request the page from the server and `without` needing to use a `hash fragment`.

So if we were at:

```txt
localhost:4040/search
```

By using the `pushstate` API we can change the URL to:

```txt
localhost:4040/artist/1234/tracks
```

And the browser won’t make a GET request to the server for `/artist/1234/tracks`.

**Unfortunately** it has one big downside: if we `reload` the page, or bookmark it and open it later, the browser would make a request to the server for e.g. `localhost:4040/artist/1234/tracks`. By using a `hash fragment` the server `never` needs to know about any application URL, it will only ever get asked for the `root page` and it will only ever return the `root page`.

So with `history` mode, we need to co-operate with a server side to serve one file, no matter what route is requested. The `Vue Router` documentation has a bunch of [Example Server Configurations](https://router.vuejs.org/guide/essentials/history-mode.html#example-server-configurations) showing how to do this.

### why isn’t history mode the default one?
the browser `history.pushState` API is only supported in `IE10+`, while the current version of Vue provides support for `IE9+`.

### Caveat: Handling 404s
A side effect of configuring our server as above is that it will `no longer report 404 error` as all not-found paths now serve up our `one and only` html file.

There are different ways to combat this, one of which is by creating a `/views/FileNotFound.vue component`, which gets loaded if `none of the existing paths match`. To do this we would place this `catch-all route` at `the bottom` of our `router/index.js`, if the URL `doesn’t match` any of the other routes it will match this route.

```js
const router = new VueRouter({
  mode: 'history',
  routes: [
    ...
    { path: '*', component: NotFoundComponent }
  ]
})
```

We obviously aren’t going to cover all the different ways you can use routing. I recommend you consult the Vue Router documentation for more details, like `nested routes`, `transition effects`, `programmatic navigation`, `passing props to routes`, and `SEO concerns`.

# Single File Component
Vue components combine markup (usually HTML), logic (JavaScript), and style (usually CSS) into one, single file. Hence the name: `single-file component`.

```html
<template>
  <div>
  // here is where we lay out the structure of our component
  </div>
</template>

<script>
  export default {
    // here is where we give our component the ability to behave and perform logic
  }
</script>

<style scoped>
// here is where we design the appearance of our component
</style>
```

Vue also allows you to use alternatives to the traditional HTML, JS and CSS setup. For example, you could use Pug, TypeScript and SCSS instead by adding the appropriate lang attributes.

```html
<template lang="pug">
</template>

<script lang="ts">
</script>

<style lang="scss" scoped>
</style>
```

**Note**: make sure you have the proper `loaders` setup and your Webpack is configured to handle these alternatives. Thanks to the helpful Vue CLI 3, this process is pretty simple.

For example, if we wanted to use SCSS, we’d need to make sure we install sass-loader and its peer dependency node-sass. We can quickly do this from the command line or install these dependencies from the Vue UI’s Dependencies tab instead.

```shell
npm install --save-dev sass-loader node-sass
```

## Component Template
```html
<template>
  <div>
    <h4>Park Cleanup</h4>
  </div>
</template>
```

a component’s template needs to have only one root element.

```html
<script>
export default {}
</script>
```

`export default` is the ES6 export statement for exporting a JavaScript module that can be imported from another location with the import statement, which we’ll get to in the next section.

```html
<style scoped>
h4 {
  color: green
}
</style>
```

Notice the `scoped` attribute? This is a convenient way to `isolate` this style `to only this component`. If we had not scoped this style rule, we could end up with `other` h4 elements in our app being styled green.

## Nesting Components
In order to use the component (named `EventCard`) inside another one (named `EventList`), we’ll need to import it. Using the Vue VSCode Snippet `vimport` and register the `EventCard` component as a child component of the `EventList` one.

**Note**: we do not need to have the `script` tag as well as add the `export` statement in the `EventCard` to make it importable.

```html
<script>
import EventCard from '@/components/EventCard.vue'; // import the EventCard component

export default {
  components: {
    EventCard, // register the EventCard as a child component
  }
}
</script>
```

## Adding Global Styles
There are several different ways to handle this, but we’ll be adding global styles into the `style` section of our `App.vue` component. Please note that it’s recommended to only store your global styles `in one place` to avoid potential conflicts.

# Global Components
While we could `import` and `locally register` a component within every parent one needing it, that could become time-consuming and add unnecessary code. It would be more efficient to `globally register` this component (make the component available to every component within our application).

## Basic Global Registration
Many of your components will be relatively generic, possibly only wrapping an element like an input or a button. We sometimes refer to these as `base components` and they tend to be used very frequently across your components.

We’ll build out a component, called `BaseIcon.vue`. Now if we go into our main.js file, we can do the following two steps:
1. Import the `BaseIcon.vue` component.
2. `Globally register` it via: `Vue.component('BaseIcon', BaseIcon)`.

**Note**: we need to register our component `above` where we’re creating our `root Vue instance`.

## Automatic Global Registration
If you get to the point you have a bunch components that need to be globally registered, there’s a way to do so automatically.

Firstly, install `Lodash`, a JavaScript library that provides utility functions for common programming tasks.

### Main.js
```js
import Vue from "vue";
import App from "./App.vue";
import router from "./router";
import store from "./store";

// the example starts here
import upperFirst from "lodash/upperFirst";
import camelCase from "lodash/camelCase";

const requireComponent = require.context(
  './components',
  false,
  /Base[A-Z]\w+\.(vue|js)$/
)

requireComponent.keys().forEach(fileName => {
  const componentConfig = requireComponent(fileName)

  /**
   * We may have file names like BaseIcon.vue(PascalCase) or base-icon.vue (kebab-case). If the name is base-icon.vue,
   * we need to convert it to PascalCase, which will allow the component to be referenced as both PascalCase (e.g. <BaseIcon/>)
   * or kebab-case (e.g. <base-icon/>).
  */
  const componentName = upperFirst(
    camelCase(
      fileName.replace(/^\.\/(.*)\.\w+$/, '$1')
    )
  )

  /**
   * we’re registering each component globally
  */
  Vue.component(
    componentName,
    /**
     * telling Vue to look for the component options on .default, which will exist if the component was exported with
     * "export default". Otherwise, Vue will fall back to the module’s root, which is what’s exported when using
     * "module.exports =" instead of "export default".
    */
    componentConfig.default || componentConfig
  )
});
// the example ends here

Vue.config.productionTip = false;

new Vue({
  router,
  store,
  render: (h) => h(App),
}).$mount("#app");
```

we’re using `require.context`, which is `a feature of Webpack`. This is a function that allows you to pass in `3 arguments`:
1. A directory to `search within`.
2. A flag indicating whether `subdirectories` should be searched, too.
3. A regular expression to `match files` against.

Webpack looks for `require.context()` in the code while building, then requires every matching file to ensure it’s in your compiled bundle, `even if it’s never used`.

### Working with SVG
instead of working with SVG code directly in our component, we’ll use the `feather-icons` library is basically a collection of symbols with a simple interface to render whichever one you like.

```shell
npm install feather-icons --save
```

#### How to use
First, import the library and then add a computed property called `svg`:

```html
<script>
import feather from 'feather-icons'
export default {
  computed: {
    svg() {
      /**
       * we get an icon from the icons dictionary by name, for example, "activity" for the "activity icon". And then,
       * we use the "toSvg" method to get the SVG of the icon. The class property is a configuration option that we use
       * to add a class attribute to the SVG.
      */
      return feather.icons['activity'].toSvg({ class: "icon" })
    }
  }
}
</script>
```

```html
<template>
  <div class="icon-wrapper" v-html="svg"></div>
</template>
```

The final rendering will look something like this:

```html
<div class="icon-wrapper">
  <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-activity icon"><polyline points="22 12 18 12 15 21 9 3 6 12 2 12"></polyline></svg>
</div>
```

**Note**: DOM elements do not have the `html` attribute as well as the `text` one. If we want to attach DOM elements or text to a component, we have to use `.innerHTML =` or `.text =` respectively. Fortunately, there are 2 directives help us to do these works within our component's template which are `v-html` and `v-text`.

the `toSvg` method also allows other optional configurations such as `width` and `height` to control the size of the icon. To make our component more dynamic, we can add props that allow us to optionally alter its width and height. By default, the icon will be `24px` by `24px`, unless we feed different values in as props.

```html
<template>
  <div class="icon-wrapper" v-html="svg"></div>
</template>

<style scoped>
</style>

<script>
import feather from 'feather-icons'
export default {
  props: {
    name: String, // the name of the symbol we want to use
    width: {
      type: [Number, String],
      default: 24
    },
    height: {
      type: [Number, String],
      default: 24
    }
  },
  computed: {
    svg() {
      /**
       * we get an icon from the icons dictionary by name, for example, "activity" for the "activity icon". And then,
       * we use the "toSvg" method to get the SVG of the icon. The class property is a configuration option that we use
       * to add a class attribute to the SVG.
      */
      return feather.icons[this.name].toSvg({ 
        class: "icon",
        width: this.width,
        height: this.height
      })
    }
  }
}
</script>
```

```html
<BaseIcon name="activity" width="48" height="48" />
```

# Slots
what if we need the `template` of a component to be `dynamic`. Do we pass in HTML as a `prop`? No. Instead, we do this with `slots`, which serve as a `placeholder` for template code that we can `slot in`.

Instead of making a separate button component for each use case, we can make one `BaseButton` component, which has a `slot` that serves as a placeholder for the template code that describes the action the button performs.

```html
<template>
  <div>
    <button><slot></slot></button>
  </div>
</template>
```

Now, when we use this component, we can write:

```html
<BaseButton>Submit</BaseButton>
```

`Submit` will be what appears where the `slot` was, like so:

```html
<div><button>Submit</button></div>
```

## Default Slot Content
```html
<template>
  <div>
    <button><slot>Submit</slot></button> // default slot content: "Submit"
  </div>
</template>
```

```html
<BaseButton/> <-- displays "Submit"

<!-- Unless we insert different content when we use it: -->
<BaseButton>Update</BaseButton> <-- displays "Update"

<BaseButton>Purchase for ${{ total }}</BaseButton> <-- displays "Purchase for $..."
```

**Note**: In some cases you may want the template code you pass into a `slot` to have access to data from the slot component itself (the child). This is what [Scoped Slots](https://www.vuemastery.com/courses/advanced-components/render-props-scoped-slots/) are for, which is a more advanced topic covered in our Advanced Components course.

## Named Slots
Sometimes it’s useful for a component to have multiple slots. We could start by adding two slots for them, like so:

```html
<template>
  <div>
    <slot name="heading"></slot>
    <slot name="paragraph"></slot>
  </div>
</template>
```

Now, we can use that name in a slot attribute on the template code that will be slotted in

```html
<MediaBox>
  <h2 slot="heading">Adam Jahr</h2>
  <p slot="paragraph">My words.</p>
</MediaBox>
```

### Default Slot
we could get away with only naming one of our slots:

```html
<template>
  <div>
    <slot name="heading"></slot>
    <slot></slot>
  </div>
</template>
```

Vue would still know how to handle this:

```html
<MediaBox>
  <h2 slot="heading">Adam Jahr</h2>
  <p>My words.</p>
</MediaBox>
```

The heading would go into the slot with the name of “heading”, and the paragraph would default into the unnamed slot.

### Slotting a Full Template
It’s also possible to pass in a full `template` like this:

```html
<MediaBox>
  <h2 slot="heading">Adam Jahr</h2>
  <template slot="paragraph">
    <p>My words.</p>
  </template>
</MediaBox>
```

This could be useful if you wanted to slot in multiple elements into the same slot. A `template` allows us to slot in `multiple` elements into the same slot, `without` adding an unnecessary wrapper element.

```html
<MediaBox>
  <h2 slot="heading">Adam Jahr</h2>
  <template slot="paragraph">
    <p>My words.</p>
    <BaseIcon name="book">
  </template>
</MediaBox>
```



