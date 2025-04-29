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

### 4. Passing HTML Element via Props

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

### 5. Passing React Element via Props

```
type CustomComponentProps = {
  component: React.ReactNode;
};

export const ComponentContainer = (props: CustomComponentProps) => {
  return <section>{props.component}</section>;
};
```

**Usage:**

```
<ComponentContainer component={<button>Click Me</button>} />
```
