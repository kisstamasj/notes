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

## Lifecycle methods
Lifecycle methods are special methods built into React, used to operate on components throughout their duration in the DOM. For example, when the component mounts, renders, updates, or unmounts.

- ```componentDidMount()```: Called whenerver the component mounted

![image](https://user-images.githubusercontent.com/48266482/227633389-56ef0d75-3e57-4420-b4ba-4c91b771c2e7.png)

### Lifecycle methods flow
1. constructor()
2. inital render()
3. componentDidMount()
4. after setState rerender the component

## Anonymus functions
Every time when a component is rerender javascript has to store again the anonymus function, because it isn't assigned to a variable, and then isn't in the memory.

## Folder structure policies

### Public
Take place all the publicly accessible files like pictures, favicon etct..

### components
- Inside that folder take place the components files. (jsx, css)
- Every component has its own folder
- The component name like this: ```comp-name.component.jsx```

## CSS in components
- import css file: ```import './App.css';```
- **Anywhere import the css file, it will applied in the entire app.**