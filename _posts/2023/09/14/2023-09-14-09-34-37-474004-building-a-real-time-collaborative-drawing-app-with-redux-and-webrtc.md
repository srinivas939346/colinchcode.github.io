---
layout: post
title: "Building a real-time collaborative drawing app with Redux and WebRTC"
description: " "
date: 2023-09-14
tags: [webdevelopment, redux, webrtc]
comments: true
share: true
---

In this tutorial, we will learn how to build a real-time collaborative drawing app using Redux and WebRTC. This app will allow multiple users to draw and see each other's drawings in real-time using WebRTC's data channel. We will be using Redux to manage the state of the drawings and WebRTC to establish a peer-to-peer connection between the users.

## Prerequisites

Before we start, make sure you have the following:

- Basic knowledge of React and Redux
- Node.js and npm installed on your machine
- An understanding of WebRTC concepts

## Setting up the project

To get started, let's set up a new React project with Redux. Open your terminal and run the following commands:

```bash
npx create-react-app drawing-app
cd drawing-app
npm install redux react-redux
```

## Creating the drawing canvas

First, let's create a simple drawing canvas component where users can draw. Create a new file `Canvas.js` and add the following code:

```javascript
import React, { useRef, useEffect } from 'react';

const Canvas = () => {
  const canvasRef = useRef(null);
  const contextRef = useRef(null);

  useEffect(() => {
    const canvas = canvasRef.current;
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    const context = canvas.getContext('2d');
    context.lineCap = 'round';
    context.strokeStyle = '#000';
    context.lineWidth = 2;
    contextRef.current = context;
  }, []);

  const startDrawing = ({ nativeEvent }) => {
    const { offsetX, offsetY } = nativeEvent;
    contextRef.current.beginPath();
    contextRef.current.moveTo(offsetX, offsetY);
  };

  const draw = ({ nativeEvent }) => {
    const { offsetX, offsetY } = nativeEvent;
    contextRef.current.lineTo(offsetX, offsetY);
    contextRef.current.stroke();
  };

  return (
    <canvas
      ref={canvasRef}
      onMouseDown={startDrawing}
      onMouseMove={draw}
      onMouseUp={() => contextRef.current.closePath()}
    ></canvas>
  );
};

export default Canvas;
```

In this code, we create a canvas element using the `canvasRef` and set the width and height of the canvas to match the window size. We also set up the context and define some drawing styles. When the user starts drawing, we begin a new path and move the cursor to the starting position. As the user moves the cursor, we draw lines and update the canvas.

## Setting up Redux

Next, let's set up Redux to manage the state of the drawings. Create a new file `drawingReducer.js` and add the following code:

```javascript
const initialState = {
  drawings: [],
};

const drawingReducer = (state = initialState, action) => {
  switch (action.type) {
    case 'ADD_DRAWING':
      return {
        ...state,
        drawings: [...state.drawings, action.payload],
      };
    case 'CLEAR_DRAWINGS':
      return {
        ...state,
        drawings: [],
      };
    default:
      return state;
  }
};

export default drawingReducer;
```

In this code, we define an initial state with an empty array for drawings. We then create a reducer function that handles two actions: `ADD_DRAWING` and `CLEAR_DRAWINGS`. The `ADD_DRAWING` action adds a new drawing to the state, and the `CLEAR_DRAWINGS` action clears all drawings.

## Connecting Redux to the app

Now let's connect Redux to our app. Edit the `src/index.js` file and update it as follows:

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import { createStore } from 'redux';
import './index.css';
import App from './App';
import drawingReducer from './drawingReducer';

const store = createStore(drawingReducer);

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

Here, we import the necessary Redux components and create a Redux store using our `drawingReducer`. We then wrap the `App` component with the `Provider` component and pass the store as a prop.

## Using Redux in the Canvas component

Now that we have set up Redux, let's use it in our `Canvas` component. Update the `Canvas.js` file as follows:

```javascript
import React, { useRef, useEffect, useState } from 'react';
import { useSelector, useDispatch } from 'react-redux';

const Canvas = () => {
  const canvasRef = useRef(null);
  const contextRef = useRef(null);
  const drawings = useSelector(state => state.drawings);
  const dispatch = useDispatch();
  const [currentDrawing, setCurrentDrawing] = useState([]);

  useEffect(() => {
    const canvas = canvasRef.current;
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    const context = canvas.getContext('2d');
    context.lineCap = 'round';
    context.strokeStyle = '#000';
    context.lineWidth = 2;
    contextRef.current = context;
  }, []);

  const startDrawing = ({ nativeEvent }) => {
    const { offsetX, offsetY } = nativeEvent;
    contextRef.current.beginPath();
    contextRef.current.moveTo(offsetX, offsetY);
    setCurrentDrawing([{ x: offsetX, y: offsetY }]);
  };

  const draw = ({ nativeEvent }) => {
    if (!canvasRef.current || !currentDrawing.length) return;
    const { offsetX, offsetY } = nativeEvent;
    contextRef.current.lineTo(offsetX, offsetY);
    contextRef.current.stroke();
    setCurrentDrawing(prevDrawing => [...prevDrawing, { x: offsetX, y: offsetY }]);
  };

  const endDrawing = () => {
    dispatch({ type: 'ADD_DRAWING', payload: currentDrawing });
    setCurrentDrawing([]);
  };

  const clearDrawings = () => {
    dispatch({ type: 'CLEAR_DRAWINGS' });
  };

  useEffect(() => {
    drawings.forEach(drawing => {
      const { x, y } = drawing[0];
      contextRef.current.beginPath();
      contextRef.current.moveTo(x, y);
      drawing.forEach(({ x, y }) => {
        contextRef.current.lineTo(x, y);
        contextRef.current.stroke();
      });
      contextRef.current.closePath();
    });
  }, [drawings]);

  return (
    <div className="canvas-container">
      <canvas
        ref={canvasRef}
        onMouseDown={startDrawing}
        onMouseMove={draw}
        onMouseUp={endDrawing}
      ></canvas>
      <button className="clear-button" onClick={clearDrawings}>
        Clear Drawings
      </button>
    </div>
  );
};

export default Canvas;
```

In this updated code, we use the `useSelector` hook to retrieve the `drawings` array from the Redux state. We also use the `useDispatch` hook to dispatch actions. When the user starts drawing, we store the current drawing coordinates in the `currentDrawing` state. In the `draw` function, we draw the lines as the user moves the cursor and update the `currentDrawing` state. When the user finishes drawing, we dispatch the `ADD_DRAWING` action with the current drawing and clear the `currentDrawing` state. We also added a button to clear all drawings using the `CLEAR_DRAWINGS` action.

## Conclusion

Congratulations! You have successfully built a real-time collaborative drawing app using Redux and WebRTC. Users can now draw on a shared canvas and see each other's drawings in real-time. Feel free to enhance the app by adding features like colors, brush size, and undo functionality.

#webdevelopment #redux #webrtc