# Typescript

- It is a Typed superset of Javascript
- Compiles down to plain JavaScript
- Code written in .ts files.
- Helps catch errors early (at compile time).

## Basics

```
let a: number = 10;
let b: string = "Hai";
let c: boolean = true;
let d: any = "Could be anything";
```

---

## Arrays

```
let arr: number[] = [1, 2, 3];
let arr1: Array<number> = [1, 2, 3];
let arr: { id: number; name: string }[] = [
  { id: 1, name: 'Alice' },
  { id: 2, name: 'Bob' }
];
let arr1: Array<{ id: number; name: string }> = [
  { id: 1, name: 'Alice' },
  { id: 2, name: 'Bob' }
];
```

---

## Tuples - Fixed length and Mixed Types

```
let arr2: [string, number] = ["Hello", 10];
```

## Objects

```
const person: { name: string; age: number } = {
    name: "Alice",
    age: 30,
};
```

## Union Types

```
let pid: string | number;
pid = 22;
pid = "abc";
```

## Enums

```
enum Direction {
    Up,
    Down,
    Left,
    Right,
}

let move: Direction = Direction.Up;
```

## Type Aliases

```
type User = {
    name: string;
    age?: number; // Optional key
};

let user: User = {
    name: "gnana",
    age: 26,
};
```

### Union with Type Alias

```
type value = string | number;
let val: value = 10;
```

### Intersection with Type Alias

```
type finalVal = { name: string } & { age: number };

let val1: finalVal = {
    name: "sai",
    age: 20,
};
```

## Interfaces

```
interface UserInterface {
    id: number;
    name: string;
    age?: number;
}

let user2: UserInterface = { id: 2, name: "John" };
```

### Extending Interfaces

```ts
interface Animal {
    name: string;
}

interface Dog extends Animal {
    breed: string;
}

const dog: Dog = {
    name: "Rocky",
    breed: "Golden Retriever",
};
```

- Interfaces can be extended (better for OOP).
- Types are more flexible (can use unions, intersections).



## Functions

```
const add = (a: number, b: number): number => {
    return a + b;
};
```

### Using Type Alias for Function

```
type AddFunction = (a: number, b: number) => number;

const add2: AddFunction = (a, b) => {
    return a + b;
};
```

### Using Interface for Function

```
interface Add {
    (a: number, b: number): number;
}

const add3: Add = (a, b) => {
    return a + b;
};
```

### Default + Optional Parameters

```
function greet(name: string = "sai", age?: number): void {
    console.log(`Hello ${name}`);
}
```

## Type Assertions

```
let n: any = 10;
let id = n as number;

// or (alternate syntax)
let id1 = <number>n;
```
- **Tell the compiler:** "Trust me, I know what I’m doing."

## Classes

```
class Person {
    id: number;
    name: string;

    constructor(id: number, name: string) {
        this.id = id;
        this.name = name;
    }

    register() {
        return `${this.name} is registered`;
    }
}

const alice = new Person(1, "Alice");
```
## Generics

### Basic Generic Function

```
function identity<T>(val: T): T {
    return val;
}

const output1 = identity<number>(123);
const output2 = identity<string>("Hello");
const output3 = identity(true); // TypeScript infers boolean
```

### Generics with Arrays

```
function getFirstElement<T>(arr: T[]): T {
    return arr[0];
}

const firstNum = getFirstElement([1, 2, 3]);
```

### Generic Type Alias

```
type IdentityFunc<T> = (arg: T) => T;

const myIdentity: IdentityFunc<number> = (arg) => arg;
```

###  Interface for generic function:

```
interface IdentityFn<T> {
  (value: T): T;
}

const identity: IdentityFn<number> = (value) => {
  return value;
};

console.log(identity(5)); 
```

### Generics in Interfaces

```
interface ApiResponse<T> {
    data: T;
    status: number;
}

const userResponse: ApiResponse<{ name: string; age: number }> = {
    data: { name: "Alice", age: 25 },
    status: 200,
};
```

### Generics in Classes

```
class Box<T> {
    content: T;

    constructor(content: T) {
        this.content = content;
    }

    getContent(): T {
        return this.content;
    }
}

const stringBox = new Box<string>("Hello");
const numberBox = new Box<number>(123);
```

### Multiple Type Parameters

```
function merge<T, U>(obj1: T, obj2: U): T & U {
    return { ...obj1, ...obj2 };
}

const merged = merge({ name: "Alice" }, { age: 25 });
```

### Setting Default Type

```
function wrapInArray<T = string>(value?: T): T[] {
    return value !== undefined ? [value] : ["" as any];
}

const arr5 = wrapInArray(10);       // number[]
const arr6 = wrapInArray("hello");  // string[]
const arr7 = wrapInArray();         // string[]
```

## Utility Types

### `Partial<Type>`

```
interface User1 {
    id: number;
    name: string;
}

type PartialUser = Partial<User1>;
// { id?: number; name?: string }
```

---

### `Required<Type>`

```
interface Profile {
    username?: string;
    email?: string;
}

type CompleteProfile = Required<Profile>;
// { username: string; email: string }
```

---

### `Readonly<Type>`

```
interface Settings {
    theme: string;
}

const appSettings: Readonly<Settings> = {
    theme: "dark",
};

// appSettings.theme = "light"; // ❌ Error
```

### `Record<Keys, Type>`

```
type Roles = "admin" | "user" | "guest";

const permissions: Record<Roles, boolean> = {
    admin: true,
    user: true,
    guest: false,
};
```

### `Pick<Type, Keys>`

```
interface Product {
    id: number;
    name: string;
    price: number;
}

type ProductPreview = Pick<Product, "id" | "name">;
// { id: number; name: string }
```

### `Omit<Type, Keys>`

```
type ProductWithoutPrice = Omit<Product, "price">;
// { id: number; name: string }
```

### `ReturnType<FunctionType>`

```
function fetchData() {
    return { id: 1, name: "test" };
}

type FetchDataReturn = ReturnType<typeof fetchData>;
// { id: number; name: string }
```

---

## 🎯 Extra Utilities You Should Know

### `keyof` Operator

```
interface Car {
    brand: string;
    model: string;
}

type CarKeys = keyof Car;
// "brand" | "model"
```

### `typeof` Operator

```
const myVar = { id: 1, name: "Test" };

type MyVarType = typeof myVar;
// { id: number; name: string }
```


### Special Types: `never` and `unknown`

```
// never -> a type that never occurs
// Because it throws an error or infinite loops or crashes the program.
function throwError(): never {
    throw new Error("Something went wrong");
}

// unknown -> safer alternative to any
// You can't directly use unknown without checking its type 
let u: unknown = 1;
u = "hello";

if (typeof u === "string") {
    console.log(u.toUpperCase());
}
```

---

