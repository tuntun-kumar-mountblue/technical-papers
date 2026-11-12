## 1. What are the advantages of using JSX?
**JSX** (JavaScript XML) is a JavaScript syntax extension that lets us
write HTML-like markup inside JavaScript.

``` jsx
function App() {
  const name = "Tuntun";
  return <h1>Hello, {name}</h1>;
}
```

#Advantages

2. **Improves readability**:We can write HTML-like syntax inside JavaScript and UI structure and logic can stay together.
3. **JavaScript expressions**: We can use variables, functions and expressions inside {}.
4. **Component-based**: Makes it easier to create reusable UI components.
5. **Compile-time checking**: JSX is transformed into JavaScript using tools such as Babel, allowing tools to catch certain errors early.

## 2. What is the difference between the Virtual DOM and the Real DOM?

  -----------------------------------------------------------------------
  Real DOM                            Virtual DOM
  ----------------------------------- -----------------------------------
 Actual browser DOM tree.             Lightweight JavaScript representation of UI

  Represents the webpage elements.    Describes what the UI should look
                                      like.

  Browser APIs are used to read and   React uses element descriptions to
  update it.                          calculate UI changes.

  DOM changes can cause style,        Helps React determine which DOM
  layout, and paint work.             updates are needed.
  -----------------------------------------------------------------------


## 3. What is a bundler? Explain Webpack.

A Bundler is a tool that combines multiple files and their dependencies into one or more optimized output files (bundles) that can be served to the browser. 
These files depend on each other through import and export.

**Webpack** is a JavaScript module bundler. It takes different files as input, processes them and creates optimized bundles.

A simplified configuration:
``` js
const path = require("path");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname, "dist"),
  },
};
```

## 4. How does Vite work?

**Vite** is a modern frontend build tool that provides a development server and
a production build process.

**During development** 
1. Vite starts a development server. 
2. It serves source files as native ES modules where possible. 
3. It transforms files such as JSX when the browser requests them. 
4. It uses dependency pre-bundling to optimize dependencies. 
5. HMR (Hot Module Replacement) updates changed modules quickly, often without a full page reload.

**For production** - Vite bundles the application. - It optimizes and
minifies assets. - It outputs files ready to deploy.

Vite uses **esbuild** for dependency pre-bundling and uses **Rollup**
for production builds in the Vite and Vite 8 uses Rolldown as its bundler for both.

## 5. What is Babel?

**Babel** is a JavaScript compiler commonly used to transform modern
JavaScript syntax and JSX into JavaScript supported by the configured
target environment.

For example, JSX:

``` jsx
const element = <h1>Hello</h1>;
```

can be transformed into JavaScript using the React JSX runtime:

``` js
import { jsx } from "react/jsx-runtime";

const element = jsx("h1", { children: "Hello" });
```

## 6. What is a React Element?

A **React element** is an immutable JavaScript object that describes
what React should render.

``` jsx
const element = <h1>Hello World</h1>;
```

JSX is transformed into a React element creation call. Conceptually, the
element describes: - `type`: what should be rendered, such as `"h1"` or
a component function. - `props`: properties and children passed to it.

A React element is not the same thing as a browser DOM node. React uses
elements as descriptions when rendering and updating the UI.

## 7. In which situations does a React component re-render?

Common reasons include:

1.  **Its state is updated.** Calling a state setter can schedule a
    render.
2.  **Its parent re-renders.** By default, child components are rendered
    again as part of the parent's render.
3.  **A context it consumes changes.** Components using that context are
4.  **A class component calls `forceUpdate()`.** This is uncommon and
    generally should be avoided.

## 8. When should we use functional and class components?

For new React code, **function components are recommended**. They use
Hooks for state and other React features.

``` jsx
function Welcome() {
  return <h1>Welcome</h1>;
}
```

Class components are mainly encountered in older codebases or when
maintaining existing class-based components.

``` jsx
class Welcome extends React.Component {
  render() {
    return <h1>Welcome</h1>;
  }
}
```

## 9. What is the difference between functional and class components?

  -----------------------------------------------------------------------
  Function component                  Class component
  ----------------------------------- -----------------------------------
  Declared as a JavaScript function.  Declared as a JavaScript class
                                      extending `React.Component` or
                                      `PureComponent`.

  Uses Hooks such as `useState` and   Uses `this.state`,`this.setState()`
  `useEffect`.                         and lifecycle methods.
                                     
  Does not use `this` for component   Uses `this` to access props, state
  state.                              and methods.

  Usually has less boilerplate.       Often requires more boilerplate and
                                      method binding in older patterns.

  Recommended for new code.           Common in legacy applications and
                                      class-based Error Boundaries.
  -----------------------------------------------------------------------

## 10. Why should a component name start with an uppercase letter?

JSX uses capitalization to distinguish custom React components from
built-in HTML tags.

``` jsx
function Header() {
  return <h1>Hello</h1>;
}

function App() {
  return <Header />;
}
```

`<Header />` refers to the JavaScript component. A lowercase tag such as
`<header />` is treated as a built-in HTML element.

Therefore, React component names should begin with an uppercase letter.

## 11. Why do we need ReactDOM?

React describes the UI; **ReactDOM** is the React package that
integrates React with the browser DOM.

In a web application, `createRoot` creates a React root attached to a
DOM element, and `root.render()` displays the React tree there.

``` jsx
import { createRoot } from "react-dom/client";
import App from "./App";

const root = createRoot(document.getElementById("root"));
root.render(<App />);
```

React itself is not limited to the browser. Other renderers can target
other environments, while ReactDOM is specifically for web DOM
rendering.

## 12. What is the difference between state and props?

  -----------------------------------------------------------------------
  Props                               State
  ----------------------------------- -----------------------------------
  Data passed from a parent           Data managed by a component (or a
  component.                          Hook/store).

  Read-only to the receiving          Updated using the relevant state
  component.                          setter or state API.

  Used to configure or communicate    Used for data that changes over
  with a child.                       time and affects UI.

  Changes when the parent passes new  Changes when the component updates
  props.                              its state.
  -----------------------------------------------------------------------

Example:

``` jsx
function Greeting({ name }) {
  const [count, setCount] = useState(0);

  return (
    <>
      <h1>Hello, {name}</h1>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>
        Increase
      </button>
    </>
  );
}

// Parent:
<Greeting name="Tuntun" />
```

Here, `name` is a prop and `count` is state.

## 13. What are the differences between JSX and HTML?

  -----------------------------------------------------------------------
  JSX                                 HTML
  ----------------------------------- -----------------------------------
  Used inside JavaScript in React.    Markup language for webpages.

  Uses `className`.                   Uses `class`.

  Uses `htmlFor` for label            Uses `for`.
  association.

  JavaScript expressions go inside    JavaScript is not embedded this
  `{}`.                               way.

  Event handlers use camelCase,       HTML attributes are commonly
  e.g. `onClick`.                     lowercase, e.g. `onclick`.

  Elements must be properly closed.   Some HTML void elements do not need
                                      closing tags.

  Inline styles are JavaScript        Inline styles use a CSS string.
  objects.

  Custom React components use         HTML tags use standard tag names.
  uppercase names.
  -----------------------------------------------------------------------

Example:

``` jsx
const color = "red";

function App() {
  return (
    <label htmlFor="name">
      Name
      <input
        id="name"
        className="input"
        style={{ color }}
      />
    </label>
  );
}
```

## 14. Why do we use PropTypes?

**PropTypes** is a runtime type-checking library for component props. It
can warn developers in development when a component receives props of an
unexpected type.

``` jsx
import PropTypes from "prop-types";

function User({ name, age }) {
  return <p>{name} is {age} years old.</p>;
}

User.propTypes = {
  name: PropTypes.string.isRequired,
  age: PropTypes.number,
};
```

## 15. What are different ways to update state using setState?

This question refers to **class component** `this.setState()`.

**A. Pass an object**

``` jsx
this.setState({ count: 10 });
```

**B. Pass a function**

Use this when the next state depends on the previous state:

``` jsx
this.setState((prevState) => ({
  count: prevState.count + 1,
}));
```

**C. Pass a callback as the second argument**

The callback runs after the update has been committed:

``` jsx
this.setState(
  { count: 10 },
  () => console.log("Updated:", this.state.count)
);
```

`setState` shallowly merges the provided object into class state. For
function components, use `useState` setters instead; they replace the
state value rather than shallow-merging objects.

## 16. Explain: "useState is asynchronous in nature" with an example.

It is more accurate to say that **state updates are scheduled and may be batched**.
A state setter does not change the state variable in the currently executing render.

``` jsx
function Counter() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
    console.log(count); // Logs the value from this render
  }

  return <button onClick={handleClick}>{count}</button>;
}
```

If `count` was `0`, the log is `0`. React schedules an update and
renders again with the new value.

When the next value depends on the previous value, use a functional
update:

``` jsx
setCount((prev) => prev + 1);
```

Do not describe this as a Promise: `setState` does not return a Promise
that can be awaited.

## 17. Why should we not update state directly?

React uses state updates to know when it may need to render again.
Direct mutation does not properly notify React and can make previous
state snapshots unreliable.

Incorrect:

``` jsx
user.name = "Rahul";
```

Correct:

``` jsx
setUser((prev) => ({
  ...prev,
  name: "Rahul",
}));
```

For arrays:

``` jsx
setItems((prev) => [...prev, newItem]);
```

Use new objects or arrays rather than mutating existing state. This
makes updates predictable and works well with React's rendering model.

## 18. How can we handle form validation in React?

A common approach is to store form values and errors in state, validate
the values, and show error messages.

``` jsx
import { useState } from "react";

function SignupForm() {
  const [email, setEmail] = useState("");
  const [error, setError] = useState("");

  function handleSubmit(e) {
    e.preventDefault();

    if (!email.trim()) {
      setError("Email is required");
      return;
    }

    if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) {
      setError("Enter a valid email");
      return;
    }

    setError("");
    alert("Form submitted");
  }

  return (
    <form onSubmit={handleSubmit}>
      <label htmlFor="email">Email</label>
      <input
        id="email"
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      {error && <p role="alert">{error}</p>}
      <button type="submit">Submit</button>
    </form>
  );
}
```

For larger forms, libraries such as React Hook Form or Formik can reduce
repetitive code. Always validate important data on the server too;
client-side validation alone is not secure.

## 19. What is the Virtual DOM and how does it work?

The Virtual DOM is a common term for React's in-memory representation of
the UI. React creates element descriptions, renders components, compares
the new result with the previous result through reconciliation, and
commits necessary changes to the host environment.

Example:

``` jsx
function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <h1>Counter</h1>
      <p>{count}</p>
      <button onClick={() => setCount((n) => n + 1)}>
        Add
      </button>
    </>
  );
}
```

## 20. What is the difference between controlled and uncontrolled components?

  -----------------------------------------------------------------------
  Controlled component                Uncontrolled component
  ----------------------------------- -----------------------------------
  React state is the source of truth  The DOM maintains the input value.
  for the input value.

  Uses `value` or `checked` with an   Commonly uses `defaultValue`,
  event handler.                      `defaultChecked` and a ref.

  Easy to validate or react to every  Useful for simple forms or
  change.                             integrating with non-React code.
  -----------------------------------------------------------------------

Controlled example:

``` jsx
function Form() {
  const [name, setName] = useState("");

  return (
    <input
      value={name}
      onChange={(e) => setName(e.target.value)}
    />
  );
}
```

Uncontrolled example:

``` jsx
function Form() {
  const inputRef = useRef(null);

  function handleSubmit() {
    console.log(inputRef.current.value);
  }

  return (
    <>
      <input ref={inputRef} defaultValue="Tuntun" />
      <button onClick={handleSubmit}>Submit</button>
    </>
  );
}
```

## 21. Why do we need the key prop when displaying a list?

A `key` gives each sibling element a stable identity. React uses keys
during reconciliation to understand which list items were added,
removed, or moved.

``` jsx
const users = [
  { id: 1, name: "Aman" },
  { id: 2, name: "Riya" },
];

function UserList() {
  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

Use a stable, unique ID when possible. Avoid array indexes when list
items can be inserted, deleted, or reordered. A key is a special React
hint; it is not passed to the component as a normal prop.

## 22. Explain different lifecycle methods and their use cases.

Phase            	Hook	                When it runs
 -----------------------------------------------------------------------
**Mounting**	    useEffect(() => {},    [])	After initial commit
**Updating**  	useEffect(() => {},    [count])	After mount and when count changes
**Unmounting	**  Cleanup function	       Before effect re-runs and when component unmounts

## 23. Why do we use Context, and how does it work?

Context lets a component make data available to many descendants without
passing props through every intermediate component. This avoids **prop
drilling**.

Common use cases: - Theme (light/dark mode). - Current authenticated
user. - Locale or language. - App-level preferences.

Example:

``` jsx
import { createContext, useContext } from "react";

const ThemeContext = createContext("light");

function Child() {
  const theme = useContext(ThemeContext);
  return <p>Theme: {theme}</p>;
}

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Child />
    </ThemeContext.Provider>
  );
}
```

## 24. What is the use case of React.Fragment?

A component must return one parent-level value. `Fragment` lets us group
multiple elements without adding an extra DOM node.

``` jsx
function App() {
  return (
    <React.Fragment>
      <h1>Hello</h1>
      <p>Welcome</p>
    </React.Fragment>
  );
}
```

Short syntax:

``` jsx
function App() {
  return (
    <>
      <h1>Hello</h1>
      <p>Welcome</p>
    </>
  );
}
```

Use the explicit `<React.Fragment key={...}>` form when a Fragment in a
list needs a key. The shorthand `<>...</>` cannot receive a key.

## 25. Is it possible to loop inside JSX? Give an example.

JSX does not support a normal `for` statement directly inside its
markup. We commonly use JavaScript array methods such as `map()` inside
`{}`.

``` jsx
function UserList() {
  const users = ["Aman", "Riya", "Rahul"];

  return (
    <ul>
      {users.map((user) => (
        <li key={user}>{user}</li>
      ))}
    </ul>
  );
}
```

## 26. What are the advantages of using Hooks?

Hooks let function components use React features such as state, context,
refs, and effects.

Advantages: - Use state and other React features without writing a
class. - Reuse stateful logic through custom Hooks. - Organize related
logic together. - Avoid many class-specific patterns involving 

## 27. Explain different types of Hooks with code.

Common built-in Hooks include:

**State**

``` jsx
const [count, setCount] = useState(0);
```

**Effect**

``` jsx
useEffect(() => {
  document.title = "React App";
}, []);
```

**Ref**

``` jsx
const inputRef = useRef(null);
```

**Context**

``` jsx
const theme = useContext(ThemeContext);
```

**Reducer**

``` jsx
const [state, dispatch] = useReducer(reducer, initialState);
```

**Memoization**

``` jsx
const total = useMemo(() => calculateTotal(items), [items]);

const handleClick = useCallback(() => {
  console.log("Clicked");
}, []);
```


## 28. How do we use useEffect?

`useEffect` synchronizes a component with an external system, such as a
browser API, subscription, timer, or network connection.

Basic syntax:

``` jsx
useEffect(() => {
  // setup or synchronization

  return () => {
    // cleanup, if needed
  };
}, [dependencies]);
```

**A. No dependency array:** runs after every committed render.

``` jsx
useEffect(() => {
  console.log("After every render");
});
```

**B. Empty dependency array:** runs after the initial mount in
production; development Strict Mode may run an extra setup/cleanup
cycle.

``` jsx
useEffect(() => {
  console.log("Mounted");
}, []);
```

**C. With dependencies:** runs after mount and when a dependency
changes.

``` jsx
useEffect(() => {
  console.log("Count changed");
}, [count]);
```

**Cleanup example:**

``` jsx
useEffect(() => {
  const id = setInterval(() => {
    console.log("Tick");
  }, 1000);

  return () => clearInterval(id);
}, []);
```

Effects run after React commits the UI. Use them for synchronization
with external systems, not for every calculation that can be done during
rendering.

## 29. How do we use useRef?

`useRef` creates a mutable object whose `.current` property persists
between renders. Updating `.current` does not trigger a re-render.

**A. Access a DOM element**

``` jsx
function App() {
  const inputRef = useRef(null);

  return (
    <>
      <input ref={inputRef} />
      <button onClick={() => inputRef.current.focus()}>
        Focus
      </button>
    </>
  );
}
```

**B. Store a timer ID**

``` jsx
const timerRef = useRef(null);

function startTimer() {
  timerRef.current = setInterval(() => {
    console.log("Tick");
  }, 1000);
}

function stopTimer() {
  clearInterval(timerRef.current);
}
```

Use state for values that should appear in the UI; use refs for mutable
values that do not need to trigger rendering.

## 30. Explain the useContext Hook.

`useContext` reads and subscribes a component to a context value.

``` jsx
import { createContext, useContext } from "react";

const UserContext = createContext(null);

function Profile() {
  const user = useContext(UserContext);
  return <h1>{user.name}</h1>;
}

function App() {
  const user = { name: "Tuntun" };

  return (
    <UserContext.Provider value={user}>
      <Profile />
    </UserContext.Provider>
  );
}
```

It helps avoid prop drilling. The component reads the value from the
nearest provider above it. If the provided value changes, consumers are
updated.

## 31. Explain the useReducer Hook.

`useReducer` manages state using a reducer function. It is useful when
state logic has multiple actions or related transitions.

Syntax:

``` jsx
const [state, dispatch] = useReducer(reducer, initialState);
```

Example:

``` jsx
import { useReducer } from "react";

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    case "reset":
      return initialState;
    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <>
      <h1>{state.count}</h1>
      <button onClick={() => dispatch({ type: "increment" })}>
        +
      </button>
      <button onClick={() => dispatch({ type: "decrement" })}>
        -
      </button>
      <button onClick={() => dispatch({ type: "reset" })}>
        Reset
      </button>
    </>
  );
}
```

The reducer receives the current state and an action, then returns the
next state. Do not mutate the existing state.

## 32. Which Hooks can we use to manage state in React?

The main built-in state Hooks are:

**1. `useState`** --- simple local state.

``` jsx
const [name, setName] = useState("");
setName("Aman");
```

**2. `useReducer`** --- state with more structured update logic.

``` jsx
const [state, dispatch] = useReducer(reducer, { count: 0 });
dispatch({ type: "increment" });
```

## 33. What is the difference between a DOM element and a React element?

  -----------------------------------------------------------------------
  DOM element                         React element
  ----------------------------------- -----------------------------------
  Actual browser object/node.         JavaScript object describing UI.

  Created and managed by browser DOM  Created through JSX or React
  APIs or a renderer.                 element APIs.

  Can be changed with DOM APIs such   Immutable description; create a new
  as `textContent`.                   element description to represent a
                                      different UI.

  Example: an `HTMLDivElement`.       Example: the result of
                                      `<div>Hello</div>`.
  -----------------------------------------------------------------------

Example:

``` jsx
const reactElement = <h1>Hello</h1>;

const domElement = document.createElement("h1");
domElement.textContent = "Hello";
```

The first is a React element description. The second is an actual DOM
node.

## 34. What happens when a runtime error occurs in JSX? How can we fix it?

A runtime error happens while the application is running, for example
when code tries to access a property on `undefined`.

``` jsx
function User({ user }) {
  return <h1>{user.name}</h1>;
}
```

If `user` is `undefined`, accessing `user.name` throws an error.

**Ways to fix or handle it** 
1. Find the error in the browser console and React component stack. 
2. Check whether data exists before accessing it. 
3. Use conditional rendering or optional chaining.
4. Handle loading and error states for asynchronous data.
5. Use an Error Boundary to show fallback UI for errors in descendant rendering.

Safer example:

``` jsx
function User({ user }) {
  if (!user) return <p>Loading...</p>;

  return <h1>{user.name}</h1>;
}
```

Optional chaining:

``` jsx
<h1>{user?.name ?? "Unknown user"}</h1>
```

Error Boundaries catch many rendering errors in descendant components,
but they do not catch every error---for example, ordinary event-handler
errors or errors in asynchronous callbacks are not caught by an Error
Boundary.

## 35. What are the Rules of Hooks?

There are two core Rules of Hooks:

1.  **Call Hooks at the top level.** Do not call Hooks inside loops,
    conditions, or nested functions.
2.  **Call Hooks only from React function components or custom Hooks.**
    Do not call them from ordinary JavaScript functions or class
    components.

Correct:

``` jsx
function App({ active }) {
  const [count, setCount] = useState(0);

  if (!active) {
    return null;
  }

  return <p>{count}</p>;
}
```

Incorrect:

``` jsx
function App({ active }) {
  if (active) {
    const [count, setCount] = useState(0); // Incorrect
  }

  return null;
}
```

Following these rules lets React associate Hook state with the correct
Hook call across renders. The `eslint-plugin-react-hooks` package can
help detect violations.

## 36. Can we put Hooks inside an if statement? Why or why not?

No. Hooks must be called in the same order on every render.

Incorrect:

``` jsx
function App({ active }) {
  if (active) {
    const [count, setCount] = useState(0);
  }

  return null;
}
```

If `active` changes, the number or order of Hook calls can change. React
may then associate state with the wrong Hook call.

Correct:

``` jsx
function App({ active }) {
  const [count, setCount] = useState(0);

  if (!active) return null;

  return <p>{count}</p>;
}
```

Call the Hook unconditionally at the top level, then put the condition
inside the component logic or inside the effect as appropriate.

## 37. What are the advantages of React.StrictMode?

`React.StrictMode` is a development-only tool that helps identify
potential problems in a React application.

``` jsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import App from "./App";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

Advantages: - Helps find components with impure rendering. - Helps
detect deprecated APIs in applicable code. - Runs extra development
checks for Effects, including an additional setup/cleanup cycle, to
expose missing cleanup. - Helps identify some problems with ref
callbacks.

Important: - Strict Mode does not affect the production build. - In
development, some render and Effect behavior may happen more than once
by design. - Do not remove Strict Mode just to hide a bug; fix the
underlying side effect or missing cleanup.

## 38. How can we create a production build of a React app?

For a Vite React project:
1.  Open the project terminal.
2.  Install dependencies if needed:
``` bash
npm install
```
3.  Create the production build:
``` bash
npm run build
```
4.  Vite generates the production files in the `dist` folder by default.
5.  Test the build locally:

``` bash
npm run preview
```
6.  Deploy the contents of `dist` to a static hosting provider.

For other setups, the command depends on the toolchain. For example,
older Create React App projects commonly use `npm run build`.

## 39. What is the difference between Development and Production?

  -----------------------------------------------------------------------
  Development                         Production
  ----------------------------------- -----------------------------------
  Used while building and debugging   Used by end users.
  the application.

  Includes helpful warnings and       Optimized for delivery and runtime
  debugging information.              performance.

  Often includes source maps and      Usually minimizes exposed debugging
  detailed errors.                    details.

  May include Strict Mode development Strict Mode's extra development
  checks.                             checks do not run.

  Uses a development server and HMR.  Serves generated build assets.

  Usually not optimized for smallest  Assets are typically bundled,
  download size.                      minified, and optimized.
  -----------------------------------------------------------------------


