## Technical Pepper

# 1. What is React?

React is a JavaScript library used to build interactive user interfaces.
It helps developers create reusable UI components and is commonly used
for building single-page applications (SPAs).
Note: React is a library, not a complete framework.

### Explanation

-   React is used to build the UI of web applications.
-   It follows a component-based architecture.
-   Components can be reused in different parts of an application.
-   React updates the UI when its state or props change.


# 2. JSX, Components and Props

## 2.1 What is JSX?

i. JSX stands for JavaScript XML. It is a syntax extension for JavaScript
that allows us to write HTML-like code inside JavaScript.

ii. JSX makes UI code easier to read and write. Build tools transform JSX
into JavaScript instructions that React can understand.

## 2.2 What is a Component?

A component is a reusable and independent piece of UI in React and a 
component can contain JSX, JavaScript logic, props, state and event
handlers.

## 2.3 What are Props?

Props are read-only inputs used to pass data from a parent component to
a child component.

### Important Points

-   Props are passed from parent to child.
-   Props are read-only; a child should not modify them.
-   Props can contain strings, numbers, arrays, objects, functions and
    JSX.

# 3. Babel and Its Role in React

Babel is a JavaScript compiler that can transform JSX and modern
JavaScript syntax into JavaScript compatible with the configured target
environment.

Modern React projects can use the automatic JSX runtime, which generates
calls to JSX runtime functions instead.


# 4. Virtual DOM vs Real DOM

## What is the Real DOM?

The Real DOM is the actual document structure maintained by the browser.
It represents the elements displayed on a webpage.

## What is the Virtual DOM?

The Virtual DOM is a lightweight representation of the UI that React
uses during its rendering process.

React renders the UI, compares the new result with the previous result
during reconciliation, and commits the necessary changes to the real
DOM.

### Difference

  -----------------------------------------------------------------------
  Virtual DOM                         Real DOM
  ----------------------------------- -----------------------------------
  A lightweight representation of the The actual document structure in
  UI.                                 the browser.

  Used by React during rendering and  Used by the browser to display the
  reconciliation.                     webpage.

  React compares renders to determine DOM updates can trigger browser
  changes.                            rendering work.


# 5. What is a Bundler?

A bundler is a development tool that processes application modules and
assets and prepares files for the browser. It can also optimize assets
for production.

### Examples

-   Vite
-   Webpack
-   Parcel
-   Rollup


# 6. Why Vite Instead of Create React App?

Vite provides a fast development experience, quick server startup and
Hot Module Replacement (HMR). Create React App is deprecated for new
projects, so Vite is a popular choice for setting up React applications.

### Difference

  -----------------------------------------------------------------------
  Vite                                Create React App (CRA)
  ----------------------------------- -----------------------------------
  Modern build tool and development   Older React project setup tool.
  server.

  Uses native ES modules in           Uses Webpack-based tooling.
  development.

  Provides fast server startup and    Development startup can be slower
  HMR.                                in larger projects.

  Uses Rollup for production builds   Uses Webpack for production builds.
  through its build pipeline.

  Recommended as a common lightweight Deprecated for new applications.
  setup option.

### What is HMR?

HMR stands for Hot Module Replacement. It updates changed modules during
development without requiring a full page reload in many cases.


# 7. React Project Folder Structure

A typical Vite + React project looks like this:

### Example:
```jsx
my-react-app/
├── node_modules/
├── public/
│   └── vite.svg
├── src/
│   ├── assets/
│   ├── App.jsx
│   ├── App.css
│   ├── index.css
│   └── main.jsx
├── .gitignore
├── index.html
├── package.json
├── package-lock.json
└── vite.config.js
```
# 8. Class vs Functional Components

### Class Component

A class component is a React component created using an ES6 class. It
extends `React.Component` and uses a `render()` method to return UI.
```jsx
import React, { Component } from "react";
class App extends Component {
  render() {
    return <h1>Hello React</h1>;
  }
}
export default App;
```

### Functional Component

A functional component is a JavaScript function that returns React
elements.
```jsx
function App() {
  return <h1>Hello React</h1>;
}
export default App;
```

# 9. What are Hooks?

Hooks are special React functions that allow functional components to
use React features such as state, context, refs and effect-related
logic.

### Common Hooks

-   `useState`
-   `useEffect`
-   `useRef`
-   `useContext`
-   `useMemo`
-   `useCallback`

### Rules of Hooks

1.  Call hooks at the top level of a React component or custom hook.
2.  Do not call hooks inside loops, conditions or nested functions.
3.  Call hooks only from React function components or custom hooks.


# 10. useState

`useState` is a React hook used to add and manage state in a functional
component.

### Syntax
```jsx
const [state, setState] = useState(initialValue);
```


# 11. useEffect

`useEffect` is a React hook used to synchronize a component with
external systems, such as APIs, timers, subscriptions and browser event
listeners.

### Syntax
``` jsx
useEffect(() => {
  // Side-effect logic

  return () => {
    // Cleanup logic
  };
}, [dependencies]);
```

### Three Common Dependency Patterns

  -----------------------------------------------------------------------
  Syntax                              Behaviour
  ----------------------------------- -----------------------------------
  `useEffect(() => {})`               Runs after every committed render.

  `useEffect(() => {}, [])`           Runs after the initial mount.

  `useEffect(() => {}, [count])`      Runs after the initial mount and
                                      when `count` changes.

### What is Cleanup?

A cleanup function is used to stop or undo an effect, such as clearing a
timer or removing an event listener.


# 13. Passing Data Between Components

There are different ways to share data between React components.

## 13.1 Parent to Child -- Props

The parent passes data through props.

``` jsx
function Child({ name }) {
  return <h1>Hello {name}</h1>;
}

function Parent() {
  return <Child name="Rahul" />;
}
```

## 13.2 Child to Parent -- Callback Function

The parent passes a function to the child. The child calls that function
and sends data back.

``` jsx
function Child({ sendData }) {
  return (
    <button onClick={() => sendData("Hello Parent")}>
      Send Data
    </button>
  );
}

function Parent() {
  function receiveData(data) {
    console.log(data);
  }

  return <Child sendData={receiveData} />;
}
```

## 13.3 Between Sibling Components

For sibling components, move shared state to their nearest common
parent. Then pass the data and required callback functions through
props.

For components that are far apart in the component tree, Context API or
a state management library may be useful.


# 14. What is Lifting State Up?

Lifting state up means moving shared state from child components to
their nearest common parent component so that multiple components can
access and update the same data.


# 15. How to use event listeners in the component?

## 15.1 Event Handling in React

React provides event handler props to respond to user actions.

### Common React Events

-   `onClick`
-   `onChange`
-   `onSubmit`
-   `onMouseEnter`
-   `onKeyDown`


## 15.2 Native Event Listeners with useEffect

Sometimes we need to listen for browser events, such as window resize or
key presses. We can use `addEventListener()` inside `useEffect()`.

### Example: Window Resize

``` jsx
import { useEffect } from "react";

function App() {
  useEffect(() => {
    function handleResize() {
      console.log(window.innerWidth);
    }

    window.addEventListener("resize", handleResize);

    return () => {
      window.removeEventListener("resize", handleResize);
    };
  }, []);

  return <h1>Resize the browser window</h1>;
}

export default App;
```

### Why is Cleanup Important?

We remove the event listener when the effect is cleaned up. This
prevents unnecessary listeners from remaining active after the component
is removed or the effect is re-run.


