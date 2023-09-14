---
layout: post
title: "Transitioning from class components to functional components with Redux hooks"
description: " "
date: 2023-09-14
tags: [React, Redux]
comments: true
share: true
---

With the introduction of React Hooks, managing state in functional components has become much simpler and more readable. Redux, a popular state management library, has also embraced this shift by introducing Redux hooks.

If you've been using class components with Redux in your React application and want to transition to functional components with Redux hooks, this blog post will guide you through the process and provide practical examples.

## Why Use Functional Components with Redux Hooks?

- **Simplified Code**: Functional components are concise and easier to read, reducing boilerplate code often found in class components.
- **Better Scalability**: Redux hooks allow you to handle state management directly within functional components, making your codebase more modular and scalable.
- **Improved Performance**: Functional components with Redux hooks leverage the underlying React engine optimization, resulting in better performance.

## Step 1: Setting Up Redux with Hooks

First, ensure that you have the latest versions of `react`, `react-redux`, and `redux` installed in your project. 

```javascript
npm install react react-redux redux
```

Next, you'll need to create your Redux store and wrap your application in the `Provider` component from `react-redux`. 

In your root file (usually `index.js` or `App.js`), make the following changes:

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import { createStore } from 'redux';
import rootReducer from './reducers'; // Assuming you have a root reducer

const store = createStore(rootReducer);

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

## Step 2: Converting Class Components to Functional Components

To start transitioning from class components to functional components, identify the specific component you want to convert.

Let's say you have a `Counter` component that increments and decrements a value:

```javascript
import React, { Component } from 'react';
import { connect } from 'react-redux';
import { increment, decrement } from '../actions';

class Counter extends Component {
  render() {
    const { count, increment, decrement } = this.props;

    return (
      <div>
        <button onClick={decrement}>-</button> 
        <span>{count}</span>
        <button onClick={increment}>+</button>
      </div>
    );
  }
}

const mapStateToProps = state => {
  return {
    count: state.count
  };
};

const mapDispatchToProps = {
  increment,
  decrement
};

export default connect(mapStateToProps, mapDispatchToProps)(Counter);
```

To convert this class component to a functional component with Redux hooks, follow these steps:

1. Import the necessary hooks from `react-redux`:

   ```javascript
   import { useSelector, useDispatch } from 'react-redux';
   ```

2. Replace the class component with a functional component:

   ```javascript
   const Counter = () => {
     const count = useSelector(state => state.count);
     const dispatch = useDispatch();

     const increment = () => dispatch(increment());
     const decrement = () => dispatch(decrement());

     return (
       <div>
         <button onClick={decrement}>-</button> 
         <span>{count}</span>
         <button onClick={increment}>+</button>
       </div>
     );
   };
   ```

That's it! You've successfully converted a class component to a functional component using Redux hooks.

## Step 3: Refactoring Redux Related Code

Now that your component is functional, you can remove the code related to Redux setup and configuration from your component files. 

For example, the `mapStateToProps` and `mapDispatchToProps` functions can be removed, along with the `connect` function at the bottom of the file.

Your refactored functional component file would look like this:

```javascript
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { increment, decrement } from '../actions';

const Counter = () => {
  const count = useSelector(state => state.count);
  const dispatch = useDispatch();

  const increment = () => dispatch(increment());
  const decrement = () => dispatch(decrement());

  return (
    <div>
      <button onClick={decrement}>-</button> 
      <span>{count}</span>
      <button onClick={increment}>+</button>
    </div>
  );
};

export default Counter;
```

## Conclusion

Transitioning from class components to functional components with Redux hooks can significantly improve the readability and scalability of your React application. By following the steps outlined in this blog post, you'll be well on your way to enjoying the benefits of cleaner code and improved performance.

#React #Redux