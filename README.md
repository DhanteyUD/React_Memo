# React-Memo
React.memo is a function that you can use to optimize the render performance of pure function components and hooks. It has been introduced in React v16.6.

Using `memo` will cause React to skip rendering a component if its props have not changed thus improving performance.

# Problem
In this example, the `Todo` component re-renders even when the list of todo have not changed.

## Example:

`App.js`:

```js
import { useState } from "react";
import ReactDOM from "react-dom/client";
import Todo from "./Todo";

const App = () => {
  const [count, setCount] = useState(0);
  const [todos, setTodos] = useState(["todo 1", "todo 2"]);

  const increment = () => {
    setCount((val) => val + 1);
  };

  return (
    <>
      <Todo todos={todos} />
      <hr />
      <div>
        Count: {count}
        <button onClick={increment}>+</button>
      </div>
    </>
  );
};

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```

`Todo.js`:

```js
const Todo = ({ todos }) => {
  return (
    <>
      <h2>My Todo List</h2>
      {todos.map((todo, index) => {
        return <p key={index}>{todo}</p>;
      })}
    </>
  );
};

export default Todos;
```

When you click the increment button, the `Todo` component re-renders.

If this was a complex component, it could cause performance issues.

# Solution

To fix this problem, we can use react `memo`.

- [x] to keep the `Todo` component from needlessly re-rendering.

- [x] Wrap the `Todo` component export in `memo`:


## Example:

`App.js`:

```js
import { useState } from "react";
import ReactDOM from "react-dom/client";
import Todo from "./Todo";

const App = () => {
  const [count, setCount] = useState(0);
  const [todos, setTodos] = useState(["todo 1", "todo 2"]);

  const increment = () => {
    setCount((val) => val + 1);
  };

  return (
    <>
      <Todo todos={todos} />
      <hr />
      <div>
        Count: {count}
        <button onClick={increment}>+</button>
      </div>
    </>
  );
};

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```
`Todo.js`:

```js
import { memo } from "react";

const Todos = ({ todos }) => {
  return (
    <>
      <h2>My Todo List</h2>
      {todos.map((todo, index) => {
        return <p key={index}>{todo}</p>;
      })}
    </>
  );
};

export default memo(Todos);
```

Now the `Todo` component only re-renders when the `todos` that are passed to it through props are updated.


