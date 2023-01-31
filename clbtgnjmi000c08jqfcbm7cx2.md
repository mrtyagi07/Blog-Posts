# Redux for beginners: A step-by-step guide to state management in React

## What is Redux?

Redux is a JavaScript library for managing application state. It is often used with libraries like React or Angular for building user interfaces.

In a Redux application, the entire state of the app is stored in a single, immutable **"store"** object. The store can only be modified by dispatching actions, which are plain JavaScript objects that describe a change to the store. To specify how **actions** should modify the store, you write **"reducers"** - functions that take the current state of the store and action as arguments, and **return a new state**.

![MVC vs Flux vs Redux – The Real Differences](https://www.clariontech.com/hs-fs/hubfs/Image3-43.png?width=417&name=Image3-43.png align="left")

*<mark>I understand that redux is difficult to understand, so let's take a closer look at the real-world application of redux</mark>*

Imagine that you have a toy box with all your favorite toys in it. The toy box is like the "store" in Redux. You can only add or take away toys from the toy box by using special "actions," which are like instructions for what to do with the toys. For example, you might have an **"add toy"** action that tells you to put a new toy in the toy box or a **"remove toy"** action that tells you to take a toy out of the toy box.

To make sure that the toy box stays organized, you have a set of rules called **"reducers"** that tell you how to handle the actions. For example, you might have a rule that says "if you see an 'add toy' action, add the toy to the toy box," or "if you see a 'remove toy' action, take the toy out of the toy box."

Redux helps you keep track of your toys and makes sure that you always follow the rules for adding or taking away toys. This way, you can be sure that your toy box is always organized and that you know exactly what toys you have.

Of course, this is a very simplified explanation of Redux, and it doesn't cover all the details of how it works. However, it should give you a basic idea of what Redux is and why it might be useful.

## Why should you use Redux?

*   **Centralized state management:** One of the main benefits of Redux is that it provides a centralized place to store the state of your entire application. This can be particularly useful in larger applications, where different parts of the app may need to share state or data. With Redux, you can avoid the need to pass props down through multiple levels of components or to use props to communicate between unrelated components.
    
*   **Predictable state changes:** In Redux, state changes are triggered by dispatching actions, which are plain JavaScript objects that describe a change to the store. This makes it easy to understand how the state of your application is being modified and to debug any issues that may arise.
    
*   **Easy to test:** Because Redux is based on a set of simple functions (the store, actions, and reducers), it is easy to test your application logic in isolation. You can write unit tests for your reducers and actions to ensure that they are working as expected, and use integration tests to ensure that the different parts of your app are working together correctly.
    
*   **Developer tools:** The Redux ecosystem includes a number of developer tools that can make it easier to build, debug, and optimize your application. For example, the redux-devtools-extension browser extension provides a powerful set of tools for inspecting the state of your Redux store, dispatching actions, and rolling back changes.
    
    Overall, Redux can be a useful tool for managing the state of a React application, particularly in larger or more complex apps. However, it is not the only option, and whether or not to use Redux is a design decision that depends on the specific needs of your application.
    

## How to use Redux?

First, you'll need to install the Redux library and the react-redux library, which provides bindings for React:

```javascript
npm install @reduxjs/toolkit
```

Then, you'll need to define your actions, which are how your application's state can be modified. In this case, you'll need two actions: one to increment the counter, and one to decrement the counter.

```javascript
const INCREMENT = 'INCREMENT';

const DECREMENT = 'DECREMENT';

function increment() {
  return { type: INCREMENT };
}

function decrement() {
  return { type: DECREMENT };
}
```

Next, you'll need to define your reducer, which is a function that takes in the current state of your application and an action and returns the new state. In this case, the reducer will simply check the type of the action, and increment or decrement the counter accordingly.

```javascript
function reducer(state = 0, action) {

  switch (action.type) {
    case INCREMENT:
      return state + 1;
    case DECREMENT:
      return state - 1;
    default:
      return state;
  }
}
```

Finally, you can create your Redux store and dispatch your actions to update the state of your application.

```javascript
import { createStore } from 'redux';

const store = createStore(reducer);

store.dispatch(increment());
// The state of the store is now 1

store.dispatch(increment());
// The state of the store is now 2

store.dispatch(decrement());
// The state of the store is now 1
```

The dispatch function is used to send the increment and decrement actions to the store's reducer. You can then use the current state of the store to render your application.

```javascript
function render() {
  document.body.innerHTML = store.getState();
}

store.subscribe(render);
render();
```

This is just a basic example of how you can use Redux to manage the state of your application. There are many more advanced features and techniques that you can use to build more complex applications.

### Here's a more complex example of using Redux to manage the state of a simple to-do list application:

First, you'll define your actions. In this case, you'll need several actions: one to add a to-do, one to toggle the completion status of a to-do, and one to delete a to-do.

```javascript
const ADD_TODO = 'ADD_TODO';

const TOGGLE_TODO = 'TOGGLE_TODO';
const DELETE_TODO = 'DELETE_TODO';

function addTodo(text) {
  return { type: ADD_TODO, text };
}

function toggleTodo(index) {
  return { type: TOGGLE_TODO, index };
}

function deleteTodo(index) {
  return { type: DELETE_TODO, index };
}
```

Then, you'll define your reducer function, which will handle the different actions and update the state of the application accordingly.

```javascript
function reducer(state = [], action) {

  switch (action.type) {
    case ADD_TODO:
      return [
        ...state,
        {
          text: action.text,
          completed: false,
        },
      ];
    case TOGGLE_TODO:
      return state.map((todo, index) => {
        if (index === action.index) {
          return {
            ...todo,
            completed: !todo.completed,
          };
        }
        return todo;
      });
    case DELETE_TODO:
      return state.filter((todo, index) => index !== action.index);
    default:
      return state;
  }
}
```

Then, you can create your Redux store and dispatch your actions to update the state of your application.

```javascript
import { createStore } from 'redux';

const store = createStore(reducer);

store.dispatch(addTodo('Take out the trash'));
store.dispatch(addTodo('Do the dishes'));
store.dispatch(toggleTodo(0));
store.dispatch(deleteTodo(1));
```

You can then use the current state of the store to render your application.

```javascript
function render() {

  const todos = store.getState();

  const list = document.createElement('ul');

  todos.forEach(todo => {
    const item = document.createElement('li');
    item.textContent = todo.text;
    if (todo.completed) {
      item.classList.add('completed');
    }
    list.appendChild(item);
  });

  document.body.innerHTML = '';
  document.body.appendChild(list);
}

store.subscribe(render);
render();
```

*If you're interested in learning more about Redux and how it can be used to manage the state of your JavaScript applications, be sure to check out the official documentation. It provides a comprehensive guide to all of the features and techniques that are available in Redux and is a great resource for developers who are looking to get started with the library. Additionally, many online resources and tutorials can help you learn more about Redux and how to use it effectively. So if you're interested in incorporating Redux into your workflow, don't hesitate to dive in and start learning! So, this is it for redux in brief.*

> I hope you enjoyed reading this blog post. If you would like to stay updated on my progress and engage in discussions with me on a variety of topics, you can follow me on Twitter. I regularly post updates on my work and thoughts on various topics, and I am always open to chatting with others on the platform.