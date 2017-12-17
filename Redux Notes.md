
## Basic Setup

**1. Create store in index.js:**
```
import {createStore} from 'redux';
const store = createStore();
```
Store takes a reducer as input. Store reducer logic into its own file.

**2. Create Store Folder under src****
**3. Create reducer.js file in Store folder**
```
const initialState = {
    counter: 0
}

const reducer = (state = initialState, action) => {
    return state;
}

export default reducer;
```
**4. Import reducer into index.js and pass it to createstore**

**5. Connect store to react application:**

- ```npm install 'react-redux'```
- ```import { Provider } from 'react-redux'```
- wrap app with provider: ```<Provider store={store}> <App /> </Provider>```

**6. Import connect in Container**

```import { connect } from 'react-redux';```

Connect is a function that returns a higher order function that you can pass the component to.
Then adjust the export statement:

```export default connect()(Counter);```

In connect, we pass two pieces of info: which part of the application state is important to us in
this container, and which actions do I want to dispatch

**8. Add mapStateToProps function**

```
const mapStateToProps = (state) =>  {
    return {
        ctr: state.counter
    };
}
```

and pass it to connect.

```export default connect(mapStateToProps)(Counter);```

Now connect gives us the Counter container with access to ctr property

**9. Now dispatch actions in the container**
```
const mapDispatchToProps = dispatch => {
    return {
        onIncrementCounter: () => dispatch({type: 'INCREMENT'}),
        onDecrementCounter: () => dispatch({type: 'DECREMENT'}),
        onAddCounter: () => dispatch({type: 'ADD', value: 5 }),
        onSubtractCounter: () => dispatch({type: 'SUBTRACT', value: 5})
    }
}
```
'react-redux' is giving us the dispatch function

**10. Adjust export statement**

```export default connect(mapStateToProps, mapDispatchToProps)(Counter);```

**11. Implement the logic in reducer.js**

```
const reducer = (state = initialState, action) => {
    switch (action.type) {
        case 'INCREMENT':
            return { counter: state.counter + 1};
        case 'DECREMENT':
            return { counter: state.counter -1};
        case 'ADD':
            return { counter: state.counter + action.value};
        case 'SUBTRACT':
            return { counter: state.counter + action.value};
        default:
            return state; // THIS IS IMPORTANT -- otherwise application breaks
    }
}
```

# Combining Multiple Reducers

In Store folder, create reducers folder
then in index.js 

```
import counterReducer from './store/reducers/counter';
import resultReducer from './store/reducers/results';
import {createStore, combineReducers} from 'redux';
const rootReducer = combineReducers({
    ctr: counterReducer,
    res: resultReducer
}) // merge everything into one reducer
const store = createStore(rootReducer);
```

Then adjust

```
const mapStateToProps = (state) =>  {
    return {
        ctr: state.ctr.counter,
        results: state.res.results
    };
}
```

But now you must connect the reducer, if you need value from global state, you get it as an action (payload)

# Adding Middleware: Go to index.js and add this code

```
const logger = store => {
    return next => {
        return action => {
            console.log('[Middleware] Dispatching', action);
            const result = next(action);
            console.log('[Middleware] next state', store.getState());
            return result;
        }
    }
}
```

Now we need to apply middleware to store.

```
import { applyMiddleware} from 'redux';
const store = createStore(rootReducer, applyMiddleware(logger));
```

Note: applyMiddleware(logger) is an enhancer.


# Redux Dev Tools Extension

```import {compose} from 'redux';```

```const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose; // compose is a fallback```

This is a variable injected by chrome extension into our JS at runtime. Add it to the
index.js file right before creating the store. Compose allows us to combine enhancers.

Now, change createStore to 

```const store = createStore(rootReducer, composeEnhancers(applyMiddleware(logger)));```

# Asynchronous Code and Redux

#### Action Creators

Create subfolder in store folder and name it actions. If you have an actions.js file, move it into the folder.

An action creator is a function which creates an action.

```
const increment = () => {
    return {
        type: INCREMENT
    };
};
export const storeResult = (result) => {
    return {
        type: STORE_RESULT,
        result: result
    };
};
```

We can now use action in container. In container add this import statement

```import * as actionCreators from '../../store/actions/action';```

Now, in mapDispatchToProps function, you can change

```
onIncrementCounter: () => dispatch({type: actionTypes.INCREMENT}),
storeResult: (result) => dispatch({type: actionTypes.STORE_RESULT, result: result})
```

 to 

```
onIncrementCounter: () => dispatch(actionCreators.increment()),
storeResult: (result) => dispatch(actionCreators.storeResult(result)),
```

Note: When you execute increment() you get an action

#### Add Middleware: Redux-thunk

Redux-thunk allows your action creators to return a function which will eventually dispatch an action. Now, you can run asynchronous code.

Run: ```npm install --save redux-thunk```

Go to index.js:
```import thunk from 'redux-thunk';```

Adjust
```const store = createStore(rootReducer, composeEnhancers(applyMiddleware(logger, thunk)));```

Now in the actions.js file, adjust the code as follows

```
// Synchronous action creators: Dispatch actions created by syncrhonous one
export const saveResult = ( result ) => {
    return {
        type: STORE_RESULT,
        result: result
    };
}
//Middleware runs between the dispatching of an action, and the point in time the action
//reaches reducer. Here we dispatch an action, thunk middleware steps in, blocks the old action,
//dispatches it again, in the future. The new action will reach the reducer, but in between, redux
//thunk is able to wait. This is the asynchronous part. 
export const storeResult = (result) => {
    return dispatch => {
        setTimeout(()=> {
            dispatch(saveResult(result));
        }, 2000);
    }
};
```

Note, you have access to state. You can do something like this.

```
export const storeResult = (result) => {
    return (dispatch, getState) => {
        setTimeout(()=> {
            const oldCounter = getState().ctr.counter;
            console.log(oldCounter);
            dispatch(saveResult(result));
        }, 2000);
    }
};
```

Don't abuse this, not necessary.

# Restructuring Actions Folder

This is for bigger projects.

1. Under store, create folder actions.
2. Under actions folder, create actionTypes.js, index.js (and whatever other action files: For example: counter.js, results.js where counter stores counter related actions and results stores results related actions)
3. In the actionTypes.js file, have all the action types
```
export const INCREMENT = 'INCREMENT';
export const DECREMENT = 'DECREMENT';
...
```
4. In the index.js file, have this
```
export {
    add,
    subtract,
    increment,
    decrement
} from './counter';
export {
    storeResult,
    removeResult
} from './result';
```
5. Now in the reducers, adjust the import

```import * as actionTypes from '../actions/actionTypes';```

# Action Creators vs Reducers - where to put the logic?

### Action Creators

- Can run Async Code
- Shouldn't prepare the state update too much

### Reducers

- Pure, Sync code only!
- Core Redux Concept: Reducers is the only thing that updates state

You can argue both ways, lean towards logic in reducer. Async code goes into action creator, once you have data
that is relatively clean (i.e you changed it up a bit), pass it to reducer. Choose an approach and stick to it.
Be consistent. 

# Good Practice: Clean up Reducer

1. In store folder, create utility.js

```
export const updateObject = (oldObject, updatedValues) => {
    return {
        ...oldObject,
        ...updatedValues
    }
};
```

2. In reducer file

```
import { updateObject } from '../utility';

const reducer = (state = initialState, action) => {
    switch (action.type) {
        case actionTypes.SUBTRACT:
            return updateObject(state, {counter: state.counter - action.value});
        ...
    }
}
```
