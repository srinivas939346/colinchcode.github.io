---
layout: post
title: "Building a CRUD (Create, Read, Update, Delete) application with Redux"
description: " "
date: 2023-09-14
tags: [redux, CRUD]
comments: true
share: true
---

In this tutorial, we will walk through the process of building a CRUD application using Redux, a popular state management library in JavaScript. By following this guide, you will learn how to implement the basic CRUD operations in Redux and create a fully functional application.

### Prerequisites

Before we start, make sure you have the following prerequisites installed:

- Node.js and npm (Node Package Manager) 
- Redux and React libraries 
- Basic knowledge of JavaScript

### Step 1: Setting up the Project

Start by creating a new React project using the create-react-app command:

```bash
npx create-react-app redux-crud-app
``` 

Next, navigate to the project directory:

```bash
cd redux-crud-app
```

Install Redux and its dependencies using the npm command:

```bash
npm install redux react-redux
```

### Step 2: Creating Redux Store

The store is the central component of Redux that holds the state of the application. Create a new folder called `redux` in the `src` directory.

Inside the `redux` folder, create a file called `store.js` and add the following code:

```javascript
import { createStore } from 'redux';
import rootReducer from './reducers';

const store = createStore(rootReducer);
export default store;
```

### Step 3: Creating Reducers

Reducers are pure functions that define how the application's state should change based on the dispatched actions. Inside the `redux` folder, create another folder called `reducers`.

Inside the `reducers` folder, create a file called `items.js` and add the following code:

```javascript
const initialState = {
  items: []
};

const itemsReducer = (state = initialState, action) => {
  switch (action.type) {
    case 'ADD_ITEM':
      return {
        items: [...state.items, action.payload]
      };
    case 'DELETE_ITEM':
      return {
        items: state.items.filter(item => item.id !== action.payload)
      };
    default:
      return state;
  }
};

export default itemsReducer;
```

### Step 4: Setting up Actions

Actions are objects that describe what should be carried out in the application. Inside the `redux` folder, create another folder called `actions`.

Inside the `actions` folder, create a file called `itemActions.js` and add the following code:

```javascript
let itemId = 0;

export const addItem = item => ({
  type: 'ADD_ITEM',
  payload: {
    id: itemId++,
    name: item.name,
    description: item.description
  }
});

export const deleteItem = itemId => ({
  type: 'DELETE_ITEM',
  payload: itemId
});
```

### Step 5: Creating Components

Inside the `src` directory, create a folder called `components`. Inside the `components` folder, create a file called `ItemList.js` and add the following code:

```javascript
import React from 'react';
import { connect } from 'react-redux';
import { deleteItem } from '../redux/actions/itemActions';

const ItemList = props => {
  const handleDelete = itemId => {
    props.deleteItem(itemId);
  };

  return (
    <div>
      <h2>Item List</h2>
      <ul>
        {props.items.map(item => (
          <li key={item.id}>
            <span>{item.name}</span>
            <span>{item.description}</span>
            <button onClick={() => handleDelete(item.id)}>Delete</button>
          </li>
        ))}
      </ul>
    </div>
  );
};

const mapStateToProps = state => ({
  items: state.items
});

export default connect(mapStateToProps, { deleteItem })(ItemList);
```

Inside the `src/components` folder, create another file called `AddItemForm.js` and add the following code:

```javascript
import React, { useState } from 'react';
import { connect } from 'react-redux';
import { addItem } from '../redux/actions/itemActions';

const AddItemForm = props => {
  const [name, setName] = useState('');
  const [description, setDescription] = useState('');

  const handleSubmit = e => {
    e.preventDefault();

    if (name && description) {
      props.addItem({ name, description });
      setName('');
      setDescription('');
    }
  };

  return (
    <div>
      <h2>Add Item</h2>
      <form onSubmit={handleSubmit}>
        <input
          type="text"
          placeholder="Name"
          value={name}
          onChange={e => setName(e.target.value)}
        />
        <input
          type="text"
          placeholder="Description"
          value={description}
          onChange={e => setDescription(e.target.value)}
        />
        <button type="submit">Add</button>
      </form>
    </div>
  );
};

export default connect(null, { addItem })(AddItemForm);
```

### Step 6: Combining Reducers

Inside the `reducers` folder, create a file called `index.js` and add the following code:

```javascript
import { combineReducers } from 'redux';
import itemsReducer from './items';

const rootReducer = combineReducers({
  items: itemsReducer
});

export default rootReducer;
```

### Step 7: Integrating Redux Store

Open the `src/index.js` file and make the following changes:

Add the necessary imports:

```javascript
import { Provider } from 'react-redux';
import store from './redux/store';
```

Wrap the App component with the Provider component and pass the store as a prop:

```javascript
ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

### Step 8: Using the Components

Open the `src/App.js` file and make the following changes:

Add the necessary imports:

```javascript
import ItemList from './components/ItemList';
import AddItemForm from './components/AddItemForm';
```

Modify the App component to include the ItemList and AddItemForm components:

```javascript
function App() {
  return (
    <div>
      <h1>CRUD Application with Redux</h1>
      <AddItemForm />
      <ItemList />
    </div>
  );
}

export default App;
```

### Step 9: Test the Application

Finally, start the development server and test the application in the browser:

```bash
npm start
```

You should now see the CRUD application with the ability to add and delete items.

Congratulations! You have successfully built a CRUD application with Redux. You can further enhance the application by adding update functionality and improving the UI.

#redux #CRUD