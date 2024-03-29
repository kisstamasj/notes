# React Routing

## [React Router](https://reactrouter.com/en/main)

- install: ```yarn add react-router-dom@6```
- Example:
```jsx
//index.js
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.scss';
import App from './App';
import reportWebVitals from './reportWebVitals';
import { BrowserRouter } from 'react-router-dom';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();

```
```jsx
//App.js
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
## Fix component between routes:
- Int the parent element need to use the ```Outlet``` component from ```react-router-dom```. This component tells react where to put the children components.
- ```index``` property in Route component tells to the nested route to be the index page of the parent route.
```jsx
//App.js
import Home from "./routes/home/home.component";
import { Routes, Route, Outlet } from "react-router-dom";

const Navigation = () => {
  return (
    <div>
      <div>
        <h1>Navigation</h1>
      </div>
      <Outlet />
    </div>
  )
}

const Shop = () => {
  return (
    <h1>Shop</h1>
  )
}

const App = () => {
  return (
    <Routes>
      <Route path="/" element={<Navigation />}>
        <Route index={true} element={<Home />} />
        <Route path="shop" element={<Shop />} />
      </Route>
    </Routes>
  );
}

export default App;
```
```jsx
// routes/home/home.component.jsx
import Directory from "../../components/directory/directory.component";
import categories from '../../categories.json'
import { Outlet } from "react-router-dom";

const Home = () => {
    return (
        <>
            <Outlet />
            <Directory categories={categories} />
        </>
    );
}

export default Home;
```

## Nested Route
```jsx
//src/app.jsx

import Home from "./routes/home/home.component";
import { Routes, Route } from "react-router-dom";
import Navigation from "./routes/navigation/navigation.component";
import Authentication from "./routes/authentication/authentication.component";
import Shop from './routes/shop/shop.component';
import Checkout from './routes/checkout/checkout.component';

const App = () => {
  return (
    <Routes>
      <Route path='/' element={<Navigation />}>
        <Route index={true} element={<Home />} />
        <Route path='shop/*' element={<Shop />} /> // nested route
        <Route path='auth' element={<Authentication />} />
        <Route path='checkout' element={<Checkout />} />
      </Route>
    </Routes>
  );
};

export default App;
```
```jsx
//src/routes/shop.component.jsx

import { Routes, Route } from 'react-router-dom';
import './shop.styles.scss';
import CategoriesPreview from '../categories-preview/categories-preview.component';

const Shop = () => {
  return (
    <Routes>
      <Route index element={<CategoriesPreview />} ></Route>
    </Routes>
  );
};

export default Shop;
```

## Route parameter
```jsx
import { Routes, Route } from 'react-router-dom';
import './shop.styles.scss';
import CategoriesPreview from '../categories-preview/categories-preview.component';
import Category from '../category/category.component';

const Shop = () => {
  return (
    <Routes>
      <Route index element={<CategoriesPreview />} ></Route>
      <Route path=':category' element={<Category />} ></Route> /* parameter: /shop/some-param */
    </Routes>
  );
};

export default Shop;
```

```jsx
import { useParams } from 'react-router-dom';

...

const {category} = useParams()
```

## Navigating between routes:
```jsx
import { Link } from "react-router-dom"
...
<Link className="nav-link" to='/shop'>Shop</Link>
...
```

## OR

```jsx
import { useNavigate } from 'react-router-dom';

...

const navigate = useNavigate();

...

<Button onClick={() => navigate('/navigate-to')}>Navigatet</Button>
```

