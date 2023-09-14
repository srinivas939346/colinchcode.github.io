---
layout: post
title: "Implementing a task management app with Redux and Firebase Firestore"
description: " "
date: 2023-09-14
tags: [redux, firebase]
comments: true
share: true
---

In this tutorial, we will explore how to build a task management app using Redux for state management and Firebase Firestore as the backend database. By the end of this tutorial, you will have a functional task management app where users can create, read, update, and delete tasks in real-time.

### Prerequisites

Before we begin, make sure you have the following installed:

- Node.js and npm
- React
- Redux
- Firebase Firestore (set up your Firebase account and project)

### Setting up the Redux Store

First, let's set up the Redux store to manage the state of our application. Create a new file `store.js` and add the following code:

```javascript
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import rootReducer from './reducers';

const initialState = {};

const middleware = [thunk];

const store = createStore(
  rootReducer,
  initialState,
  applyMiddleware(...middleware)
);

export default store;
```

In this code, we import the necessary Redux functions and middleware. We create the Redux store using the `createStore` function, passing in our root reducer (which we'll create next), initial state, and middleware.

### Creating the Reducers

Next, let's create the reducers that will handle the different actions for our app. Create a new folder `reducers` and inside it, create a file `taskReducer.js`. Add the following code:

```javascript
import { CREATE_TASK, READ_TASK, UPDATE_TASK, DELETE_TASK } from '../actions/types';

const initialState = {
  tasks: []
};

const taskReducer = (state = initialState, action) => {
  switch (action.type) {
    case CREATE_TASK:
      return {
        ...state,
        tasks: [...state.tasks, action.payload]
      };
    case READ_TASK:
      return {
        ...state,
        tasks: action.payload
      };
    case UPDATE_TASK:
      return {
        ...state,
        tasks: state.tasks.map((task) => {
          if (task.id === action.payload.id) {
            return action.payload.updatedTask;
          } else {
            return task;
          }
        })
      };
    case DELETE_TASK:
      return {
        ...state,
        tasks: state.tasks.filter((task) => task.id !== action.payload)
      };
    default:
      return state;
  }
};

export default taskReducer;
```

In this code, we define the initial state with an empty array of tasks. We create a task reducer function that handles different action types such as creating a task, reading tasks, updating a task, and deleting a task.

### Creating the Actions

Now, let's create the actions that will trigger the reducer functions. Create a new folder `actions` and inside it, create a file `taskActions.js`. Add the following code:

```javascript
import { CREATE_TASK, READ_TASK, UPDATE_TASK, DELETE_TASK } from './types';
import { firestore } from '../firebase';

export const createTask = (taskData) => async (dispatch) => {
  try {
    const docRef = await firestore.collection('tasks').add(taskData);
    const task = { id: docRef.id, ...taskData };
    dispatch({
      type: CREATE_TASK,
      payload: task
    });
  } catch (error) {
    console.error(error);
  }
};

export const readTasks = () => async (dispatch) => {
  try {
    const snapshot = await firestore.collection('tasks').get();
    const tasks = snapshot.docs.map((doc) => {
      return {
        id: doc.id,
        ...doc.data()
      };
    });
    dispatch({
      type: READ_TASK,
      payload: tasks
    });
  } catch (error) {
    console.error(error);
  }
};

export const updateTask = (taskId, updatedTask) => async (dispatch) => {
  try {
    const taskRef = firestore.collection('tasks').doc(taskId);
    await taskRef.update(updatedTask);
    dispatch({
      type: UPDATE_TASK,
      payload: { id: taskId, updatedTask }
    });
  } catch (error) {
    console.error(error);
  }
};

export const deleteTask = (taskId) => async (dispatch) => {
  try {
    const taskRef = firestore.collection('tasks').doc(taskId);
    await taskRef.delete();
    dispatch({
      type: DELETE_TASK,
      payload: taskId
    });
  } catch (error) {
    console.error(error);
  }
};
```

In this code, we define different action creator functions for creating, reading, updating, and deleting tasks. We use the Firebase Firestore API to interact with the backend database.

### Connecting Redux with React Components

Now that we have defined the Redux store, reducers, and actions, let's connect everything with our React components. Here's an example of how to connect a component called `TaskList`:

```javascript
import React, { useEffect } from 'react';
import { connect } from 'react-redux';
import { readTasks } from '../actions/taskActions';

const TaskList = ({ tasks, readTasks }) => {
  useEffect(() => {
    readTasks();
  }, [readTasks]);

  return (
    <div>
      {tasks.map((task) => (
        <div key={task.id}>
          <h3>{task.title}</h3>
          <p>{task.description}</p>
        </div>
      ))}
    </div>
  );
};

const mapStateToProps = (state) => ({
  tasks: state.tasks
});

export default connect(mapStateToProps, { readTasks })(TaskList);
```

In this code, we import the necessary functions from React and Redux. We define a functional component `TaskList` that uses the `useEffect` hook to call the `readTasks` action on component mount. We map over the tasks in the Redux state and display them in the component.

To connect the component to the Redux store, we use the `connect` function from `react-redux`. We define a `mapStateToProps` function to map the tasks from the Redux state to component props. We also use the `connect` function to connect the `readTasks` action to the component.

### Conclusion

In this tutorial, we have learned how to build a task management app using Redux for state management and Firebase Firestore as the backend database. We have set up the Redux store, created reducers and actions, and connected our React components to Redux. You can further enhance this app by adding more features like user authentication and task filtering.

#redux #firebase