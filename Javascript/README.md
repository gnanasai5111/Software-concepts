# JAVASCRIPT

##  JavaScript Execution Context 

- In JavaScript, everything happens inside an Execution Context.
- Each Execution Context consists of two main components:
  
  ### 1. Memory Component (also called Variable Environment)
  - Stores variables and functions in key-value pairs.
  - It is created during the Creation Phase, before any code is executed.
  - Variables are initially assigned the value undefined.
  - Functions are stored as full function definitions. 
  
  ### 2. Code Component (also called Thread of Execution)
  - Responsible for executing the code line by line, during the Execution Phase.

- JavaScript is a synchronous, single-threaded language:
  - Single-threaded means it can execute one command at a time.
  - Synchronous means it runs in a top-to-bottom, step-by-step manner unless asynchronous behavior is introduced (e.g., via callbacks, promises, async/await).

- Types of Execution Context:
  - **Global Execution Context (GEC)**: Created by default; one per JS program.
  - **Function Execution Context (FEC)**: Created every time a function is invoked.
  - **Eval Execution Context**: Created when `eval()` is used (rare and discouraged).

- The Global Execution Context is the default context where your JS code starts running.

## Call Stack (a.k.a Execution Stack)

- The Call Stack is a stack-based data structure (LIFO - Last In, First Out).
- It manages the execution of multiple functions.
- The Global Execution Context is pushed first.
- When a function is called, a new Execution Context is pushed onto the stack.
- When the function returns, its context is popped off.

## Hoisting 

Hoisting is JavaScript's default behavior of moving declarations to the top of the current execution context (memory phase) before the code is executed.

- var is hoisted and initialized as undefined. You can access it before its declaration, but the value will be undefined 
- let and const are hoisted  but not initialised. They are in temporal deadzone untill they are defined. Accessing them before that causes a ReferenceError
- Function Declarations (like function foo() {}) are hoisted. For Function Expressions (like const foo = function () {} or arrow functions), only variables are hoisted

## Undefined vs Not Defined

- Undefined means variable exists in memory, but has no value yet. Accessing it gives undefined.
- Not defined means variable has never been declared. Accessing it gives Reference error as variable doesnt exist in memory.

