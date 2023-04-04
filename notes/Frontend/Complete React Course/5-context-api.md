# Context API

## Create Context API

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
