---
layout: post
title: "Implementing an undo history with Redux and lodash's debounce function"
description: " "
date: 2023-09-14
tags: [redux, undo]
comments: true
share: true
---

In many applications, having the ability to undo and redo actions is crucial for a good user experience. In this tutorial, we'll explore how to implement an undo history feature using Redux and Lodash's debounce function.

## Redux Setup

First, let's set up Redux in our project. Install the necessary packages by running the following command:

```
npm install redux
```

Next, create a file called `store.js` and add the following code:

```javascript
import { createStore } from 'redux';

const initialState = {
  undoHistory: [],
  present: null,
};

function reducer(state = initialState, action) {
  switch (action.type) {
    case 'ADD_ITEM':
      return {
        ...state,
        undoHistory: [...state.undoHistory, state.present],
        present: action.payload,
      };
    case 'UNDO':
      return {
        ...state,
        present: state.undoHistory[state.undoHistory.length - 1],
        undoHistory: state.undoHistory.slice(0, -1),
      };
    case 'RESET':
      return {
        ...state,
        undoHistory: [],
        present: null,
      };
    default:
      return state;
  }
}

const store = createStore(reducer);

export default store;
```

Here, we define our initial state with an `undoHistory` array that will store previous states, and a `present` variable that will hold the current state. We then define our reducer function that handles various actions, such as adding an item, undoing an action, and resetting the state.

## Using Lodash's Debounce Function

To ensure that the undo history is not filled with unnecessary states, we can use Lodash's debounce function to debounce the adding of items to the undo history array. Install Lodash by running the following command:

```
npm install lodash
```

Now, update the reducer code in `store.js` as follows:

```javascript
import { createStore } from 'redux';
import debounce from 'lodash/debounce';

const initialState = {
  undoHistory: [],
  present: null,
};

function reducer(state = initialState, action) {
  switch (action.type) {
    case 'ADD_ITEM':
      const debouncedAddToHistory = debounce(() => {
        state.undoHistory.push(state.present);
        state.undoHistory = state.undoHistory.slice(-5);
      }, 500);
      state.present = action.payload;
      debouncedAddToHistory();
      return { ...state };
    case 'UNDO':
      return {
        ...state,
        present: state.undoHistory[state.undoHistory.length - 1],
        undoHistory: state.undoHistory.slice(0, -1),
      };
    case 'RESET':
      return {
        ...state,
        undoHistory: [],
        present: null,
      };
    default:
      return state;
  }
}

const store = createStore(reducer);

export default store;
```

In the `ADD_ITEM` case, we create a debounced function `debouncedAddToHistory` that adds the present state to the undo history array and keeps only the last 5 states. This function is called every time we dispatch an `ADD_ITEM` action, but is debounced to only execute after 500 milliseconds of inactivity. This ensures that we only add important states to the undo history.

## Conclusion

By combining Redux for state management with Lodash's debounce function, we have successfully implemented an undo history feature in our application. Users will now be able to undo and redo actions, providing them with a smoother and more powerful user experience.

#redux #undo-history