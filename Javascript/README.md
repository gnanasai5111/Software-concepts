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

## Shadowing 

- Shadowing happens when a variable in a local scope (block/function) has the same name as a variable in an outer scope. The inner variable "shadows" or overrides access to the outer one within its scope.

## Closures

- A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment).In other words, a closure gives a function access to its outer scope.

```

function init() {
  var name = "Mozilla"; // name is a local variable created by init
  function displayName() {
    // displayName() is the inner function, that forms a closure
    console.log(name); // use variable declared in the parent function
  }
  displayName();
}
init();

```

## Functions

### Function Statement or Function Declaration

```
function fn(){
}
```

### Function Expression
 
```
let fn=function(){
}
```

### Named Function Expression

```
let fn=function name(){
}
```

### Parameters and Arguments

```
function sum(a,b){  - Parameters
}
sum(2,3); - Arguments(Actual values)
```

### Anonymous Functions
- function without a name

```
function(){
}
```

### Arrow Functions
- Shorter syntax

```
var a =()=>{
}
```

### First class Functions

- The ability to use functions as values(first class citizens). We can assign a function to a variable, pass function as an argument and also can return an function.

```

let greet = function(name) {
  return `Hello, ${name}!`;
};

function callFunction(fn, name) {
  return fn(name);
}

console.log(callFunction(greet, 'Alice'));  // Outputs: Hello, Alice!

```

### Higher Order Functions

- It is a function that either takes one or more functions as arguments and returns a function as a result.

```

// Higher-order function that takes a function as an argument
function applyOperation(fn, num) {
  return fn(num);
}

let square = function(x) {
  return x * x;
};

console.log(applyOperation(square, 4));  // Outputs: 16

```

### Callback functions

- A function that is passed as an argument to another function, and is called later inside that function.
- Callbacks are used to perform asynchronous operations

```
setTimeout(()=>{
  console.log("running")
},(2000));

```

## Array Methods

- **map** : Transforms each element in an array and returns a new array with the modified values.
- **filter** : Returns a new array with elements that pass a specified condition (test).
- **reduce** : Reduces the array to a single value by applying an operation  across elements.
- **every** : Returns true if all elements pass the given condition; otherwise, returns false.
- **some** : Returns true if at least one element passes the condition; otherwise, returns false.
- **find** : Returns the first element that satisfies the condition, or undefined if none do.
- **findIndex** - Returns the index of the matching element instead of the element itself.
- **flatMap** - returns a new array formed by applying a given callback function to each element of the array, and then flattening the result by one level.

```

// map()
const nums = [1, 2, 3];
const doubled = nums.map(n => n * 2); 
console.log(doubled); // [2, 4, 6]

// filter()
const numbers = [1, 2, 3, 4];
const even = numbers.filter(n => n % 2 === 0); 
console.log(even); // [2, 4]

// reduce()
const arr = [1, 2, 3, 4];
const sum = arr.reduce((acc, curr) => acc + curr, 0); 
console.log(sum); // 10

// every()
const list = [2, 4, 6];
const allEven = list.every(n => n % 2 === 0); 
console.log(allEven); // true

// some()
const mixed = [1, 3, 4];
const hasEven = mixed.some(n => n % 2 === 0); 
console.log(hasEven); // true

// find()

const arr = [5, 10, 15];
const found = arr.find(n => n > 7); // 10

// findIndex()

const arr = [10, 20, 30];
const index = arr.findIndex(n => n === 20); // 1

// flatMap()

const arr1 = [1, 2, 1];

const result = arr1.flatMap((num) => (num === 2 ? [2, 2] : 1)); //  [1, 2, 2, 1]


```

## Javascript Runtime environment

- A JavaScript runtime environment is the platform that provides the necessary tools and libraries to execute JavaScript code.
- It includes JS Engine, Call Stack,Event Loop,Callback Queue (Macrotask Queue),Microtask Queue,Memory heap, Web apis and storage apis.

### JavaScript Engine Architecture (e.g., V8)

- It Parses, compiles, and executes JS code.
- Parser: Converts code to AST (Abstract Syntax Tree).
- Interpreter :  It translates the source code into machine code line-by-line.
- Compiler : It translates the entire source code of a program into machine code.
- JIT (Just in time compilation) -  JIT is a hybrid approach that combines both compilation and interpretation. It compiles code just before or while the program is running, rather than ahead of time.  The JavaScript engine first interprets the code to start execution quickly. As the program runs, it identifies frequently executed parts of the code (called "hot spots") and compiles them into optimized machine code. This compiled code can then be reused, making future executions of those parts faster.
- Profiler: Detects which parts of code are used often.

### Memory Heap

- The area where objects and functions are stored dynamically. JS allocates memory here during execution.

### Garbage Collector

- Automatically frees memory no longer used. Most JS engines use the Mark-and-Sweep algorithm.

### Mark-and-Sweep Algorithm

- Mark: Start from root and mark all reachable memory.
- Sweep: Clean up all unmarked (unreachable) memory.

### Event Loop

- JavaScript operates in a single-threaded environment, meaning only one piece of code runs at a time. The event loop ensures that tasks are executed in the correct order, enabling asynchronous programming and keeping the main thread non-blocking.
- It monitors the Call Stack, Microtask Queue, and Callback (Macrotask) Queue.

**Workflow** :
- Executes all synchrounous code (Call Stack).
- Executes all tasks from the Microtask Queue(higher priority).
- Executes one task at a time from the Callback (Macrotask) Queue per cycle

### Microtask and callback Queue

- Microtask queue stores higher priority tasks like Promises, mutation observer
- Callback queue stores tasks like setTimeout, Dom apis.

## Callbacks

- Callback: A function that is passed as an argument to another function, and is called later inside that function.
- Callback Hell:	Deep nesting of callbacks that leads to unreadable, unmaintainable and error prone code.
- Inversion of Control:	Loss of control when you hand over your function to someone else's function.

## Promises
- A Promise is an object that represents the eventual completion (or failure) of an asynchronous operation.

**States of a Promise**
- Pending
- Fulfilled
- Rejected

```

const promise = new Promise((resolve, reject) => {
  if (/* success */) {
    resolve(result);
  } else {
    reject(error);
  }
});

promise
  .then((result) => {
    // success
  })
  .catch((error) => {
    // error
  })
  .finally(() => {
    // always runs
  });

```

- Promise.resolve() creates a resolved (fulfilled) promise, meaning it’s already in the fulfilled state and its value is passed directly.
- Promise.reject() creates a rejected promise, meaning it’s already in the rejected state and its reason (error) is provided directly.

```

const resolvedPromise = Promise.resolve("Task completed");

resolvedPromise.then((value) => {
  console.log(value); // "Task completed"
});

const rejectedPromise = Promise.reject("Something went wrong");

rejectedPromise.catch((error) => {
  console.log(error); // "Something went wrong"
});

```

## Promise.all()

- Waits for all promises to resolve. Returns an array of resolved values in order of the input promises. If any promise rejects, the entire operation fails and goes to .catch()

## Promise.allSettled()

- Waits for all promises to settle (either resolve or reject). Never fails early.Returns an array of objects with status and values.

## Promise.race()

- Settles as soon as the first promise settles (fulfilled or rejected).Returns the value or error from that first settled promise.

## Promise.any()

- Returns the first fulfilled promise.Ignores rejected promises.If all promises reject, it throws an AggregateError.

```

1. Promise.all()

const p1 = Promise.resolve(1);
const p2 = Promise.resolve(2);
const p3 = Promise.resolve(3);

Promise.all([p1, p2, p3])
  .then((values) => console.log("All resolved:", values)) // [1, 2, 3]
  .catch((err) => console.error("Error:", err));

With one rejection:

const p1 = Promise.resolve(1);
const p2 = Promise.reject("Failed!");
const p3 = Promise.resolve(3);

Promise.all([p1, p2, p3])
  .then((values) => console.log(values))
  .catch((err) => console.error("Error:", err)); // Error: Failed!


2. Promise.allSettled()

const p1 = Promise.resolve("Success");
const p2 = Promise.reject("Oops");
const p3 = Promise.resolve("Done");

Promise.allSettled([p1, p2, p3])
  .then((results) => console.log(results));

Output:

[
  { status: 'fulfilled', value: 'Success' },
  { status: 'rejected', reason: 'Oops' },
  { status: 'fulfilled', value: 'Done' }
]

3. Promise.race()

const p1 = new Promise((res) => setTimeout(() => res("First"), 100));
const p2 = new Promise((res) => setTimeout(() => res("Second"), 200));

Promise.race([p1, p2])
  .then((value) => console.log("Winner:", value)); // Winner: First

With one rejecting first:

const p1 = new Promise((_, rej) => setTimeout(() => rej("Failed early"), 50));
const p2 = new Promise((res) => setTimeout(() => res("Slow success"), 100));

Promise.race([p1, p2])
  .then((val) => console.log(val))
  .catch((err) => console.error("Error:", err)); // Error: Failed early

4. Promise.any()

const p1 = Promise.reject("Error 1");
const p2 = Promise.resolve("Success");
const p3 = Promise.resolve("Another Success");

Promise.any([p1, p2, p3])
  .then((result) => console.log("First fulfilled:", result)) // First fulfilled: Success
  .catch((err) => console.error("All failed:", err));

With all rejected:

const p1 = Promise.reject("Error 1");
const p2 = Promise.reject("Error 2");

Promise.any([p1, p2])
  .then((val) => console.log(val))
  .catch((err) => {
    console.error("All promises failed");
    console.error(err.errors); // ["Error 1", "Error 2"]
  });


```

## Async/Await

- async/await is syntactic sugar over Promises that makes asynchronous code look and behave like synchronous code.
- Async is a keyword that is used before function.
- Async function always returns an Promise.
- Await can only be used inside an async function
- Await pauses execution until the Promise settles (fulfilled or rejected) and returns the resolved value or throws if rejected

```

async function riskyOperation() {
  try {
    const data = await someFailingPromise();
    console.log(data);
    return data;
  } catch (error) {
    console.error("Error caught:", error.message);
    return err;
  }
}
riskyOperation().then((data)=>{}).catch((err)=>{})

```

## Call, Apply , Bind

- They are used to change the value of this inside a function
  
- **call** -  Calls the function right away with a given this and arguments one by one.
- **apply** - Works just like call() but takes arguments in an array.
- **bind** - Doesn't call the function immediately, it returns a new function and you can call it later.

```

function greet(msg) {
  console.log(msg + ", " + this.name);
}

const user = { name: "John" };
greet.call(user, "Hello"); // Hello, John
greet.apply(user, ["Hi"]); // Hi, John
const sayHi = greet.bind(user, "Hey");
sayHi(); // Hey, John


```

## Polyfill for bind,call,apply 

- Polyfill is browser fallback. It means we write own implementation for that

**Bind Polyfill**

```

const obj={
firstName:"Gnana",
lastName:"sai"
}

const getName=function(city,age){

console.log(this.firstName+" "+this.lastName+" from "+ city +" of age "+age)
}


let fn=getName.bind(obj,"hyderabad");
fn(26)

Function.prototype.myBind=function(...args){
let fn=this;
let params=args.slice(1)
return function(...args2){
fn.apply(args[0],[...params,...args2])
}
}

let fn2=getName.myBind(obj,"hyderbad")
fn2(26)

```
**Polyfill for bind without call and apply**

```

const obj={
firstName:"Gnana",
lastName:"sai"
}

const getName=function(city,age){

console.log(this.firstName+" "+this.lastName+" from "+ city +" of age "+age)
}


let fn=getName.bind(obj,"hyderabad");
fn(26)

Function.prototype.myBind=function(...args){
let fn=this;
let params=args.slice(1)
let obj=args[0];
console.log(fn,args[0])
return function(...args2){
obj.fns=fn;
obj.fns(...[...params,...args2])
}
}

let fn2=getName.myBind(obj,"hyderbad")
fn2(26)

```

**Apply Polyfill**

```

const obj ={
name:"gnanasai",
city:"hyderabad"}

function sayIntro (company,place){
console.log(`name is ${this.name}, place is ${this.city} and company is ${company} and work place is ${place} `)
}

Function.prototype.myApply= function (context,args){
context.fnc = this;
context.fnc(...args);
}
sayIntro.myApply(obj,["safearth","banglore"])

```

**Call Polyfill**

```

const obj ={
name:"gnanasai",
city:"hyderabad"}

function sayIntro (company,place){
console.log(`name is ${this.name}, place is ${this.city} and company is ${company} and work place is ${place} `)
}

Function.prototype.myCall= function (context,...args){
context.fnc = this;
context.fnc(...args);
}
sayIntro.myCall(obj,"safearth","banglore")

```

## Spread and Rest

- **Spread** - Used to spread elements from an array or object.
- **Rest** - Collects things together

```
// Spread

// In arrays
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5];

console.log(arr2);

// In objects
const person = { name: "Gnana", age: 25 };
const updatedPerson = { ...person, city: "Hyderabad" };

console.log(updatedPerson); 
// { name: "Gnana", age: 25, city: "Hyderabad" }

// In Functions

const nums = [1, 2, 3];
console.log(Math.max(...nums)); // 3 (equivalent to Math.max(1, 2, 3))

// Rest

// In Arrays

const arr = [1, 2, 3, 4];
const [first, second, ...rest] = arr;

console.log(first);  // 1
console.log(second); // 2
console.log(rest);   // [3, 4]

// In Objects

const user = { name: "Gnana", age: 25, city: "Hyderabad" };
const { name, ...rest } = user;

console.log(name);   // "Gnana"
console.log(rest);   // { age: 25, city: "Hyderabad" }

// In Functions

function sum(...numbers) {
  return numbers.reduce((a, b) => a + b, 0);
}

console.log(sum(1, 2, 3, 4)); // 10

```

// Function Currying

- It converts a function with multiple parameters into a sequence of functions.
- Each function takes a single argument and returns another function until all arguments are received.

```

// Normal Function
// function add(a, b) {
//     return a + b;
// }
// console.log(add(2, 3)); 

// Function Currying
function add(a) {
    return function(b) {
        return a + b;
    }
}

const addTwo = add(5);  // First function call with 5
console.log(addTwo(4));

```

## Async and defer in script tag

- **Without async/defer** : HTML parsing is blocked immediately when the script is encountered, until it’s loaded and executed.
- **async** : Script is loaded in the background. When it’s ready, HTML parsing is paused and the script executes immediately
- **defer** : Script is loaded in the background, but it waits to execute until after HTML parsing is complete.



