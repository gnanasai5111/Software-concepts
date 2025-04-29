### React with Typescript

## Props Examples

### Basic String Prop

```
type GreetProps = {
  name: string;
};

export const Greet = (props: GreetProps) => {
  return (
    <div>
      <h1>Welcome {props.name}</h1>
    </div>
  );
};
```

### Passing Array of Objects as Props

```
type Item = {
  id: number;
  title: string;
};

type ItemsProps = {
  items: Item[];
};

export const ItemsList = (props: ItemsProps) => {
  return (
    <ul>
      {props.items.map((item) => (
        <li key={item.id}>
          {item.id} - {item.title}
        </li>
      ))}
    </ul>
  );
};
```

**Usage:**

```
<ItemsList
  items={[
    { id: 1, title: 'Apple' },
    { id: 2, title: 'Banana' },
    { id: 3, title: 'Cherry' }
  ]}
/>
```

### Passing Object as Prop

```
type UserProps = {
  user: {
    id: number;
    name: string;
  };
};

export const UserCard = (props: UserProps) => {
  return (
    <div>
      <p>User ID: {props.user.id}</p>
      <p>User Name: {props.user.name}</p>
    </div>
  );
};
```

**Usage:**

```
<UserCard user={{ id: 1, name: 'Alice' }} />
```

### Passing HTML Element via Props

```
type HtmlElementProps = {
  element: JSX.Element;
};

export const HtmlContainer = (props: HtmlElementProps) => {
  return <div>{props.element}</div>;
};
```

**Usage:**

```
<HtmlContainer element={<p>This is a paragraph</p>} />
```

---

### Passing React Element via Props

```
type CustomComponentProps = {
  component: React.ReactNode;
};

// JSX content (<div>Hello</div>)	React.ReactNode
// Component  (<Component />)	React.ComponentType<> - you can add props inside <>

export const ComponentContainer = (props: CustomComponentProps) => {
  return <section>{props.component}</section>;
};
```

**Usage:**

```
<ComponentContainer component={<button>Click Me</button>} />
```


Absolutely! Here's the improved summary — now with the **corresponding input element** shown below each event type:

---

## Event Handler Types in React (TypeScript)

### Click Events

```
React.MouseEvent<HTMLButtonElement>
React.MouseEvent<HTMLDivElement>
```

```
<button onClick={handleClick}>Click</button>
<div onClick={handleClick}>Click Me</div>
```

---

### Input Change (Text, Email, etc.)

```
React.ChangeEvent<HTMLInputElement>
```

```
<input type="text" onChange={handleChange} />
<input type="email" onChange={handleChange} />
```

---

### Checkbox Change

```
React.ChangeEvent<HTMLInputElement> // access `e.target.checked`
```

```
<input type="checkbox" onChange={handleCheckboxChange} />
```

---

### Radio Button Change

```
React.ChangeEvent<HTMLInputElement>
```

```
<input type="radio" name="gender" value="male" onChange={handleRadioChange} />
<input type="radio" name="gender" value="female" onChange={handleRadioChange} />
```

### Select Dropdown

```
React.ChangeEvent<HTMLSelectElement>
```

```
<select onChange={handleSelectChange}>
  <option value="apple">Apple</option>
  <option value="banana">Banana</option>
</select>
```

### Keyboard Events

```
React.KeyboardEvent<HTMLInputElement>
```

```
<input type="text" onKeyDown={handleKeyDown} />
```

---

### Form Submit

```
React.FormEvent<HTMLFormElement>
```

```
<form onSubmit={handleSubmit}>
  <button type="submit">Submit</button>
</form>
```

---

### Focus / Blur Events

```
React.FocusEvent<HTMLInputElement>
```

```
<input type="text" onFocus={handleFocus} onBlur={handleBlur} />
```

### Textarea

```
React.ChangeEvent<HTMLTextAreaElement>
```

```
<textarea onChange={handleTextAreaChange}></textarea>
```

### File Input

```typescript
React.ChangeEvent<HTMLInputElement> // access `e.target.files`
```

```tsx
<input type="file" onChange={handleFileChange} />
```

### CSS styling

```
const divStyle: React.CSSProperties = {
  backgroundColor: 'lightblue',
  padding: '10px',
  borderRadius: '8px'
};
<div style={divStyle}>Styled Div</div>
```

## React Hooks with TypeScript

### 🛠️ useState

```
type User = {
  name: string;
  age: number;
  email: string;
};

const [user, setUser] = useState<User>({
  name: '',
  age: 0,
  email: '',
});
```

```
<button onClick={() => setUser({ name: 'John', age: 30, email: 'john@example.com' })}>
  Set User
</button>
```


### useRef (with input focus)

```
const inputRef = useRef<HTMLInputElement>(null);

const focusInput = () => {
  inputRef.current?.focus();
};
```

```
<input ref={inputRef} type="text" />
<button onClick={focusInput}>Focus Input</button>
```

### useContext (strict context with non-null default)

```
type AuthContextType = {
  user: string;
  login: (name: string) => void;
};

const AuthContext = createContext<AuthContextType | undefined>(undefined);
```

### useReducer (complex form management)

```
type FormState = {
  username: string;
  password: string;
  rememberMe: boolean;
};

type FormAction =
  | { type: 'SET_USERNAME'; payload: string }
  | { type: 'SET_PASSWORD'; payload: string }
  | { type: 'TOGGLE_REMEMBER' };

const formReducer = (state: FormState, action: FormAction): FormState => {
  switch (action.type) {
    case 'SET_USERNAME':
      return { ...state, username: action.payload };
    case 'SET_PASSWORD':
      return { ...state, password: action.payload };
    case 'TOGGLE_REMEMBER':
      return { ...state, rememberMe: !state.rememberMe };
    default:
      return state;
  }
};

const [formState, dispatch] = useReducer(formReducer, {
  username: '',
  password: '',
  rememberMe: false,
});
```

## Generic List Component 

```

type ListProps<T> = {
  items: T[];
  renderItem: (item: T) => React.ReactNode;
};

function List<T>({ items, renderItem }: ListProps<T>) {
  return <ul>{items.map(renderItem)}</ul>;
}

<List
  items={[{ id: 1, name: 'John' }, { id: 2, name: 'Jane' }]}
  renderItem={(user) => <li key={user.id}>{user.name}</li>}
/>

// You can extend it like T extends { id: number } to restrict structure

```

example 2

```

type ListProps<T> = {
  items: T[];
};

export const List = <T,>(props: ListProps<T>) => {
  return (
    <div>
      {props.items.map((item, index) => {
        if (typeof item === "object") {
          // If item is an object and has a 'name' property
          return <h1 key={index}>{(item as any).name}</h1>;
        } else {
          // If item is a string or number
          return <h1 key={index}>{String(item)}</h1>;
        }
      })}
    </div>
  );
};

import { Greet } from "./Greet";
import { List } from "./List";
import "./styles.css";

export default function App() {
  return (
    <div className="App">
      <List items={[1, 2, 3]} />
      <List items={["sai", "gnana", "dachi"]} />
      <List
        items={[
          {
            id: 1,
            name: "sai",
          },
          {
            id: 2,
            name: "gnana",
          },
          {
            id: 1,
            name: "dachi",
          },
        ]}
      />
    </div>
  );
}


```

## React.ReactNode

```
// Represents anything React can render: JSX, string, number, null, array, etc.
type PropsWithChildren = {
  children: React.ReactNode;
};

const Card = ({ children }: PropsWithChildren) => {
  return <div>{children}</div>;
};

<Card>Hello</Card>
<Card><h1>Title</h1><p>Content</p></Card>
```


## React.ComponentType
```

//  Represents a React Component itself (function or class), not JSX.
// Useful when you want to pass a component via props and render it later.

type RendererProps = {
  component: React.ComponentType<{ title: string }>;
};

const Renderer = ({ component: Component }: RendererProps) => {
  return <Component title="Hello from ComponentType" />;
};

const Header = ({ title }: { title: string }) => <h1>{title}</h1>;

// Usage
<Renderer component={Header} />
```

##  JSX.Element
```

// Represents the JSX returned by a component. It’s a specific element, not anything renderable.
// A single React element (not an array, not a string, not multiple things).


const MyComponent = (): JSX.Element => {
  return <h1>Hello from JSX.Element</h1>;
};
```

## React.ReactElement
```
// A fully constructed element created by JSX or React.createElement.
// Use when you expect a *valid JSX element* as a prop, NOT strings or numbers.

type WrapperProps = {
  element: React.ReactElement;
};

const Wrapper = ({ element }: WrapperProps) => {
  return <div>{element}</div>;
};

// Valid usage
<Wrapper element={<h2>I’m a ReactElement</h2>} />

// ❌ Invalid usage
<Wrapper element="hello" /> // Error: Not a valid ReactElement
```


##  React.FC (FunctionComponent)
```
// Shortcut for typing functional components. Includes `children` by default.

type HeaderProps = {
  title: string;
};

const Header: React.FC<HeaderProps> = ({ title, children }) => {
  return (
    <>
      <h1>{title}</h1>
      <div>{children}</div>
    </>
  );
};

// Usage
<Header title="React FC">This is the subtitle</Header>
```






