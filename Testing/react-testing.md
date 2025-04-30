### JEST
- It is a Javascript testing Framework. It is a test runner that finds the tests, runs the tests, determine whether the tests passed or failed and reports it back in a humam readable manner.

### React Testing Library
- It is a Javascript testing utility that provides virtual Dom to test react applications.

## Types of testing
1. **Unit Testing** : Testing individual units (functions/components) in isolation.
2. **Integration Testing** : Testing how multiple units/components work together.
3. **End-End Testing**: Testing the entire app as a user from the UI perspective.

## test or it
- The test method is used to define and run a unit test.

Syntax: **test(name,fn,timeout)**
 
1. First argument is Test name and it is  used to identify the test.
2. Second argument is function that contains expectations of the test.
3. Third argument is timeout which is optional argument for specifying how long to wait before aborting the test.Default timeout is 5 second.

## render
- This function is used to render your component into the virtual DOM so that you can interact with it in your tests. It comes from the React Testing Library.

## screen
- screen is an object that provides access to queries used to interact with the rendered output or virtual dom properties. It comes from the React Testing Library.

## expect
- expect is used for making assertions in your tests. It's part of Jest and allows you to check if something is true, false, or matches specific values.

```
import { render, screen } from '@testing-library/react';
import MyComponent from './MyComponent';

test('displays the correct button label', () => {
  render(<MyComponent />);
  const button = screen.getByRole('button', { name: /submit/i });
  expect(button).toBeInTheDocument();
});
```

## Test Driven development (TDD)
- It is a software development process where you write tests before writing the software code

## Describe (Grouping Tests)
- describe is a Jest function used to group related tests together.

Syntax: **describe(name,fn)**

```
describe('ComponentName', () => {
  test('should do something', () => {
    // test logic
  });

  test('should do another thing', () => {
    // test logic
  });
});
```

## Filtering Tests
- Use .only to run a specific test
- Use .skip to skip a specific test

Syntax : test.only() , describe.only() , test.skip() ,describe.skip()

## File Naming conventions

- ComponentName.test.tsx
- ComponentName.spec.tsx
- Folder named __tests__ and having tsx files .

## Coverage
- Its a metric that helps you understand how much of your software code is tested

Syntax : Inside package.json, in scripts , **"coverage":"npm test --coverage --watchAll"**

## Assertions
- An assertion is a statement that verifies if a specific condition is true. If it's false, the test fails. In Jest, assertions are made using expect().

```
syntax: expect(actual).toBe(expected);
ex: expect(1 + 1).toBe(2);
```
## Matcher Function
- A matcher is a function chained to expect() that defines how the actual value should be compared to the expected value.

Jest provides many built-in matchers.

Primitive Matchers
- toBe(value) : Exact equality (===)  ex: expect(5).toBe(5)
- toEqual(value) : Deep equality (use for objects/arrays) ex:  expect({ a: 1 }).toEqual({ a: 1 }
- toBeGreaterThan(number) :  Checks if value is greater than given number ex:  expect(10).toBeGreaterThan(5)

Dom Matchers(jest-dom)
- toBeInTheDocument() : Checks if the element is present in the DOM ex: expect(screen.getByText(/hello/i)).toBeInTheDocument()
- toBeVisible(): Checks if the element is visible (not display: none, etc.) ex:expect(button).toBeVisible()
- toBeDisabled():  Checks if a form control is disabled or not ex:expect(input).toBeDisabled()

## React Testing Library (RTL) Queries
- They are used to find elements in the component

To find single element on page we have ,
- getBy... - throws error if not found (synchronous
- queryBy... - returns null if not found (synchronous)
- findBy... -  waits for element (asynchronous)

To find Multiple elements on page we have ,
- getAllBy... - throws error if none found
- queryAllBy... -  returns empty array if none found
- findAllBy... - waits for all matching elements

suffix can be

- **getByRole()** - Most recommended – selects elements by ARIA role (like button, textbox). It also Supports options for matching by name, checked, disabled, etc.
```
// Match a button by role and name
const button = screen.getByRole('button', { name: submit });

// Match a checkbox
const checkbox = screen.getByRole('checkbox', { name: accept terms });

// Match a heading (h1)
const heading = screen.getByRole('heading', { level: 1 });

// The option name is used when matching an element by its visible accessible name, such as the label or inner text of an element.
```

- **getByLabelText()** - Selects input elements by their associated label text.
```
const input = screen.getByLabelText('Email');
```
- **getByPlaceholderText()** - Selects input by its placeholder value
```
const input = screen.getByPlaceholderText('Enter email');
```
- **getByText()** - 	Selects element by its visible text
```
const heading = screen.getByText('Welcome!');
```
- **getByDisplayValue()** - Selects input elements by the value they're displaying
```
const input = screen.getByDisplayValue('John Doe');
```
- **getByAltText()** - Selects elements (typically images) by their alt attribute.
```
const logo = screen.getByAltText('Company Logo');
```
- **getByTitle()** - Selects elements by their title attribute.
```
const closeButton = screen.getByTitle('Close');
```
- **getByTestId()** - Selects elements by their data-testid attribute.
```
const button = screen.getByTestId('submit-button');
```

## User Interactions in React Testing Library

-  **@testing-library/user-event** :  A utility to simulate realistic user interactions .

```
import React, { useState } from 'react';

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>Counter: {count}</h1>
      <button onClick={() => setCount((prev) => prev + 1)}>Increment</button>
      <button onClick={() => setCount((prev) => prev - 1)}>Decrement</button>
      <button onClick={() => setCount(0)}>Reset</button>
    </div>
  );
}


import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import Counter from './Counter';

test('increments, decrements, and resets the counter', async () => {
  const user = userEvent.setup();  // It creates the user Instance
  render(<Counter />);

  // Check initial state
  expect(screen.getByText(/counter: 0/i)).toBeInTheDocument();

  // Increment
  await user.click(screen.getByRole('button', { name: /increment/i }));
  expect(screen.getByText(/counter: 1/i)).toBeInTheDocument();

  // Decrement
  await user.click(screen.getByRole('button', { name: /decrement/i }));
  expect(screen.getByText(/counter: 0/i)).toBeInTheDocument();

  // Reset
  await user.click(screen.getByRole('button', { name: /reset/i }));
  expect(screen.getByText(/counter: 0/i)).toBeInTheDocument();
});

```

- **Mouse Interactions** : click(),dblClick(),tripleClick(),hover(),unhover()
- **Keyboard Interactions** : type(),tab(),keyboard()

## Testing Providers

- Sometimes your components depend on context providers (like Redux, Theme, Router, etc.). In such cases, you need to wrap them during testing.

```
render(<Component />, { wrapper: ProviderWrapper });
```

## Testing CustomHooks

- For Testing custom hooks we use renderHook()
- Use act() when testing state updates inside hooks.

```
import { renderHook, act } from '@testing-library/react';
import { useCounter } from './useCounter';

test('should increment counter', () => {
  const { result } = renderHook(() => useCounter());

  act(() => {
    result.current.increment();
  });

  expect(result.current.count).toBe(1);
});
```


