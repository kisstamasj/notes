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

### Setup Redux

#### File structure

- src/store/store.js