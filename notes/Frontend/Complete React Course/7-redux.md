# Redux and Reducer

## Context API VS Redux
- Redux always warp the entire application, Context API can isolate the components
- Context API has multiple reducer and multiple action to dispatch the state, Redux has a root reducer and one action to update all reducer

## Reducer
Reducers are functions that take the current state and an action as arguments, and return a new state result. 
In other words, `(state, action) => newState.`

- In reducer there are no buisness logics.
- Reducer is useful when one update modify multiple values inside of the state (ex.: Put item in the cart, it will update the cart items, cart count and cart total)

## Context with Reducer
```jsx
import { useReducer } from 'react';

export const UserContext = createContext({
  currentUser: null,
  setCurrentUser: () => null,
});

export const USER_ACTION_TYPES = {
  SET_CURRENT_USER: 'SET_CURRENT_USER',
};

const userReducer = (state, action) => {
  const { type, payload } = action;

  switch (USER_ACTION_TYPES.SET_CURRENT_USER) {
    case 'SET_CURRENT_USER':
      return { ...state, currentUser: payload };
    default:
      throw new Error(`Unhandled type ${type} in userReducer`);
  }
};

const INITAL_STATE = {
  currentUser: null,
};

export const UserProvider = ({ children }) => {
  const [state, dispatch] = useReducer(userReducer, INITAL_STATE);
  const { currentUser } = state;
  const setCurrentUser = (user) => {
    dispatch({ type: USER_ACTION_TYPES.SET_CURRENT_USER, payload: user });
  };
  
  const value = { currentUser, setCurrentUser };

  return <UserContext.Provider value={value}>{children}</UserContext.Provider>;
};
```

## Redux
Global state management

- install: `yarn add redux react-redux redux-logger`
- all reducer in redux receive every single action that get dispatched 
- every reducer has own folder

### Setup Redux

#### File structure

- src/store/store.js
This is the main redux store file.
```js
import { compose, legacy_createStore as createStore, applyMiddleware } from 'redux';
import logger from 'redux-logger';

import { rootReducer } from './root-reducer';

const middleWares = [logger];

const composedEnhancers = compose(applyMiddleware(...middleWares));

export const store = createStore(rootReducer, undefined, composedEnhancers);

```
- custom middlware in the store.js
```js
import { compose, legacy_createStore as createStore, applyMiddleware } from 'redux';
import logger from 'redux-logger';

import { rootReducer } from './root-reducer';

const loggerMiddleware = (store) => (next) => (action) => {
  if (!action.type) {
    return next(action);
  }

  console.log('type', action.type);
  console.log('payload', action.payload);
  console.log('currentState', store.getState());
  next(action);
  console.log('next state: ', store.getState());
};

const middleWares = [loggerMiddleware];

const composedEnhancers = compose(applyMiddleware(...middleWares));

export const store = createStore(rootReducer, undefined, composedEnhancers);
```

- src/store/root-reducer.js

  - The root reducer combine all reducer to one. 
  - Whenever a reducer change the whole root reducer will be output a new object, so every useSelector will be re run, the will cause a component rerender.

```js
import { combineReducers } from 'redux';
import { userReducer } from './user/user.reducer';

export const rootReducer = combineReducers({
  user: userReducer,
});
```

- src/store/user/user.reducer.js

  User reducer is an example reducer.

```js
const INITAL_STATE = {
  currentUser: null,
};

export const userReducer = (state = INITAL_STATE, action) => {
  const { type, payload } = action;

  switch (type) {
    case 'SET_CURRENT_USER':
      return { ...state, currentUser: payload };
    default:
      return state;
  }
};
```
> In the default case need to return the incoming state

- src/store/user/user.action.js

  - The actions are setting the state in the store.
  - Every action has to return with an action type (`{type: ACTION_TYPE, payload: {}}`) with `creatAction` util

```js
import { createAction } from '../../utils/reducer/reducer.utils';
import { USER_ACTION_TYPES } from './user.types';

export const setCurrentUser = (user) => createAction(USER_ACTION_TYPES.SET_CURRENT_USER, user);
```

- src/store/user/user.types.js

  - Each reducer has own types. 
  - Best practice to write to the action is what for. 

```js
export const USER_ACTION_TYPES = {
  SET_CURRENT_USER: 'user/SET_CURRENT_USER',
};
```

- src/store/user/user.selector.js

  - Selector for retrive data from the store. 
  - Selector also contains the business logic of transform the data for more efficient way to use inside components.
  - If a a selector get fired then all selector will be run. Thats why useful the reselect library.

```js
export const selectCurrentUser = (state) => state.user.currentUser;
```

Convert categories array to a categories map
```js
export const selectCategoriesMap = (state) =>
  state.categories.categories.reduce((acc, category) => {
    const { title, items } = category;
    acc[title.toLowerCase()] = items;
    return acc;
  }, {});

```

#### Dispatch action:
```js
import { setCurrentUser } from './store/user/user.action';
import { useDispatch } from 'react-redux';

...

const dispatch = useDispatch();

...

dispatch(setCurrentUser(user));
```
> There are only one dispatch in the entire application

#### Get data from store
```js
import { useSelector } from 'react-redux';
import { selectCurrentUser } from '../../store/user/user.selector';

...

const currentUser = useSelector(selectCurrentUser);
```

### Reselect library

- install: `yarn add reselect`
- Memoize the reducer, do if some selector get fired the memoized selector will be only run when the current reducer changed.

```js
import { createSelector } from 'reselect';

const selectCategoryReducer = (state) => state.categories;

export const selectCategories = createSelector(
  [selectCategoryReducer],
  (categoriesSlice) => categoriesSlice.categories
);

export const selectCategoriesMap = createSelector([selectCategories], (categories) =>
  categories.reduce((acc, category) => {
    const { title, items } = category;
    acc[title.toLowerCase()] = items;
    return acc;
  }, {})
);
```

## Redux persist

- install: `yarn add redux-persist`
- store redux store data in local sotrage 

```js
//src/store/store.js
import { compose, legacy_createStore as createStore, applyMiddleware } from 'redux';
import logger from 'redux-logger';
import { rootReducer } from './root-reducer';

import { persistStore, persistReducer} from 'redux-persist'
import storage from 'redux-persist/lib/storage'

const persistConfig = {
  key: 'root',
  storage,
  blacklist: ['user']
}

const presistedReducer = persistReducer(persistConfig, rootReducer)

const middleWares = [logger];

const composedEnhancers = compose(applyMiddleware(...middleWares));

export const store = createStore(presistedReducer, undefined, composedEnhancers);

export const persistor = persistStore(store)
```

```jsx
// src/index.js

import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.scss';
import App from './App';
import reportWebVitals from './reportWebVitals';
import { BrowserRouter } from 'react-router-dom';
import { Provider } from 'react-redux';
import { persistor, store } from './store/store';
import { PersistGate } from 'redux-persist/integration/react';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <Provider store={store}>
      <PersistGate persistor={persistor}>
        <BrowserRouter>
          <App />
        </BrowserRouter>
      </PersistGate>
    </Provider>
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

## Middleware
```js
export const loggerMiddleware = (store) => (next) => (action) => {
  if (!action.type) {
    return next(action);
  }

  console.log('type', action.type);
  console.log('payload', action.payload);
  console.log('currentState', store.getState());
  next(action);
  console.log('next state: ', store.getState());
};
```
