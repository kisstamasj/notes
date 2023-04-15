# NPM vs. Yarn

- Install dependencies from package.json: ```npm install == yarn```
- Install a package and add to package.json: ```npm install package --save == yarn add package```
- Install a devDependency to package.json: ```npm install package --save-dev == yarn add package --dev```
- Remove a dependency from package.json: ```npm uninstall package --save == yarn remove package```
- Upgrade a package to its latest version: ```npm update --save == yarn upgrade```
- Install a package globally: ```npm install package -g == yarn global add package```

# CLI commands

- create react app: ```npx create-react-app@latest <your-project-name>```

# JSX
JSX stands for JavaScript XML. JSX allows us to write HTML in React. JSX makes it easier to write and add HTML in React.

# Class components 

## Basic Class component
- The render method render the UI.
- The render method can return only one element, can not be a sibling element
  ```jsx
  render() {
      return (
          <div>
              <h1>Hello this is the CardList component</h1>
          </div>
      )
  }
  ```
- The render method will be called when on state change or props change. If a component is getting rerender then all the component will be rerendered inside that component. The render flow goes down on the component tree.

```jsx
import { Component } from 'react'

import logo from './logo.svg';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <p>
            Edit <code>src/App.js</code> and save to reload.
          </p>
          <a
            className="App-link"
            href="https://reactjs.org"
            target="_blank"
            rel="noopener noreferrer"
          >
            Learn React
          </a>
        </header>
      </div>
    );
  }
}

export default App;
```

## Class Component State Management
- Whenever the state changes then the whole component is rerendered.
- set the state: ```this.setState()``` 
  - this method will shallow merge the current state, this means only updates the given property of the state
  - the set State method is an asyncronous function
  - it can access two callback function: the first is the setter (the return object will be the state), the second function will be called after the setState
    ```jsx
    this.setState(() => {
        return {name:{firstName: 'Tomi', lastName: 'Kiss'}}
      }, () => {
        console.log(this.state)
      })
    }}
    ```

```jsx
import { Component } from 'react'

import logo from './logo.svg';
import './App.css';

class App extends Component {
  constructor(){
    super();

    this.state = {
      name: {firstName: 'Yihua', lastName: 'Zhang'},
      company: 'ZTM'
    }
  }

  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <p>
            Hi {this.state.name.firstName } {this.state.name.lastName}, I work at {this.state.company}
          </p>
          <button
            onClick={() => {
              this.setState({name:{firstName: 'Tomi', lastName: 'Kiss'}})
              console.log(this.state)
            }}>Change Name</button>
        </header>

      </div>
    );
  }
}

export default App;
```

## Lifecycle methods in class components
Lifecycle methods are special methods built into React, used to operate on components throughout their duration in the DOM. For example, when the component mounts, renders, updates, or unmounts.

- ```componentDidMount()```: Called whenerver the component mounted

![image](https://user-images.githubusercontent.com/48266482/227633389-56ef0d75-3e57-4420-b4ba-4c91b771c2e7.png)

### Lifecycle methods flow
1. constructor()
2. inital render()
3. componentDidMount()
4. after setState rerender the component

# Functional Component
- No constructor method (there is no class), because its just function
- Return JSX
- React just call the functional component and put the return to the page
- There is no lifecycle methods
- If state or props are changing then the full function get called again and runs from top to bottom. Unlike in class component where only get called the render method.
- Properties came from the props parameter of the function
  ```jsx
  const Card = ({ id, name, email }) => {
      return (
          <div className="card-container">
              <img alt={`monster ${name}`} src={`https://robohash.org/${id}?set=set2&size=180x180`} />
              <h2>{name}</h2>
              <p>{email}</p>
          </div>
      )
  }
  ```

```jsx
import { useEffect, useState } from 'react'

import CardList from './components/card-list/card-list.component';
import './App.css';
import SearchBox from './components/search-box/search-box.component';

const App = () => {

  const [monsters, setMonsters] = useState([])
  const [searchField, setSearchField] = useState('')

  const fetchData = () => {
    fetch('https://jsonplaceholder.typicode.com/users')
      .then((response) => response.json())
      .then((users) => setMonsters(users))
  }

  useEffect(() => {
    fetchData()
  }, [])

  const filterdMonsters = monsters.filter((monster) => {
    return monster.name.toLowerCase().includes(searchField);
  })

  const onSearchChange = (e) => {
    const searchField = e.target.value.toLowerCase();
    setSearchField(searchField)
  }

  return (
    <div className="App">
      <h1 className='app-title'>Monster Rolodex</h1>
      <SearchBox onChangeHandler={onSearchChange} placeholder='search monsters' className='monsters-search-box' />
      <CardList monsters={filterdMonsters} />
    </div>
  )
}
```

## Hooks
React Hooks are a way for your function components to “hook” into React’s lifecycle and state. They were introduced in React 16.8.0. Previously, only Class based components were able to use React’s lifecycle and state. Aside from enabling Function components to do this, Hooks make it incredibly easy to reuse stateful logic between components.

- ```useState()```: [**useState**](https://react.dev/reference/react/useState) is React Hook that allows you to add state to a functional component. It returns an array with two values: the current state and a function to update it. The Hook takes an initial state value as an argument and returns an updated state value whenever the setter function is called.
- ```useEffect()```: [**useEffect(callback, dependencies)**](https://react.dev/reference/react/useEffect#useeffect) is the hook that manages the side-effects in functional components. callback argument is a function where to put the side-effect logic. dependencies is a list of dependencies of your side-effect: being props or state values. Best practices is when the useEffect only contains one effect.

# Folder structure policies

## ./public
Take place all the publicly accessible files like, index.html, pictures, favicon etc..

## ./src
All source code files

### ./src/assets
Take place all asset file like svg, icon etc...

### ./src/components
- Inside that folder take place the components files. (jsx, css)
- Every component has its own folder
- The component name like this: ```comp-name.component.jsx```

### ./src/routes
- That folder holds up the routing files, page files.
- Each rout get its own folder.
- File naming: ```rout-name.component.jsx```

### ./src/utils
- utility functions, for example connection to firebase
- each utility has own folder

### ./src/contexts
- floder for context APIs
- file naming: ```context-name.context.jsx```

# CSS in components
- import css file: ```import './App.css';```
- **Anywhere import the css file, it will applied in the entire app.**


# Keywords

## [Virtual DOM](https://legacy.reactjs.org/docs/faq-internals.html)

## reflow 
A reflow computes the layout of the page. A reflow on an element recomputes the dimensions and position of the element, and it also triggers further reflows on that element’s children, ancestors and elements that appear after it in the DOM. Then it calls a final repaint. Reflowing is very expensive, but unfortunately it can be triggered easily.

Reflow occurs when you:

- insert, remove or update an element in the DOM
- modify content on the page, e.g. the text in an input box
- move a DOM element
- animate a DOM element
- take measurements of an element such as offsetHeight or getComputedStyle
- change a CSS style
- change the className of an element
- add or remove a stylesheet
- resize the window
- scroll

## Props drilling
What is Prop Drilling? In a traditional React application, data is often shared between components using props. Manually sharing this data can be hectic, especially when shared between multiple nested components. Also, sharing data between two child components can be cumbersome.

## Anonymus functions
Every time when a component is rerender javascript has to store again the anonymus function, because it isn't assigned to a variable, and then isn't in the memory.

## Pure function
Pure functions are the functions that always yield consistent output and do not have any side effects. Pure function makes the code easily readable, and testable and increases the performance.

## Inpure function
An inpure function is a function that contains one or more side effects. It mutates data outside of its lexical scope and does not predictably produce the same output for the same input.

### [Pure and Inpure functions example](https://dev.to/codeofrelevancy/you-need-to-know-about-pure-functions-impure-functions-in-javascript-57)

# Special components

## Fragment
This is a special built in react component. Useful when you dont want any element for root element of a component. React will just render nothing.
With that component is equivalent if you use just empty tags: ```<></>```.
```jsx
import { Fragment } from "react"
import { Outlet } from "react-router-dom"

const Navigation = () => {
    return (
        <Fragment>
            <div>
                <h1>Navigation</h1>
            </div>
            <Outlet />
        </Fragment>
    )
}


export default Navigation
```

OR

```jsx
import { Fragment } from "react"
import { Outlet } from "react-router-dom"

const Navigation = () => {
    return (
        <>
            <div>
                <h1>Navigation</h1>
            </div>
            <Outlet />
        </>
    )
}


export default Navigation
```

## Importing SVG as react component
```jsx
import { ReactComponent as CrwnLogo } from '../../assets/crown.svg'
```

## Handling forms
- one object in state for every form input
```js
const defaultFormFields = {
    email: '',
    password: ''
}

...

const [formFields, setFormfields] = useState(defaultFormFields)

...

//handeling input value change
const handleChange = (event) => {
    const { name, value } = event.target;

    setFormfields({ ...formFields, [name]: value })
}

```

## [React Design Patterns](https://www.linkedin.com/pulse/most-common-react-design-patterns-baqir-nekfar) 
