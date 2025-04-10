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

