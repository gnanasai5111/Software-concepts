### Hooks
- Hooks are special functions in React that let you use state, lifecycle, context, refs, and more React features in functional components.

## useState
- useState is a Hook that lets you add state to functional components.
- It returns a pair: the current state value and a function to update it.
- Updating the state causes the component to re-render.

```

import { useState } from 'react';
function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>Count: {count}</button>;
}

setCount(count + 1)	Use only when you're not depending on previous state
setCount(prev => prev + 1)	Use when the new state depends on previous state

```

## useEffect 
- `useEffect` is a Hook that lets you perform side effects in function components.
- Common uses: data fetching, setting up subscriptions, accessing the DOM, etc.
- It runs after the dom is rendered.
- You can optionally return a function to clean up (runs on unmount or before the effect re-runs).
- It also accepts an array of dependencies: if any dependency changes, the effect re-runs.

```

import { useEffect } from 'react';

function Timer() {
  useEffect(() => {
    // Start a timer on mount
    const interval = setInterval(() => {
      console.log('Tick');
    }, 1000);

    // Cleanup function: clears interval on unmount or before the effect re-runs
    return () => {
      clearInterval(interval);  // Stop the timer
      console.log('Cleaned up');
    };
  }, []);  // Empty array: Effect runs only once after initial render

  return <p>Open the console to see the timer ticking.</p>;
}

```

## useContext 

- React Context is a way to manage state globally.
- When you have deeply nested components that require access to the same data, instead of passing data via props (called prop drilling), Context API can be used to share the data directly with components that need it.
- Create a Context: Using React.createContext() to create a context object that holds the value you want to share globally.
- Context Provider: Wrap the components where you want to provide access to the context value using the Context.Provider. This allows you to specify a value for that context.
- Consume Context:Use useContext to access the context value in child components.r.

```

import React, { useState, useContext } from 'react';

// Create a Context
const ThemeContext = React.createContext(); // here you can also provide default value

// Create a provider component
function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');
  
  const toggleTheme = () => {
    setTheme((prevTheme) => (prevTheme === 'light' ? 'dark' : 'light'));
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

// A component that consumes the context
function ThemedButton() {
  const { theme, toggleTheme } = useContext(ThemeContext);
  
  return (
    <button
      style={{
        background: theme === 'light' ? 'white' : 'black',
        color: theme === 'light' ? 'black' : 'white',
      }}
      onClick={toggleTheme}
    >
      Switch Theme
    </button>
  );
}

// Main App Component
function App() {
  return (
    <ThemeProvider>
      <ThemedButton />
    </ThemeProvider>
  );
}

export default App;

```

## useReducer

- useReducer is a React hook that is used to manage complex state logic in functional components.

How useReducer Works:

- **Reducer function**: The reducer function takes the current state and an action as arguments and returns a new state. This is where all state transitions occur.

- **Dispatch function**: You use the dispatch function to send actions to the reducer function, which updates the state accordingly.

- **Initial state**: The initial state is provided when calling useReducer.

- Every time an action is dispatched, the component re-renders with the updated state.

```

import React, { useReducer } from 'react';

// Define the initial state
const initialState = { count: 0 };

// Define the reducer function
function counterReducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + action.payload };  // action.payload is used here
    case 'decrement':
      return { count: state.count - action.payload };  // action.payload is used here
    case 'reset':
      return { count: 0 };
    default:
      return state;
  }
}

// The Counter component that uses useReducer
function Counter() {
  // Using useReducer
  const [state, dispatch] = useReducer(counterReducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment', payload: 5 })}>Increment by 5</button>
      <button onClick={() => dispatch({ type: 'decrement', payload: 2 })}>Decrement by 2</button>
      <button onClick={() => dispatch({ type: 'reset' })}>Reset</button>
    </div>
  );
}

export default Counter;

```

## useRef

- Creates a reference to a DOM element or a value.
- Lets you access or update the reference without causing a re-render.
- The reference persists across re-renders

```

import { useRef, useEffect } from 'react';

function MyComponent() {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current.focus(); // Focus input on mount
  }, []);

  return <input ref={inputRef} />;
}

```

## useMemo

- useMemo memoizes a computed value.(It caches the value)
- It only recomputes the value when dependencies change.
- Used to avoid expensive calculations on every render.

```

import { useMemo, useState } from "react";
import "./styles.css";

export default function App() {
  const [number, setNumber] = useState(0);
  const [dark, setDark] = useState(false);

  function slowFunction(number) {
    for (let i = 0; i < 100000; i++) {}
    return number * 2;
  }

  const doubleNumber = useMemo(() => {
    return slowFunction(number);
  }, [number]);

  const themeStyles = useMemo(() => {
    return {
      backgroundColor: dark ? "black" : "white",
      color: dark ? "white" : "black",
    };
  }, [dark]);
  return (
    <div className="App">
      <input
        type="number"
        value={number}
        onChange={(e) => setNumber(e.target.value)}
      />
      <button onClick={() => setDark((prev) => !prev)}>Toggle Theme</button>
      <div style={themeStyles}>{doubleNumber}</div>
    </div>
  );
}

```

## useCallback

- useCallback memoizes a function.(It caches the function)
- It returns the same function instance unless the dependencies change.
- Helps prevent unnecessary re-creations of functions on every render.
- Mostly used to optimize performance, especially when passing functions as props to child components.

```

import { useCallback, useState } from "react";
import List from "./List";
import "./styles.css";

export default function App() {
  const [number, setNumber] = useState(0);
  const [dark, setDark] = useState(false);

  const getItems = useCallback(() => {
    return [number, number + 1, number + 2];
  }, [number]);

  const themeStyles = {
    backgroundColor: dark ? "black" : "white",
    color: dark ? "white" : "black",
  };

  return (
    <div style={themeStyles}>
      <input
        type="number"
        value={number}
        onChange={(e) => setNumber(e.target.value)}
      />
      <button onClick={() => setDark((prev) => !prev)}>Toggle Theme</button>
      <List getItems={getItems} />
    </div>
  );
}

import { useEffect, useState } from "react";

const List = ({ getItems }) => {
  const [items, setItems] = useState([]);

  useEffect(() => {
    setItems(getItems());
  }, [getItems]);

  return items.map((i) => <h1>{i}</h1>);
};

export default List;

```

## useLayoutEffect 

- useLayoutEffect is just like useEffect, **but it runs synchronously after all DOM mutations, before the browser paints the screen.
- It's useful when you need to measure the DOM or make layout changes before the browser paints.

```

import { useLayoutEffect, useEffect, useRef, useState } from "react";

function App() {
  const [show, setShow] = useState(false);
  const popup = useRef();
  const button = useRef();
  useLayoutEffect(() => {
    if (popup.current == null || button.current == null) {
      return;
    }
    const { bottom } = button.current.getBoundingClientRect();
    popup.current.style.top = `${bottom + 25}px`;
  }, [show]);

  return (
    <div>
      <button ref={button} onClick={() => setShow((prev) => !prev)}>
        click
      </button>
      {show && (
        <div style={{ position: "absolute" }} ref={popup}>
          This is Popup
        </div>
      )}
    </div>
  );
}

export default App;

```


