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


