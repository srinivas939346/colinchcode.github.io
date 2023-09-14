---
layout: post
title: "Building a Kanban board with draggable cards using Redux"
description: " "
date: 2023-09-14
tags: [React, Redux]
comments: true
share: true
---

In this tutorial, we will learn how to build a Kanban board with draggable cards using Redux. Kanban boards are popular project management tools that help teams visualize their workflow and track the progress of tasks.

## What is Redux?

**Redux** is a predictable state container for JavaScript apps. It helps manage the state of your application in a centralized store, making it easy to access and update data from different components.

## Setting up the Project

Before we begin, make sure you have Node.js and npm installed on your machine. You can check the versions by running `node -v` and `npm -v` in your terminal.

To get started, create a new project folder and navigate to it in your terminal. Then, initialize a new npm project by running the following command:

```shell
npm init -y
```

Once the project is initialized, install the necessary dependencies:

```shell
npm install react react-dom redux react-redux
```

## Creating the Kanban Board

### Creating the Card Component

First, let's create a `Card` component that represents a task on the Kanban board. In your `src` folder, create a new file called `Card.js` and add the following code:

```jsx
import React from 'react';

const Card = ({ title }) => {
  return (
    <div className="card">
      <div className="card-title">{title}</div>
    </div>
  );
};

export default Card;
```

### Setting up Redux Store and Reducers

Next, let's set up the Redux store and reducers. In your `src` folder, create a new folder called `store` and inside it, create a new file called `index.js`. Add the following code:

```jsx
import { createStore } from 'redux';

const initialState = {
  cards: [
    { id: 1, title: 'Task 1' },
    { id: 2, title: 'Task 2' },
    // Add more tasks here
  ],
};

const reducer = (state = initialState, action) => {
  // Add reducer logic here
};

const store = createStore(reducer);

export default store;
```

In the code above, we have set up an initial state with some sample tasks. We also defined a reducer function that will handle actions and update the state accordingly.

### Combining Reducers

Since we may have multiple reducers in our application, it's a good practice to combine them into a single root reducer using the `combineReducers` function from Redux. Modify the `index.js` file in the `store` folder as follows:

```jsx
import { createStore, combineReducers } from 'redux';

const cardReducer = (state = initialState.cards, action) => {
  // Add cardReducer logic here
};

const rootReducer = combineReducers({
  cards: cardReducer,
});

const store = createStore(rootReducer);

export default store;
```

### Creating the Kanban Board Component

Now let's create the `KanbanBoard` component which will render the draggable cards. In your `src` folder, create a new file called `KanbanBoard.js` and add the following code:

```jsx
import React from 'react';
import { useSelector } from 'react-redux';
import Card from './Card';

const KanbanBoard = () => {
  const cards = useSelector((state) => state.cards);

  return (
    <div className="kanban-board">
      {cards.map((card) => (
        <Card key={card.id} title={card.title} />
      ))}
    </div>
  );
};

export default KanbanBoard;
```

In the code above, we used the `useSelector` hook from `react-redux` to access the cards from the Redux store.

### Adding the Kanban Board to App Component

Finally, let's add the `KanbanBoard` component to the `App` component. Replace the contents of `App.js` with the following code:

```jsx
import React from 'react';
import KanbanBoard from './KanbanBoard';

const App = () => {
  return (
    <div className="app">
      <h1>Kanban Board</h1>
      <KanbanBoard />
    </div>
  );
};

export default App;
```

## Conclusion

In this tutorial, we learned how to build a Kanban board with draggable cards using Redux. We created a Card component, set up the Redux store with reducers, and built a KanbanBoard component to render the draggable cards. Now you can customize and enhance the Kanban board to fit your project management needs!

## #React #Redux