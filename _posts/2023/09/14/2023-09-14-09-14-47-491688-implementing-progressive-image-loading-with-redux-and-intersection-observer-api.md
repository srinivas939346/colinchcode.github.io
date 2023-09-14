---
layout: post
title: "Implementing progressive image loading with Redux and Intersection Observer API"
description: " "
date: 2023-09-14
tags: [redux, intersection]
comments: true
share: true
---

In modern web development, it is essential to optimize the loading time of web pages, especially when it comes to images. Progressive image loading is a technique that enhances the user experience by initially showing a low-resolution placeholder image and gradually replacing it with the higher resolution image as it loads. This technique significantly reduces the perceived page load time.

## Intersection Observer API

The **Intersection Observer API** is a powerful browser API that allows us to efficiently track the visibility of DOM elements within the viewport. It notifies us when a specific element intersects or becomes visible in the viewport. We can leverage this API to implement progressive image loading.

## Getting Started

Before we start, make sure you have a basic understanding of Redux and the Intersection Observer API. We will be using Redux to manage our application's state and the Intersection Observer API to track the visibility of images.

### Step 1: Set Up Redux

First, let's set up Redux in our application if it's not already done. Install the necessary packages and create the required files.

```bash
npm install redux react-redux
```

Create a `store.js` file and set up the Redux store with any necessary middleware and reducers.

```javascript
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import rootReducer from './reducers';

const store = createStore(rootReducer, applyMiddleware(thunk));

export default store;
```

### Step 2: Create Actions and Reducers

Next, let's create the necessary actions and reducers to handle the progressive image loading logic. We will assume that you have an existing Redux store set up.

Create an `imageActions.js` file and define the actions.

```javascript
export const loadImage = (url, id) => ({
  type: 'LOAD_IMAGE',
  payload: {
    url,
    id,
  },
});

export const imageLoaded = (id) => ({
  type: 'IMAGE_LOADED',
  payload: {
    id,
  },
});
```

Create a `imageReducer.js` file and define the reducer.

```javascript
const initialState = {};

const imageReducer = (state = initialState, action) => {
  switch (action.type) {
    case 'LOAD_IMAGE':
      return {
        ...state,
        [action.payload.id]: {
          url: action.payload.url,
          loaded: false,
        },
      };
    case 'IMAGE_LOADED':
      return {
        ...state,
        [action.payload.id]: {
          ...state[action.payload.id],
          loaded: true,
        },
      };
    default:
      return state;
  }
};

export default imageReducer;
```

### Step 3: Track Image Visibility

We will leverage the Intersection Observer API to track the visibility of the images and dispatch actions accordingly. Create a new file called `ProgressiveImage.js` and implement the following code:

```javascript
import React, { useEffect, useRef } from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { loadImage, imageLoaded } from './imageActions';

const ProgressiveImage = ({ url, id }) => {
  const dispatch = useDispatch();
  const imageRef = useRef(null);
  const images = useSelector((state) => state.images);

  useEffect(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting && !images[id].loaded) {
          dispatch(imageLoaded(id));
          const image = new Image();
          image.onload = () => {
            dispatch(imageLoaded(id));
          };
          image.src = images[id].url;
        }
      });
    });

    observer.observe(imageRef.current);

    return () => {
      observer.unobserve(imageRef.current);
    };
  }, [dispatch, id, images]);

  useEffect(() => {
    if (!images[id]) {
      dispatch(loadImage(url, id));
    }
  }, [dispatch, id, images, url]);

  return <img src={images[id]?.loaded ? images[id].url : placeholderImagePath} ref={imageRef} />;
};

export default ProgressiveImage;
```

We create a functional component `ProgressiveImage` that takes a `url` and an `id` as props. Inside the component, we use the `useRef` hook to create a reference to the image element and the `useSelector` hook to access the Redux store. We then use the `useEffect` hook to set up the Intersection Observer and handle the image loading logic.

### Step 4: Use ProgressiveImage Component

Finally, use the `ProgressiveImage` component in your application wherever you want to load images progressively.

```javascript
import React from 'react';
import ProgressiveImage from './ProgressiveImage';

const App = () => {
  return (
    <div>
      <h1>Progressive Image Loading Example</h1>
      <ProgressiveImage url="your-image-high-resolution-url" id="unique-id" />
    </div>
  );
};

export default App;
```

Replace `"your-image-high-resolution-url"` with the URL of your high-resolution image and `"unique-id"` with a unique identifier for the image.

## Conclusion

In this blog post, we explored how to implement progressive image loading using Redux and the Intersection Observer API. We set up Redux, created necessary actions and reducers, and used the Intersection Observer to track image visibility. By implementing this technique, we can significantly improve the perceived page load time and enhance the user experience.

#redux #intersection-observer-api