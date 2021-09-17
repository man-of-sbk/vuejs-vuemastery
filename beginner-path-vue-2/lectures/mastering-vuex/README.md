# Intro to Vuex
`Vuex 4` was recently released, the latest version of Vuex made to be compatible with `Vue 3`. Almost all `4 APIs` have remained the same from `Vuex 3`, which this course teaches. However, there are a few breaking changes that you can [learn about here](https://next.vuex.vuejs.org/guide/migrating-to-4-0-from-3-x.html#installation-process).

## The Case for State Management
`Vuex` based on `flux`, created by facebook.

`states` are the data that your components `depend on` and `render`. Without `Vuex`, as your app grows, each Vue component might have its own version of state.

But if one component changes its state, and a distant relative is `also using that same state`, we need to communicate that change by communicating events up and passing props down to share data, but that can become overly complicated. Instead, we can consolidate all of our state into one place that contains the current state of our entire application. One `single source of truth`. every component has direct access to this global State.

Just like the `Vue instance’s data`, this State is `reactive`. When one component updates the `State`, other components that are using that data get `notified`, `automatically receiving the new value`.

But just consolidating data into a single source of truth doesn’t fully solve the problems of managing state. What happens when `many components` alter the State `in different ways`, from `different locations`? We need some standardization. Otherwise, changes to our State could be unpredictable and untraceable.

A `State Management Pattern` This is why `Vuex` provides a `full state management pattern` for a simple and standardized way to `make state changes`. And if you’re familiar with `Vue`, `Vuex` should look quite similar.

```js
const store = new Vuex.Store({
  state: {
    isLoading: false,
    todos: []
  },
  mutations: {
    SET_LOADING_STATUS(state) {
      state.isLoading = !state.isLoading
    },
    SET_TODOS(state, todos) {
      state.todos = todos
    }
  },
  actions: {
    fetchTodos(context) {
      context.commit('SET_LOADING_STATUS')

      axios.get('/api/todos').then(response => {
        context.commit('SET_LOADING_STATUS')
        context.commit('SET_TODOS', response.data.todos)
      })
    }
  },
  getters: {
    doneTodos(state) {
      return state.todos.filter(todo => todo.done)
    }
  }
});
```

the above `vuex` instance's properties compared to a `vue` one:
* While the `Vue` instance has a `data` property, the `Vuex` store has `state`. Both are `reactive`.

* while the `instance` has `methods`, which among other things can update `data`, the `store` has `Actions`, which can update the `state` (via `mutations`).

* while the `instance` has `computed properties` to access `data`, the `store` has `getters` to access `state`.

* `Vuex` provides a way to `track state changes`, with `Mutations`. We can use `Actions` to `commit` `Mutations`, and from the `Vue DevTools`, we can even `trace back in time` through a record of each mutation to the state.

In our `State`, we have an `isLoading` property, along an array for `todos`.

Below that we have a `Mutation` to switch our `isLoading` state between `true` and `false`. And a `Mutation` to set our `state` with the `todos` that we’ll receive from an `API call` in our `action` below.

Our `Action` here has multiple steps. First, it’ll `commit` the `Mutation` to set the `isLoading` status to `true`. Then it’ll make an API call, and when the response returns, it will `commit` the `Mutation` to set the `isLoading` status to `false`. Finally it’ll commit the `Mutation` to set the state of our `todos` with the response from our API.

**note**:
* `mutations` can be directly commited inside components' methods `this.$store.commit('INCREMENT_COUNT')`, but with `actions`, we can share common logic which commit `mutations` for us to multiple components.

* **Mutations Must Be Synchronous**, any `state mutation` performed in the callback of an asynchronous `mutation` is essentially `un-trackable`!. `Mutations` are designed and created (by Vuex) to update `states` `whenever executed`, think of them like `setters`. Thus, there's `no need` to know when an asynchronous operation ends inside `mutations`.

* `actions` is similar to `mutations`, just functions. However, letting users to directly update `states` produces the problem that `Vuex` is trying to solve, that is no proper `state-change tracking`, it would be hard to track where states are changed. Thus, `mutations` have its own benefits here. Moreover, separating the `mutations` and `actions` would be easier to handle `asynchronous operations`, since tracking when asynchronous operations return is a no easy task. In this case, `mutations` role would be to track when asynchronous operations end. In addition, `actions` also play the role of making state changes easier to track in operations happening in the application layer (not the Vuex store layer).

# State & Getters
## Accessing State
If we take a look at our `main.js` file, we see we’re importing our `Vuex` `store` file, and providing it to our `root Vue instance`. This will be set up for us if we selected `Vuex` when creating our project with the `Vue CLI`.

```js
import store from './store' 

new Vue({
  router,
  store, // <-- injecting the store for global access
  render: h => h(App)
}).$mount('#app')
```

This makes the `store` globally accessible throughout our app by `injecting` it into every component. This way, `any component` can access the `store` and the properties on it (such as `State`, `Actions`, `Mutations` and `Getters`) by using `$store`.

**note**: `Vue` instances themselves do not have the `store` property, the property is added by the `Vuex` lib itself. FOr more information on how to add custom properties to the `option` argument object of `Vue` instances, [check this](https://vuejs.org/v2/api/#vm-options). We can see the lib is accessing the `store` property [here](https://github.com/vuejs/vuex/blob/dev/src/mixin.js):

```js
  function vuexInit () {
    const options = this.$options // <---
    // store injection
    if (options.store) {
      this.$store = typeof options.store === 'function'
        ? options.store()
        : options.store
    } else if (options.parent && options.parent.$store) {
      this.$store = options.parent.$store
    }
  }
```

Back to our section content, if our `store` looks like this:

```js
// src/store.js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: { // <---
    user: { id: 'abc123', name: 'Adam Jahr' }
  },
  mutations: {},
  actions: {}
})
```

Then we can access the `user` state like this:

```html
// EventCreate.vue
<template>
  <h1>Create Event, {{ $store.state.user.name }}</h1>
</template>
```

what if we needed to use the user’s name in multiple places within our `component`? Sure, we could write `this.$store.state.user.name` all over the place… Or we could write it once, in a `computed` property, called `userName`.

```html
<template>
  <div>
      <h1>Create an Event, {{ userName }}</h1>
      <p>This event is created by {{ userName }}</p>
  </div>
</template>

<script>
export default {
  computed: {
    userName() { // <---
      return this.$store.state.user.name
    }
  }
}
</script>
```

And if we needed to use it in a method of our component, we could simply say `this.userName`.

## The `mapState` Helper
If we need to access different parts of our `State` (in our `store`) from the `same component`, it can get repetitive to have `multiple computed properties` each returning `this.$store.state.something`. To simplify things, we can use the `mapState` helper provides us a quick way to access our `state` without having to directly make a reference to the `$store` property. In addition, it returns an object of functions, returning different parts of our `state` as how we tell them to return.

**note**: technically, the functions returned by the `mapState` helper simply return its associated part of our `state` as what we tell them to. Thus, we can pretty much use them anywhere we want (`methods`, `computed`,...). However, they are often used as `computed properties` to keep our app a highly performer.

```js
// store.js
// here is our store
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    user: { id: 'abc123', name: 'Adam Jahr' },
    categories: [
      'sustainability',
      'nature',
      'animal welfare',
      'housing',
      'education',
      'food',
      'community'
    ]
  },
  mutations: {},
  actions: {}
})
```

Now, in `EventCreate.vue`, we can import `mapState`. Then use it to `map` our `State` to a `computed property` that can retrieve our user’s name, and our categories.

```html
<template>
  <div>
      <h1>Create an Event, {{ userName }}</h1>
      <p>This event is created by {{ userName }}</p>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  computed: mapState({
    userName: state => state.user.name,
    categories: state => state.categories
  })
}
</script>
```

Notice that we’re using a function, taking in `state` and returns the `property of the state` we want, `state.user.name` and `state.categories`. there’s an even `simpler way` to write this, like so:

```js
  computed: mapState({
    userName: state => state.user.name,
    categories: 'categories' // <-- simplified syntax for top-level State
  })
```

This is `equivalent` to `state => state.categories`.

We could simplify the `mapState` syntax `even more`, like so:

```js
  computed: mapState(['categories', 'user'])
```

now in our template we’d just need to use dot notation to access our user’s name.

```html
<h1>Create an Event, {{ user.name }}</h1>
```

**note**: to access `local state` with `this` inside the function, defined inside the `mapState` helper, a `normal function` **must** be used

```js
import { mapState } from 'vuex'

export default {
  computed: mapState({
    // to access local state with `this`, a normal function must be used
    countPlusLocalState (state) {
      return state.count + this.localCount
    }
  })
}
```

### Object Spread Operator
as `mapState` returns an `object of functions`, we can use `...` to merge the `object's functions` to other traditionally created ones.

```js
  computed: {
    traditionallyCreatedComputedProp() {
      return something
    },
    ...mapState(['categories', 'user']) // <-- using object spread operator
  }
```

## Getters
While we can access the Store’s `State` `directly`, sometimes we want to access `derived state`. 

```js
  computed: {
    catLength() {
      return this.$store.state.categories.length
    }
  }
```

But what if `multiple components` need to use this same value? By creating a `Vuex Getter`, we can avoid `unnecessary code duplication`. Also, since Getters are cached, this is a bit more performant of an option, too.

```js
// store.js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    user: { id: 'abc123', name: 'Adam Jahr' },
    categories: [
      'sustainability',
      'nature',
      'animal welfare',
      'housing',
      'education',
      'food',
      'community'
    ]
  },
  mutations: {},
  actions: {},
  getters: {}
})

```

As you can see, `Getters` `are` a function that takes in the `state` as an argument, and allows us to return `processed or filtered state`.

let’s use our `catLength` Getter. Just like accessing State, we’ll put it in a `computed property`.

### Passing getters to Getters 
we can pass in `getters` as the `second argument` to a `Getter`. This allows us to access another `Getter` from within the `Getter` we’re creating.

```js
// store.js
...
export default new Vuex.Store({
  state: {
    ...
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false },
      { id: 3, text: '...', done: true },
      { id: 4, text: '...', done: false }
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    },
    activeTodosCount: (state, getters) => { // <--- getters returns all the getters of this store
      return state.todos.length - getters.doneTodos.length
    }
  }
})
```

This example was just to demonstrate the power of passing in getters to a Getter, there are better way to write the `activeTodosCount` getter.

## Dynamic Getters
we can creat `dynamic getters` by returning a function and pass arguments to the function. For example, if we had an array of events, we could retrieve an event by `id` like so:

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    events: [
      { id: 1, title: '...', organizer: '...' },
      { id: 2, title: '...', organizer: '...' },
      { id: 3, title: '...', organizer: '...' },
      { id: 4, title: '...', organizer: '...' }
    ]
  },
  getters: {
    getEventById: state => id => { // <---
      return state.events.find(event => event.id === id)
    }
  }
})
```

```html
<template>
  <div>
      <h1>Create an Event, {{ user.name }}</h1>
      <p>This event is created by {{ user.id }}</p>

      <!-- use the computed property here -->
      <p>{{ getEvent(1) }}</p>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  computed: {
    getEvent() { // <--- a computed property returning the function "getEventById", returned by the "getEventById" getter
      return this.$store.getters.getEventById
    },
    ...mapState(['categories', 'user'])
  }
}
</script>
```

## The `mapGetters` Helper
Just like `accessing State` with `mapState`, we can map `Getters` to functions with the `mapgetters` helper, the types of arguments that the `mapGetter` helper receives are similar with the `mapState` one.

```html
<template>
  <div>
      <h1>Create an Event, {{ user.name }}</h1>
      <p>This event is created by {{ user.id }}</p>
      <p>{{ getEventById(1) }}</p>
  </div>
</template>

<script>
import { mapState, mapGetters } from 'vuex'

export default {
  computed: {
    ...mapGetters(['getEventById']),
    ...mapState(['categories', 'user'])
  }
}
</script>
```

# Mutations & Actions Pt. 1
we can use Mutations to `update`, or `mutate`, our `State`.

```js
// store.js

...
  state: {
    count: 0
  },
  mutations: {
    INCREMENT_COUNT(state) {
      state.count += 1
    }
  }
```

As you can see, our `INCREMENT_COUNT` mutation is taking in our Vuex `state` as an argument and using it to increment the `count`.

Now, Inside our `EventCreate` component, we’ll can commit the mutation:

```html
<template>
  <button @click="incrementCount">Increment</button>
</template>

<script>
  export default {
    methods: {
      incrementCount() {
        this.$store.commit('INCREMENT_COUNT');
      }
    }
  }
</script>
```

Checking the `Vue DevTools`, visit the `Vuex` tab, we can see our `count` is being updated. In addition, the `INCREMENT_COUNT` `mutation calls` are logged in the `DevTools` as well.

![](images/1.png)

If we click on `Base State`, we’re able to `see` the `State` of our app `prior to` the `INCREMENT_COUNT Mutation` being committed. **Note** that the app's `states` will not be reverted in `real time` as we select `previously commited mutations`.

![](images/2.png)
![](images/3.png)

**note**:  If you’re wondering why our `Mutation` is in all `capital letters`, that’s because it’s common within `Flux-based` patterns to put them in all caps. This is optional.

## Dynamic Mutations
We can pass a payload to a `Mutation` to make it `dynamic`.

```js
// store.js

...
  state: {
    count: 0
  },
  mutations: {
    INCREMENT_COUNT(state, value) { // the "mutation" can now access a passed in argument, presented by the "value" argument
      state.count += value
    }
  }
```

```js
export default {
  data() {
    return {
      incrementBy: 1
    }
  },
  methods: {
    incrementCount() {
      this.$store.commit('INCREMENT_COUNT', this.incrementBy) // <--- pass the "incrementBy" data to the "INCREMENT_COUNT" mutation's handler 
    }
  }
}
```

## Actions
While Vuex `Mutations` are `synchronous`, meaning they will happen one after the other, `Actions` can be `asynchronous`. We can use `Actions` to wrap some `business logic` around a `Mutation`, or `Mutations`.

for example, if we only wanted to update the `count` if our app has a `user`, we could write:

```js
// store.js

  actions: {
    updateCount({ state, commit }, incrementBy) {
      if (state.user) {
        commit('INCREMENT_COUNT', incrementBy)
      } 
  }
```

note that It is using `object destructuring` to get `state` and `commit` from the `Vuex` `context object`: `{ state, commit }`.

The `context` object is the `first argument` of any `Action`, and it exposes the `same set of properties` that are on the `store instance` (`state`, `mutations`, `actions`, `getters`). So you can call `context.commit` to commit a `mutation`, for example. Or say `context.state.count` to get the value of the `count` State.

Additionally, `updateCount` is taking in the `payload` value. The payload is `the second argument` of all `Actions`.

Now, within our `component`, we’d `dispatch` the `Action`.

```js
// component1.vue

...
  methods: {
    incrementCount() {
      this.$store.dispatch('updateCount', this.incrementBy)
    },
  }
```

## Adding to Our Example App

```shell
npm install vuejs-datepicker --save
```

