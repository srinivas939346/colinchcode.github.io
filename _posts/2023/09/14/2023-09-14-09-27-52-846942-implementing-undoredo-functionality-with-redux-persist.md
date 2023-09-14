---
layout: post
title: "Implementing undo/redo functionality with Redux-persist"
description: " "
date: 2023-09-14
tags: [redux, undo]
comments: true
share: true
---

The ability to undo and redo actions is a critical feature in many applications. It allows users to revert changes and navigate through the history of their interactions. In this blog post, we will explore how to implement undo/redo functionality with Redux-persist, a popular library for persisting Redux state.

## What is Redux-persist?

Redux-persist is a middleware library for Redux that helps with storing and retrieving the Redux store state to persistent storage. It supports various storage engines such as LocalStorage, AsyncStorage, and more. With Redux-persist, the state can be saved when the user closes the application and restored when they reopen it.

## Steps to Implement Undo/Redo Functionality

To implement undo/redo functionality with Redux-persist, follow these steps:

1. First, install the necessary dependencies by running the following command in your project directory:

```bash
npm install redux redux-persist redux-undo
```

2. Set up Redux in your application by creating a store and configuring Redux-persist. Here's an example of how you can configure Redux-persist in a simple Redux store setup:

```javascript
import { createStore, applyMiddleware } from 'redux';
import { persistStore, persistReducer } from 'redux-persist';
import storage from 'redux-persist/lib/storage';
import undoable from 'redux-undo';

import rootReducer from './reducers';

const persistConfig = {
  key: 'root',
  storage,
};

const persistedReducer = persistReducer(persistConfig, undoable(rootReducer));

export const store = createStore(persistedReducer);
export const persistor = persistStore(store);
```

In this example, we use the `storage` module from Redux-persist to configure the persistence storage engine. We also use the `undoable` function from `redux-undo` to enable the undo/redo functionality for our Redux state.

3. Implement the undo/redo actions in your reducers. With `redux-undo`, you can wrap your root reducer with the `undoable` function to automatically enable undo/redo actions for all reducers. Here's an example:

```javascript
import { combineReducers } from 'redux';
import undoable, { excludeAction } from 'redux-undo';

const initialState = {
  count: 0,
};

const counterReducer = (state = initialState, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return { count: state.count + 1 };
    case 'DECREMENT':
      return { count: state.count - 1 };
    default:
      return state;
  }
};

const rootReducer = combineReducers({
  counter: undoable(counterReducer, {
    limit: 10, // Maximum number of history items to keep
    filter: excludeAction(['REDO', 'UNDO']), // Exclude the undo/redo actions from history
  }),
});

export default rootReducer;
```

Make sure to wrap your actual reducer with `undoable` and pass any desired options (in this case, we set a limit on the number of history items to keep and exclude undo/redo actions from the history).

4. Update your application components to dispatch undo and redo actions. You can use the `ActionCreators` provided by `redux-undo` to dispatch the `UNDO` and `REDO` actions. Here's an example:

```javascript
import React from 'react';
import { connect } from 'react-redux';
import { ActionCreators } from 'redux-undo';

const App = ({ count, undo, redo, increment, decrement }) => {
  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
      <button onClick={undo}>Undo</button>
      <button onClick={redo}>Redo</button>
    </div>
  );
};

const mapStateToProps = (state) => ({
  count: state.counter.present.count,
});

const mapDispatchToProps = {
  undo: ActionCreators.undo,
  redo: ActionCreators.redo,
  increment: () => ({ type: 'INCREMENT' }),
  decrement: () => ({ type: 'DECREMENT' }),
};

export default connect(mapStateToProps, mapDispatchToProps)(App);
```

In this example, we connect the App component to the Redux store and provide the `undo` and `redo` actions from `redux-undo`. We also dispatch the `INCREMENT` and `DECREMENT` actions when the buttons are clicked.

## Wrapping Up

By following the steps outlined above, you can easily implement undo/redo functionality in your Redux application using Redux-persist and the `redux-undo` library. This gives users the ability to undo and redo actions, ensuring a smooth and intuitive user experience.

Remember to import the necessary dependencies, configure Redux-persist, update your reducers, and dispatch the undo and redo actions in your application components.

#redux #undo