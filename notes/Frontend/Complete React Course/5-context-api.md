# Context API

## Create Context API
- When a component is hooked into the context, and the value of the context is changed, the functional component will be re run, but if there is nothing  to change in the DOM the component wont be rernder.
- Consider of when to use, becaouse it can cause performance issue when you hook into a context with a lots of component, and if the context value is change, then all the component it is possible to rerender.

```jsx
// ./src/contexts/user.context.jsx

import { createContext, useState } from "react";

// as the actual value want to access
export const UserContext = createContext({
    currentUser: null,
    setCurrentUser: () => null
});

// functional component
export const UserProvider = ({ children }) => {
    const [currentUser, setCurrentUser] = useState(null);
    const value = { currentUser, setCurrentUser };
    return <UserContext.Provider value={value}>{children}</UserContext.Provider>
}
```

## Wrap your app into the provider
```jsx
import { UserProvider } from './contexts/user.context';

...

<UserProvider>
    <App />
</UserProvider>
```

## Use the Context into the components
```jsx
import { UserContext } from "../../contexts/user.context";

...

const { setCurrentUser, currentUser } = useContext(UserContext)

```
