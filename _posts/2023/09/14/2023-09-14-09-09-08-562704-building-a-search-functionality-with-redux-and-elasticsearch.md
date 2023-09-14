---
layout: post
title: "Building a search functionality with Redux and Elasticsearch"
description: " "
date: 2023-09-14
tags: [redux, elasticsearch]
comments: true
share: true
---

Search functionality is a crucial part of many web applications, allowing users to quickly find the information they need. In this tutorial, we will explore how to build a search functionality using Redux for state management and Elasticsearch as our search engine.

## Prerequisites 
To follow along, make sure you have the following installed:

- Node.js
- Redux
- Elasticsearch

## Setting Up Elasticsearch

First, let's set up Elasticsearch. Download and install Elasticsearch onto your machine. Once installed, start the Elasticsearch server.

## Installing Redux and Dependencies

Create a new Redux project by running the following command in your terminal:

```
npx create-react-app search-app
cd search-app
```

Now, install the necessary dependencies:

```
npm install redux react-redux elasticsearch
```

## Setting Up the Redux Store

In the src folder, create a new file called store.js. In this file, set up the Redux store and the necessary reducers and actions:

```javascript
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import { createLogger } from 'redux-logger';
import rootReducer from './reducers';

const logger = createLogger();

const store = createStore(
  rootReducer,
  applyMiddleware(thunk, logger)
);

export default store;
```

## Creating Redux Actions

Create a new file called actions.js in the src folder. This file will contain the actions needed for searching:

```javascript
import { search } from './elasticsearch';

export const SEARCH_REQUEST = 'SEARCH_REQUEST';
export const SEARCH_SUCCESS = 'SEARCH_SUCCESS';
export const SEARCH_FAILURE = 'SEARCH_FAILURE';

export const searchRequest = () => ({
  type: SEARCH_REQUEST,
});

export const searchSuccess = (results) => ({
  type: SEARCH_SUCCESS,
  payload: results,
});

export const searchFailure = (error) => ({
  type: SEARCH_FAILURE,
  payload: error,
});

export const performSearch = (query) => {
  return async (dispatch) => {
    dispatch(searchRequest());

    try {
      const results = await search(query);
      dispatch(searchSuccess(results));
    } catch (error) {
      dispatch(searchFailure(error));
    }
  };
};
```

## Creating the Elasticsearch Integration

Create a new file called elasticsearch.js in the src folder. In this file, integrate with Elasticsearch and perform the search query:

```javascript
import { Client } from 'elasticsearch';

const client = new Client({ node: 'http://localhost:9200' });

export const search = async (query) => {
  try {
    const response = await client.search({
      index: 'myindex',
      body: {
        query: {
          match: {
            myfield: query,
          },
        },
      },
    });

    return response.hits.hits;
  } catch (error) {
    throw new Error('Error performing search');
  }
};
```

## Creating the Search Component

In the src folder, create a new file called SearchComponent.js. This file will contain the UI component for the search functionality:

```javascript
import React, { useState } from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { performSearch } from './actions';

const SearchComponent = () => {
  const [query, setQuery] = useState('');
  const results = useSelector((state) => state.search.results);
  const dispatch = useDispatch();

  const handleSearch = () => {
    dispatch(performSearch(query));
  };

  return (
    <div>
      <input
        type="text"
        value={query}
        onChange={(e) => setQuery(e.target.value)}
      />
      <button onClick={handleSearch}>Search</button>
      <ul>
        {results.map((result) => (
          <li key={result._id}>{result._source.name}</li>
        ))}
      </ul>
    </div>
  );
};

export default SearchComponent;
```

## Integrating Redux and the Search Component

In the src folder, open the App.js file and update it as follows:

```javascript
import React from 'react';
import { Provider } from 'react-redux';
import store from './store';
import SearchComponent from './SearchComponent';

const App = () => {
  return (
    <Provider store={store}>
      <SearchComponent />
    </Provider>
  );
};

export default App;
```

## Conclusion
In this tutorial, we have explored how to build a search functionality using Redux and Elasticsearch. By leveraging the power of Redux for state management and Elasticsearch for fast and efficient search, you can create robust search functionalities in your web applications.

#redux #elasticsearch