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



