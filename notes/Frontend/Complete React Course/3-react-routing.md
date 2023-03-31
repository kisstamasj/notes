# React Routing

## [React Router](https://reactrouter.com/en/main)

- install: ```yarn add react-router-dom@6```
- Example:
```jsx
import Home from "./routes/home/home.component";
import { Routes, Route } from "react-router-dom";

const App = () => {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
    </Routes>
  );
}

export default App;
```
