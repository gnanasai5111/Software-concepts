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
