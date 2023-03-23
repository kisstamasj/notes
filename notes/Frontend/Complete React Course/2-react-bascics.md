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

# Class and Functional components 

## Basic Class component
The render method render th UI.
```js
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

## Class Component State management
- Whenever the state changes then the whole component is rerendered.
- set the state: ```this.setState()``` 
  - this method will shallow merge the current state, this means only updates the given property of the state
  - the set State method is an asyncronous function
  - it can access two callback function: the first is the setter (the return object will be the state), the second function will be called after the setState
    ```js
    this.setState(() => {
        return {name:{firstName: 'Tomi', lastName: 'Kiss'}}
      }, () => {
        console.log(this.state)
      })
    }}
    ```

```js
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
