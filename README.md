# React Redux Spinner

A simple spinner for any "long" running tasks (such as fetching data off a server).

![Demo of spinner functionality](https://github.com/Storytel/react-redux-spinner/raw/master/rrs.gif)

**DEMO**:  https://storytel.github.io/react-redux-spinner

## Installation

```bash
npm install react-redux-spinner --save
```

## Usage

Import the library.
```javascript
import {
  Spinner, // The React component
  pendingTasksReducer, // The redux reducer
  pendingTask, // The action key for modifying loading state
  begin, // The action value if a "long" running task begun
  end // The action value if a "long" running task ended
} from 'react-redux-spinner';
```

Install the reducer to the store. Make sure it reduces the `pendingTasks` key.
This is best done using `combineReducers` from `redux`.

```javascript
import { createStore, combineReducers } from 'redux'
const reducer = combineReducers({
  pendingTasks: pendingTasksReducer
});

const store = createStore(reducer);
```

Put the `Spinner` component anywhere in your application.

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
const App extends React.Component {
  render() {
    return (<Spinner />)
  }
}
```

Start a long running task. This will increase the running tasks counter by 1.
The spinner will be shown when the running tasks is greater than 0.
```javascript
store.dispatch({
  type: 'ANY_OF_YOUR_ACTION_TYPES'
  [ pendingTask ]: begin // Make sure you embrace `pendingTask` in brackets [] to evaluate it
  // Any additional key/values may be included here
});
```

When your long running task is done.
```javascript
store.dispatch({
  type: 'ANY_OF_YOUR_ACTION_TYPES_DONE'
  [ pendingTask ]: end
  // Any additional key/values may be included here
});
```

## Pro-tips

  * Don't want to bloat your namespace with `begin` or `end` variables?

```javascript
import rrs from 'react-redux-spinner';

dispatch({
  type: 'ACTION_TYPE',
  [ rrs.pendingTask ]: rrs.begin
});
```

  * Use [ES6 object shorthand syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer)

```javascript
import { pendingTasksReducer as pendingTasks } from 'react-redux-spinner';
const reducer = combineReducers({ pendingTasks });
```

