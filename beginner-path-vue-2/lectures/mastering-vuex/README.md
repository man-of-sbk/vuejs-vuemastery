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
* **Mutations Must Be Synchronous**, any `state mutation` performed in the callback of an asynchronous `mutation` is essentially `un-trackable`!. `Mutations` are designed and created (by Vuex) to update `states` `whenever executed`, think of them like `setters`. Thus, there's `no need` to know when an asynchronous operation ends inside `mutations`.

* `actions` is similar to `mutations`, just functions. However, letting users to directly update `states` produces the problem that `Vuex` is trying to solve, that is no proper `state-change tracking`, it would be hard to track where states are changed. Thus, `mutations` have its own benefits here. Moreover, separating the `mutations` and `actions` would be easier to handle `asynchronous operations`, since tracking when asynchronous operations return is a no easy task. In this case, `mutations` role would be to track when asynchronous operations end. In addition, `actions` also play the role of making state changes easier to track in operations happening in the application layer (not the Vuex store layer).


