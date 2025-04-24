# REACT

- React is an open-source JavaScript library used to build user interfaces, primarily for single-page applications (SPAs).
- It was created and is maintained by Meta (formerly Facebook).
- React focuses on building reusable UI components that update efficiently when data changes.

## Components

- A component is a reusable, independent block of UI. You can combine components to build complex interfaces.

Two types of components :

### Functional Components

- Functional components are simple JavaScript functions that takes props as input and  return JSX (UI elements).
- Earlier known as stateless components.
- With the introduction of Hooks (from React 16.8), they can now manage state, side effects, and more.
- Preferred way to write components today.

```

function Welcome() {
  return <h1>Hello, Welcome to React!</h1>;
}

export default Welcome;

```

### Class Components

- It Uses ES6 classes and extend React.Component .It must have render method to return JSX.
- Traditional way of writing stateful components.
- Use lifecycle methods and manage state via this.state

```

class Welcome extends React.Component{
  render(){
    return <h1>Hello, Welcome to React!</h1>;
  }
}

```

## JSX

- JSX stands for JavaScript XML.
- It’s a special syntax extension used in React that allows writing HTML-like code inside JavaScript.
- Even though JSX looks like HTML, it's actually JavaScript under the hood.
- JSX makes UI code cleaner, readable, and lets you embed JavaScript expressions using {}

```

// JSX gets converted by Babel into plain JavaScript:
const element = <h1 className="title" id="heading">Hello, React!</h1>

// converts to this
const element = React.createElement(
  "h1",
  { className: "title", id: "heading" },
  "Hello, React!"
);

React.createElement(type, props, children);

- type: the HTML tag or React component name
- props: an object of attributes/props (or null if none)
- children: content inside the tag (text or more elements)

```
- JSX must have one parent/root element:
- Use **className** instead of class
- Use camelCase for events and attributes: onClick, htmlFor, tabIndex

## Props

- Props are short for properties.
- They are read-only and used to pass data from a parent component to a child component.
- Think of props like function arguments — they help components be reusable and customizable.
- Props are immutable they cannot be changed by the child component.

## State

- State is a built-in object that stores dynamic data in a component.
- When the state changes, the component re-renders.
- Unlike props, state is local to the component and can be changed.

```

import React, { useState } from 'react';

function Welcome(props) {
  // Using state
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>Hello, {props.name}!</h1> {/* Using props */}
      <p>You clicked {count} times.</p>
      <button onClick={() => setCount(count + 1)}>Click Me</button>
    </div>
  );
}

// Usage
// <Welcome name="John" />

import React, { Component } from 'react';

class Welcome extends Component {
  constructor(props) {
    super(props);
    // Using state
    this.state = {
      count: 0
    };
  }

  handleClick = () => {
    this.setState({ count: this.state.count + 1 }); // Updating state
  };

  render() {
    return (
      <div>
        <h1>Hello, {this.props.name}!</h1> {/* Using props */}
        <p>You clicked {this.state.count} times.</p>
        <button onClick={this.handleClick}>Click Me</button>
      </div>
    );
  }
}

// Usage
// <Welcome name="John" />

```

### this.setState

- It's the method used to update the component’s state.
- When you call setState(), React will re-render the component with the updated state.
- It is asynchronous — meaning it may not update the state immediately.

2 ways using setState

```
// first one
this.setState({ count: this.state.count + 1 });

// second one
this.setState((prevState) => ({
  count: prevState.count + 1
}));

React may batch multiple setState calls together for performance.
So if you're doing:

this.setState({ count: this.state.count + 1 });
this.setState({ count: this.state.count + 1 });
You might still end up with only +1 instead of +2.

✅ But with callback:

this.setState(prev => ({ count: prev.count + 1 }));
this.setState(prev => ({ count: prev.count + 1 }));
You’ll correctly get +2.


```

## Event Handler and Binding

- An event handler is a function that runs when a user interacts with the UI — like clicking a button, typing in an input, etc.

```

import React from "react";

class Welcome extends React.Component {
  constructor() {
    super();
    this.state = { count: 0 };
  }

  clickHandler() {
    console.log(this); // Here this is undefined
  }
  render() {
    return (
      <div>
        <h1>{this.state.count}</h1>
        <button onClick={this.clickHandler}>Increment</button>
      </div>
    );
  }
}

export default Welcome;

// When a regular function is called in strict mode, and it's not bound to any object, the value of this becomes undefined

**There are ways to handle this**

First approach :

import React from "react";

class Welcome extends React.Component {
  constructor() {
    super();
    this.state = { count: 0 };
  }

  clickHandler() {
    console.log(this);
  }
  render() {
    return (
      <div>
        <h1>{this.state.count}</h1>
        <button onClick={this.clickHandler.bind(this)}>Increment</button>
      </div>
    );
  }
}

export default Welcome;

- this.clickHandler.bind(this) ensures that this inside the function always refers to the current instance of the Welcome class, preventing it from being undefined.
- Calling .bind(this) inside render() creates a new function on every re-render, which can impact performance.

Second approach :

- To optimize, bind the method once in the constructor or use an arrow function.

import React from "react";

class Welcome extends React.Component {
  constructor() {
    super();
    this.state = { count: 0 };
    this.clickHandler = this.clickHandler.bind(this);
  }

  clickHandler() {
    console.log(this);
  }
  render() {
    return (
      <div>
        <h1>{this.state.count}</h1>
        <button onClick={this.clickHandler}>Increment</button>
      </div>
    );
  }
}

export default Welcome;

Third approach :

import React from "react";

class Welcome extends React.Component {
  constructor() {
    super();
    this.state = { count: 0 };
  }

  clickHandler = () => {
    console.log(this);
  };
  render() {
    return (
      <div>
        <h1>{this.state.count}</h1>
        <button onClick={this.clickHandler}>Increment</button>
      </div>
    );
  }
}

export default Welcome;

- Arrow functions don’t have their own this binding. Instead, they lexically inherit this from their parent scope (the context where the function is defined).
- In the case of React class components, when you define an arrow function as a method, this refers to the class instance, because the arrow function inherits this from the class constructor (the parent scope).

Fourth approach :

import React from "react";

class Welcome extends React.Component {
  constructor() {
    super();
    this.state = { count: 0 };
  }

  clickHandler() {
    console.log(this);
  }
  render() {
    return (
      <div>
        <h1>{this.state.count}</h1>
        <button onClick={() => this.clickHandler()}>Increment</button>
      </div>
    );
  }
}

export default Welcome;

- Arrow functions inherit this lexically from their surrounding context, so using () => this.clickHandler() ensures this correctly refers to the component instance in the method.
- Using an arrow function in the event handler ensures this is correctly bound, but it creates a new function on each render, which can impact performance in larger apps


```

- It’s usually better to use one of the other methods like binding in the constructor or using an arrow function in the class property.(2 and 3 methods)

## Conditional Rendering
- Conditional rendering means showing components or elements based on a condition.

```

{isLoggedIn ? <Dashboard /> : <Login />}

{hasError && <p>Error occurred!</p>}

function Greeting({ isLoggedIn }) {
  if (isLoggedIn) return <h1>Welcome!</h1>;
  else return <h1>Please login</h1>;
}

```

## List Rendering

- Used to render multiple items from an array using .map()

```

const users = ["Alice", "Bob", "Charlie"];

{users.map((user, index) => (
  <p key={index}>{user}</p>
))}

```
- **Keys** are special string attribute that help react indentify which elements have been changed, addeded or removed. A key must be unique among siblings.

- When a React component re-renders (for example, due to state or props change), React doesn't directly update the real DOM. Instead, it updates a lightweight copy called the Virtual DOM.

Here's how the process works:

- React creates a new Virtual DOM that represents the updated UI.
- It then compares the new Virtual DOM with the previous one using a process called diffing.

During this comparison, keys play a critical role:

- They help React identify which items in a list have changed, moved, been added, or removed.
- If a key remains the same between renders, React assumes the item is the same and preserves its DOM node and internal state.
- If the key is different or reused incorrectly (like using index), React destroys the old node and creates a new one, which can lead to performance issues and UI bugs.
- After diffing, React performs reconciliation — it updates only the parts of the real DOM that actually changed, instead of re-rendering the whole page.

**Why Keys Matter**

- With the right keys (like unique IDs), React efficiently updates the DOM with minimal changes.
- Using unstable keys (like array index) makes it hard for React to match elements correctly, leading to unnecessary re-renders or even incorrect UI behavior.

- **Diffing** is comparing the old and new Virtual DOM trees to find differences.
- **Reconciliation** is updating the real DOM efficiently based on those differences.

## Real DOM (Document Object Model)

- The Real DOM is the actual structure that the browser uses to represent the page. It's a tree-like structure where each node is an element in the webpage (e.g., <div>, <p>, etc.).

- Key Points about Real DOM:
  
- Slower Performance: Direct manipulations of the real DOM are often slow. Changing an element requires a complete re-render of the entire DOM tree, even if only one small part of the UI has changed.

- Heavy Re-rendering: Every time the state of the app changes, the real DOM is updated, leading to possible performance issues, especially with large applications.

- Browser-Dependent: The real DOM is tightly connected to the browser, and the page’s state is rendered immediately in the UI.

## Virtual DOM

- The Virtual DOM is a lightweight copy of the real DOM. It is an in-memory representation of the real DOM that React uses to optimize rendering performance.

- Key Points about Virtual DOM:
  
- Faster Updates: The virtual DOM allows React to perform efficient diffing by comparing the old virtual DOM with the new one, finding the differences, and only updating the changed parts in the real DOM.

- No Direct Manipulation: The virtual DOM is not visible in the browser, and we never directly manipulate it. It’s simply a tool for React to efficiently calculate and update what’s necessary in the real DOM.

- Reconciliation: React uses the virtual DOM to figure out the minimal set of updates to apply to the real DOM (through a process called reconciliation). This minimizes re-rendering and improves performance.

## React styling 

### Inline Styles

Pros: Easy to use, ideal for small components or dynamic styles.
Cons: Cannot use media queries, pseudo-classes, or complex styles.ions.

 ### Stylesheets (CSS)

Pros: Well-known, easy to set up, and supports all CSS features.
Cons: Global scope can lead to style conflicts, harder to maintain in large applications.

 ### CSS Modules

Pros: Well-known, easy to set up, supports all CSS features.
Cons: Global styles can cause conflicts, harder to manage in large apps.

 ### Styled Components

Pros: Combines CSS with JavaScript for scoped and dynamic styles, supports all CSS features.
Cons: Adds a dependency, may impact performance and increase bundle size..

```

import React, { useState } from "react";

// Inline Styles
const inlineStyles = {
  backgroundColor: "lightblue",
  color: "darkblue",
  padding: "10px",
  borderRadius: "5px",
};

// Stylesheets (CSS)
import './styles.css';

// CSS Modules
import styles from './App.module.css';

// Styled Components
import styled from 'styled-components';

const Button = styled.button`
  background-color: lightcoral;
  color: white;
  padding: 10px;
  border-radius: 5px;
  &:hover {
    background-color: coral;
  }
`;

function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      {/* Inline Styles */}
      <div style={inlineStyles}>
        <h1>Inline Styles</h1>
        <p>Count: {count}</p>
        <button style={inlineStyles} onClick={() => setCount(count + 1)}>
          Increment
        </button>
      </div>

      {/* Stylesheets (CSS) */}
      <div className="stylesheet">
        <h1>Stylesheets (CSS)</h1>
        <p>Count: {count}</p>
        <button className="button" onClick={() => setCount(count + 1)}>
          Increment
        </button>
      </div>

      {/* CSS Modules */}
      <div className={styles.moduleContainer}>
        <h1>CSS Modules</h1>
        <p>Count: {count}</p>
        <button className={styles.button} onClick={() => setCount(count + 1)}>
          Increment
        </button>
      </div>

      {/* Styled Components */}
      <div>
        <h1>Styled Components</h1>
        <p>Count: {count}</p>
        <Button onClick={() => setCount(count + 1)}>
          Increment
        </Button>
      </div>
    </div>
  );
}

export default App;

styles.css (for Stylesheets)

/* Global styles */
.stylesheet {
  background-color: lightyellow;
  padding: 20px;
  border-radius: 8px;
}

.button {
  background-color: lightgreen;
  color: white;
  padding: 10px;
  border-radius: 5px;
}

App.module.css (for CSS Modules)


/* Scoped styles using CSS Modules */
.moduleContainer {
  background-color: lightgreen;
  padding: 20px;
  border-radius: 8px;
}

.button {
  background-color: lightpink;
  color: white;
  padding: 10px;
  border-radius: 5px;
}


```

## Controlled and uncontrolled components

- In controlled components, the form element's value is controlled by React state. The value of the input is always in sync with the component's state, and React handles all updates to the state.

```

import React, { useState } from 'react';

function ControlledInput() {
  const [value, setValue] = useState('');

  const handleChange = (e) => {
    setValue(e.target.value); // React state controls the input value
  };

  return (
    <input
      type="text"
      value={value} // The value is controlled by state
      onChange={handleChange}
    />
  );
}

export default ControlledInput;

```
- In uncontrolled components, form data is handled by the DOM itself, rather than React. You don't manage the state of the form element, and you access the value using a ref.

```

import React, { useRef } from 'react';

function UncontrolledInput() {
  const inputRef = useRef();

  const handleSubmit = () => {
    alert('Value: ' + inputRef.current.value); // Get the value via ref
  };

  return (
    <div>
      <input type="text" ref={inputRef} />
      <button onClick={handleSubmit}>Submit</button>
    </div>
  );
}

export default UncontrolledInput;

```

- In general, controlled components are preferred for forms where you need full control over the input fields and data, whereas uncontrolled components can be used for simpler forms where you don’t need to interact with the input state frequently.

## Lifecycle of components

- 3 Phases

1. Mounting
2. Updating
3. Unmounting

## Mounting 

- Mounting means putting elements into the DOM.

React has four built-in methods that gets called, in this order, when mounting a component:

- **constructor()**
- **getDerivedStateFromProps()**
- **render()**
- **componentDidMount()**

### Construtor 

- The constructor() method is called before anything else, when the component is initiated, and it is the natural place to set up the initial state and other initial values.
- The constructor() method is called with the props, as arguments, and you should always start by calling the super(props) before anything else, this will initiate the parent's constructor method and allows the component to inherit methods from its parent (React.Component).

### getDerivedStateFromProps

- The getDerivedStateFromProps() method is called right before rendering the element(s) in the DOM.
- This is the natural place to set the state object based on the initial props.
- It takes state as an argument, and returns an object with changes to the state.

### render

- The render() method is required, and is the method that actually outputs the HTML to the DOM.

### componentDidMount

- The componentDidMount() method is called after the component is rendered.
- This is where you run statements that requires that the component is already placed in the DOM.

```

import React from "react";

class LifecycleDemo extends React.Component {
  constructor(props) {
    super(props);
    this.state = { favoriteColor: "red" };
    console.log("1. constructor - State initialized");
  }

  static getDerivedStateFromProps(props, state) {
    console.log("2. getDerivedStateFromProps - Sync props to state if needed");
    return null; // usually used to update state from props
  }

  render() {
    console.log("3. render - Returning JSX");
    return (
      <div>
        <h1>My Favorite Color is {this.state.favoriteColor}</h1>
      </div>
    );
  }

  componentDidMount() {
    console.log("4. componentDidMount - Component mounted, good for API calls");
    // Example API call or timer
    setTimeout(() => {
      this.setState({ favoriteColor: "blue" });
    }, 2000);
  }
}

export default LifecycleDemo;

```

## Updating

- The next phase in the lifecycle is when a component is updated.A component is updated whenever there is a change in the component's state or props

React has five built-in methods that gets called, in this order, when updating a component:

- **getDerivedStateFromProps()**
- **shouldComponentUpdate()**
- **render()**
- **getSnapshotBeforeUpdate()**
- **componentDidUpdate()**

## getDerivedStateFromProps

- Also at updates the getDerivedStateFromProps method is called. This is the first method that is called when a component gets updated.
- This is still the natural place to set the state object based on the initial props.

## shouldComponentUpdate

- In the shouldComponentUpdate() method you can return a Boolean value that specifies whether React should continue with the rendering or not.The default value is true.

## render

- The render() method is of course called when a component gets updated, it has to re-render the HTML to the DOM, with the new changes.

## getSnapshotBeforeUpdate

- In the getSnapshotBeforeUpdate() method you have access to the props and state before the update, meaning that even after the update, you can check what the values were before the update.
- If the getSnapshotBeforeUpdate() method is present, you should also include the componentDidUpdate() method, otherwise you will get an error.

## componentDidUpdate

- The componentDidUpdate method is called after the component is updated in the DOM.

```

import React from "react";

class UpdatingDemo extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0,
    };
    console.log("Constructor");
  }

  static getDerivedStateFromProps(props, state) {
    console.log("1. getDerivedStateFromProps");
    return null; // rarely used to update state from props
  }

  shouldComponentUpdate(nextProps, nextState) {
    console.log("2. shouldComponentUpdate");
    return true; // returning true allows update
  }

  getSnapshotBeforeUpdate(prevProps, prevState) {
    console.log("3. getSnapshotBeforeUpdate");
    return null; // you can return scroll position or DOM info
  }

  componentDidUpdate(prevProps, prevState, snapshot) {
    console.log("4. componentDidUpdate");
    console.log("Previous State:", prevState.count);
    console.log("Current State:", this.state.count);
  }

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    console.log("Rendering...");
    return (
      <div>
        <h1>Count: {this.state.count}</h1>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}

export default UpdatingDemo;

```

## unmounting

It is when a component is removed from the DOM 

React has only one built-in method that gets called when a component is unmounted:

### componentWillUnmount()

- The componentWillUnmount method is called when the component is about to be removed from the DOM.

```

import React from "react";

class LifecycleDemo extends React.Component {
  constructor() {
    super();
    this.state = {
      count: 0,
      show: true,
    };
  }

  componentDidMount() {
    console.log("ComponentDidMount: Mounted");

    // Adding an event listener
    window.addEventListener("keydown", this.handleKeyPress);
  }

  componentDidUpdate(prevProps, prevState) {
    if (prevState.count !== this.state.count) {
      console.log("ComponentDidUpdate: Count changed");
    }
  }

  componentWillUnmount() {
    console.log("ComponentWillUnmount: Cleaning up");

    // Important: Removing the event listener
    window.removeEventListener("keydown", this.handleKeyPress);
  }

  handleKeyPress = (event) => {
    if (event.key === "ArrowUp") {
      this.setState((prevState) => ({
        count: prevState.count + 1,
      }));
    }
  };

  toggleComponent = () => {
    this.setState((prevState) => ({
      show: !prevState.show,
    }));
  };

  render() {
    if (!this.state.show) return null;

    return (
      <div>
        <h2>Lifecycle with Event Listener</h2>
        <p>Press ↑ Arrow to increase count</p>
        <p>Count: {this.state.count}</p>
        <button onClick={this.toggleComponent}>Unmount Component</button>
      </div>
    );
  }
}

export default LifecycleDemo;

```


