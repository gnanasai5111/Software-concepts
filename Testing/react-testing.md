### JEST
- It is a Javascript testing Framework. It is a test runner that finds the tests, runs the tests, determine whether the tests passed or failed and reports it back in a humam readable manner.

### React Testing Library
- It is a Javascript testing utility that provides virtual Dom to test react applications.

## Types of testing
1. **Unit Testing** : Testing individual units (functions/components) in isolation.
2. **Integration Testing** : Testing how multiple units/components work together.
3. **End-End Testing**: Testing the entire app as a user from the UI perspective.

## test
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


