---
title: Redux store advanced setup with Redux devtools extension
description: Boilerplate code to setup Redux store with `Redux devtools extension` enhancer. This code uses the extension if its available and does not fail in the environments where the extension is not available.
tags: redux, redux-store, redux-devtools-extension
created: 2018-10-19
---

Its important to setup your Redux store to work with and without `Redux devtools extension`. 
This one of the common mistakes for the beginners to write the store setup by expecting the `Redux devtools extension` and fail in production with following error 
```javascript
redux.js:523 Uncaught TypeError: Cannot read property 'apply' of undefined
    at redux.js:523
    at o (redux.js:87)
    at Object.<anonymous> (store.js:7)
    at t (bootstrap ffa628421a5fd58f8088:19)
    at Object.<anonymous> (main.8c8e3ecf.js:14104)
    at t (bootstrap ffa628421a5fd58f8088:19)
    at Object.<anonymous> (main.8c8e3ecf.js:13117)
    at t (bootstrap ffa628421a5fd58f8088:19)
    at bootstrap ffa628421a5fd58f8088:62
    at bootstrap ffa628421a5fd58f8088:62
```

Following is the boilerplate code to setup Redux store with `Redux devtools extension` enhancer. This code uses the extension if its available and does not fail in the environments where the extension is not available. 

```javascript
import { createStore, applyMiddleware, compose } from 'redux';
import thunk from 'redux-thunk';
import rootReducer from './reducers';

const initialState = {};
const middleware = [thunk];


const composeEnhancers =
  typeof window === 'object' &&
   window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ ?   
    window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({
      // Specify extension’s options like name, actionsBlacklist, actionsCreators, serialize...
}) : compose;

const enhancer = composeEnhancers(
    applyMiddleware(...middleware),
    // other store enhancers if any
);    

const store = createStore(
    rootReducer, 
    initialState, 
    enhancer
);

export default store;
```