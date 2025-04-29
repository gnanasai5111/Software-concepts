### React with Typescript

## Props

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
