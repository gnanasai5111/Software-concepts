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

## this keyword

- this keyword refers to an object.
- Alone, this refers to the global object.
- In an object method, this refers to the object.
- In a function, this refers to the global object. In strict Mode , this refers to undefined.
- Arrow functions do NOT have their own this. They inherit it from the surrounding (lexical) scope.
- In an event, this refers to the element that received the event.
- Methods like call(), apply(), and bind() can refer this to any object.

## Scope

- Scope determines accessibility of variables in different parts of the code.
- **Global Scope** : Variables declared outside any function/block. Accessible everywhere.
- **Function Scope** : Variables declared inside a function. Accessible only within that function.
- **Block Scope** : Introduced with let and const. Variables inside {} (if/else, loops, etc.) are accessible only inside that block.

## Scope Chain 

- When accessing a variable, JavaScript searches in the current scope.
- If not found, moves upward to the parent scope.
- Continues until it reaches the global scope.
- This chain of scopes is called the Scope Chain.

## Lexical Environment

- A lexical environment in JavaScript is a data structure that stores variables and functions defined in the current scope, along with references to all outer scopes. It is also known as the lexical scope.
- The lexical environment is created when a function is defined and persists as long as the function or any of its closures remain accessible.

## var, let, const

- **var** - Function Scope. They can be redeclared and reassigned.  Hoisted and initialized as undefined
- **let** - Block Scope. They can not be redeclared but can be reassigned. Hoisted, but exists in the Temporal Dead Zone (TDZ) until initialized.
- **const** - Block Scope. They can not be redeclared and cannot be reassigned. Hoisted, but exists in the Temporal Dead Zone (TDZ) until initialized.

## Error Types

- Syntax Error happens when you break js grammar rules.
- Type Error happens when an operation is performed on a value of the wrong type.
- Reference Error happens when trying to access a variable that doesn’t exist in the scope.

```

// 🧨 1. SyntaxError Example
// This will throw a SyntaxError because of the missing closing bracket
try {
  eval("let a = 10 console.log(a"); 
} catch (e) {
  console.error("SyntaxError:", e.message);
}

// 🧨 2. TypeError Example
// Trying to call a number like a function will throw a TypeError
try {
  let num = 5;
  num(); // num is not a function
} catch (e) {
  console.error("TypeError:", e.message);
}

// 🧨 3. ReferenceError Example
// Accessing an undeclared variable throws a ReferenceError
try {
  console.log(notDeclaredVar);
} catch (e) {
  console.error("ReferenceError:", e.message);
}

```




