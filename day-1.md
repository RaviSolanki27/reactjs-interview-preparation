
# Day 1: React Basics
## What is React?

React is a **JavaScript library** for building user interfaces, developed and maintained by **Meta (Facebook)**. It allows developers to create reusable UI components and efficiently manage the state of web applications.

---

## Why Use React?

1. **Component-Based Architecture**:  
   React's component-based structure promotes reusability and modularity, making code easier to maintain and scale.

2. **Virtual DOM**:  
   React uses a **Virtual DOM** to update the UI efficiently. Instead of updating the real DOM directly, React minimizes changes by comparing differences (diffing) and applying updates selectively.

3. **Declarative UI**:  
   React allows developers to describe "what" the UI should look like, rather than "how" to manipulate the DOM to achieve it.

4. **React Hooks**:  
   Hooks like `useState` and `useEffect` simplify state management and side-effect handling in functional components.

5. **Rich Ecosystem**:  
   React has a vast ecosystem of libraries and tools, making it highly versatile for various use cases (e.g., routing with React Router, state management with Redux).

6. **Cross-Platform Support**:  
   React can be used to build web applications (**ReactJS**) and mobile applications (**React Native**) using the same principles.

7. **Large Community & Support**:  
   React has a large and active community, ensuring robust support, extensive documentation, and numerous learning resources.

---

React is ideal for building modern, interactive, and dynamic web applications, making it one of the most popular front-end libraries in the development world.

---


- What is a class component? a class component in object-oriented programming is a blueprint for creating objects that share common properties and methods. The class defines both the state (properties) and behavior (methods) that objects created from it will have.

- **What is a class component in React?** A class component in React is a JavaScript class that extends from **React.Component** and has at least one method called `render()` that returns **JSX**. This type of component allows you to manage state and lifecycle methods, which is one of the key differences between class components and functional components (before React 16.8 introduced hooks).

- **What is a functional component?** A functional component in React is a simpler way of defining components using JavaScript functions instead of classes. These components are typically used for components that do not require their own state or lifecycle methods, although with the introduction of React Hooks in React 16.8, functional components can now manage state and perform side effects as well.

---

## Difference between class component and functional component?

---

| **Feature**                | **Class Component**                                         | **Functional Component**                                    |
|----------------------------|-------------------------------------------------------------|-------------------------------------------------------------|
| **Syntax**                 | Uses `class` syntax and a `render()` method.               | Uses function syntax (no `render()` method).                |
| **State Management**       | Uses `this.state` and `this.setState()` for state management. | Uses the `useState()` hook for state management.            |
| **Lifecycle Methods**      | Uses lifecycle methods like `componentDidMount()`, `componentDidUpdate()`, `componentWillUnmount()`. | Uses the `useEffect()` hook for side effects (similar to lifecycle methods). |
| **`this` Keyword**         | The `this` keyword is used to refer to the component instance. | The `this` keyword is not used in functional components.     |
| **Hooks**                  | Cannot use hooks (prior to React 16.8).                    | Can use hooks like `useState`, `useEffect`, `useContext`, etc. |
| **Performance**            | More overhead due to the class-based structure and `this` keyword. | Typically more performant and lightweight.                  |
| **Readability and Maintenance** | Can become verbose with multiple lifecycle methods, event handlers, and the `constructor()`. | More concise, easier to read, and maintain. No `this` keyword and less boilerplate. |
| **Event Handling**         | Uses class methods and binds `this` to access state and props. | Directly accesses state and props without needing to bind `this`. |
| **Code Example**           | ```class MyComponent extends React.Component {```<br/> ```constructor(props) {```<br/>``` super(props);```<br/>``` this.state = { count: 0 };```<br/>``` }```<br/>``` render() {```<br/>``` return (<button onClick={() => this.setState({ count: this.state.count + 1 })}>Increment</button>);```<br/>``` }```<br/>```}``` | ```const MyComponent = () => {```<br/>``` const [count, setCount] = useState(0);```<br/>``` return (<button onClick={() => setCount(count + 1)}>Increment</button>);```<br/>```}``` |
| **Default Use Case**       | Best used for more complex components with multiple lifecycle methods. | Best for simple, readable components and functional logic with hooks. |
| **Legacy Code**            | Common in older React codebases.                           | Preferred in newer React codebases with React 16.8+ features. |
| **Error Boundaries**       | Can implement error boundaries using `componentDidCatch()` for handling JavaScript errors. | Cannot implement error boundaries directly. Error boundaries are still class-based in React. |

---

### Conclusion:

- **Class Components** are more complex and were the original way of defining React components. They are still useful for some specific cases (e.g., error boundaries), but with modern React features like **hooks**, **functional components** have become the preferred choice due to their simplicity, readability, and performance.

---


### Lifecycle Methods in Class Components vs. Functional Components with Hooks

| **Lifecycle Method**               | **Class Component**                                                                                                    | **Functional Component with Hooks**                                                                                             |
|------------------------------------|------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| **1. Mounting (component mounting)** | **`constructor()`** - Called once before the component is mounted. It is used for initializing state or binding methods. | **`useState()`** - Initializes state for the component. The `useEffect()` hook can be used to perform actions on mount.         |
| **2. Mounting (component mounting)** | **`componentDidMount()`** - Called after the component is mounted in the DOM. Used for fetching data or side effects. | **`useEffect()`** with an empty dependency array `[]` mimics `componentDidMount`. It runs once after the initial render.       |
| **3. Rendering (rendering UI)**     | **`render()`** - A required method that returns the JSX to render the UI of the component.                             | **Return statement** in the function body - The component returns JSX directly from the function body. No `render()` method is needed. |
| **4. Updating (props or state change)** | **`shouldComponentUpdate()`** - Determines if the component should re-render. Returns a boolean.                      | **`useMemo()`** and **`React.memo()`** can be used to optimize re-renders based on specific conditions, similar to `shouldComponentUpdate`. |
| **5. Updating (props or state change)** | **`componentDidUpdate(prevProps, prevState)`** - Called after every update to the component.                          | **`useEffect()`** - Runs after every render unless you pass specific dependencies in the dependency array.                    |
| **6. Unmounting (component removal)** | **`componentWillUnmount()`** - Called just before the component is unmounted and removed from the DOM.                | **`useEffect()`** with a cleanup function inside it. It acts like `componentWillUnmount` when returned from the hook.           |
| **7. Error Handling**               | **`componentDidCatch(error, info)`** - Catches JavaScript errors in the component tree and displays fallback UI.      | Error boundaries in functional components are not supported. Use class components for error boundaries.                       |

---

### Detailed Breakdown

1. **`constructor()` (Class) → `useState()` (Function)**
   - **Class Component**: The constructor is used for initializing state and binding methods.
   - **Functional Component**: `useState()` is used to initialize state directly in the component body.

2. **`componentDidMount()` (Class) → `useEffect()` (Function)**
   - **Class Component**: `componentDidMount` is invoked after the component has been rendered to the screen. It's typically used for side-effects like API calls or subscribing to services.
   - **Functional Component**: `useEffect()` with an empty dependency array `[]` behaves similarly to `componentDidMount`. It runs once after the component is mounted.

3. **`render()` (Class) → `Return` (Function)**
   - **Class Component**: The `render()` method is required in class components. It returns the JSX to be rendered by the component.
   - **Functional Component**: In functional components, the return statement directly renders the JSX. No `render()` method is required.

4. **`shouldComponentUpdate()` (Class) → `useMemo()` or `React.memo()` (Function)**
   - **Class Component**: `shouldComponentUpdate()` lets you prevent unnecessary re-renders by returning `false` if the component should not re-render.
   - **Functional Component**: `useMemo()` or `React.memo()` can be used to optimize re-renders in functional components by memoizing the result of a computation or wrapping a component to only re-render when its props change.

5. **`componentDidUpdate()` (Class) → `useEffect()` (Function)**
   - **Class Component**: `componentDidUpdate` is called after the component re-renders due to a prop or state change.
   - **Functional Component**: `useEffect()` is called after each render, and you can specify specific dependencies in the second argument to control when it runs.

6. **`componentWillUnmount()` (Class) → `useEffect()` Cleanup (Function)**
   - **Class Component**: `componentWillUnmount()` is called just before the component is removed from the DOM. It's used for cleanup (e.g., removing event listeners or canceling API requests).
   - **Functional Component**: The cleanup function in `useEffect()` handles cleanup when the component is unmounted. It is returned from the `useEffect()` hook and runs when the component is about to unmount.

7. **Error Handling**
   - **Class Component**: `componentDidCatch()` is used to catch errors in the component tree and render a fallback UI.
   - **Functional Component**: Error boundaries are still not possible in functional components. To handle errors in functional components, you need to use class components for error boundaries or use try-catch blocks inside `useEffect`.

---

### Example: Mounting Lifecycle in Both Components

#### **Class Component**

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = { data: null };
  }

  componentDidMount() {
    fetch('/api/data')
      .then(response => response.json())
      .then(data => this.setState({ data }));
  }

  render() {
    return (
      <div>
        {this.state.data ? <p>{this.state.data}</p> : <p>Loading...</p>}
      </div>
    );
  }
}
```

#### **Functional Component**

```jsx
import { useState, useEffect } from 'react';

const MyComponent = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('/api/data')
      .then(response => response.json())
      .then(data => setData(data));
  }, []); // Empty array mimics componentDidMount()

  return (
    <div>
      {data ? <p>{data}</p> : <p>Loading...</p>}
    </div>
  );
};
```

---

### Conclusion:

- **Class Components** require the `render()` method to output JSX, whereas **functional components** can directly return JSX from the function body.
- **Functional components** with **hooks** (like `useState`, `useEffect`) provide a simpler, more concise way to manage state and lifecycle methods compared to class components.

---
## Install React and set up a project using Create React App.

Here are the commands to create a React project in **JavaScript** and **TypeScript**:

### For JavaScript:
```bash
npx create-react-app my-app
```

### For TypeScript:
```bash
npx create-react-app my-app --template typescript
``` 

Replace `my-app` with your desired project name.


---

Here’s the explanation about the syntax of **Functional Components** in React, written in Markdown:

---

# Functional Components in React

Functional components are one of the two types of components in React (the other being class components). They are simpler to write and typically used for presentational purposes.

## Syntax of Functional Components

A **functional component** is just a JavaScript function that returns JSX. It does not have access to lifecycle methods or state by default (though you can use hooks to manage state and side effects). Here's the basic syntax:

### Basic Functional Component

```jsx
import React from 'react';

const MyComponent = () => {
  return <div>Hello, World!</div>;
};

export default MyComponent;
```

### Explanation:
1. **Function Declaration**: The component is defined as a function (`const MyComponent = () => {}`).
2. **JSX Return**: Inside the function, you return the JSX that will render the UI (e.g., `<div>Hello, World!</div>`).
3. **Export**: `export default MyComponent;` makes the component available for import in other parts of your application.

## With Props

You can pass **props** to functional components, just like in class components. The props are received as function arguments.

```jsx
import React from 'react';

const Greeting = (props) => {
  return <h1>Hello, {props.name}!</h1>;
};

export default Greeting;
```

Alternatively, you can use **destructuring** to extract props:

```jsx
import React from 'react';

const Greeting = ({ name }) => {
  return <h1>Hello, {name}!</h1>;
};

export default Greeting;
```

### Explanation:
- **Props**: `props` is an object that contains all the properties passed to the component. In the destructuring version, `{ name }` extracts the `name` prop directly.
  
## Using State and Effects (with Hooks)

In modern React, **hooks** allow functional components to manage state and side effects, which were previously only available in class components.

### Example with `useState`:

```jsx
import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};

export default Counter;
```

### Explanation:
- **`useState`**: `useState(0)` initializes a state variable (`count`) with an initial value of `0`. `setCount` is a function that updates the `count` state.

### Example with `useEffect`:

```jsx
import React, { useState, useEffect } from 'react';

const DataFetcher = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('/api/data')
      .then((response) => response.json())
      .then((data) => setData(data));
  }, []); // Empty array means it runs only once (componentDidMount)

  return <div>{data ? <p>{data}</p> : <p>Loading...</p>}</div>;
};

export default DataFetcher;
```

### Explanation:
- **`useEffect`**: Runs after the component mounts. The empty dependency array `[]` ensures the effect runs only once, similar to `componentDidMount` in class components.

---

## Summary

- **Functional components** are defined using a function that returns JSX.
- **Props** are passed as arguments to the function.
- **State** and **side effects** can be handled using hooks like `useState` and `useEffect`.
- Functional components are generally more concise and easier to understand than class components, making them the preferred choice for many React developers today.

---

Here’s an explanation about **JSX**, including how to write and render JSX, as well as embedding expressions and applying styles, in **Markdown** format:

---

# JSX in React

**JSX (JavaScript XML)** is a syntax extension for JavaScript, commonly used with React to describe what the UI should look like. It allows you to write HTML-like structures within JavaScript code, making React code more readable and expressive.

## Writing and Rendering JSX

JSX is not a separate language; it is a syntactic sugar over `React.createElement()` calls. When you write JSX, React compiles it to `React.createElement()` calls, which the browser can render.

### Basic Syntax

Here’s how you can write JSX:

```jsx
import React from 'react';

const MyComponent = () => {
  return <h1>Hello, JSX!</h1>;
};

export default MyComponent;
```

### Explanation:
- The JSX syntax looks similar to HTML but is embedded within JavaScript code. In this case, it returns an `<h1>` element with the text "Hello, JSX!".
- You can render this component in the root DOM node (usually `index.js` or `App.js` in a React app).

### Rendering JSX

To render a JSX element into the DOM, you typically use `ReactDOM.render()`. In modern React (since React 18), you would use `ReactDOM.createRoot()` for rendering:

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import MyComponent from './MyComponent';

// Render JSX
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<MyComponent />);
```

### Explanation:
- `ReactDOM.createRoot()` creates a root DOM node to render the React component.
- The component (`MyComponent`) is rendered inside the element with `id="root"`.

## Embedding Expressions in JSX

You can embed JavaScript expressions inside JSX by wrapping them in curly braces `{}`. These expressions can be variables, function calls, or mathematical operations.

### Example with Variables:

```jsx
const name = 'John';

const Greeting = () => {
  return <h1>Hello, {name}!</h1>;
};
```

### Example with Function Calls:

```jsx
const getMessage = () => 'Welcome to JSX!';

const Message = () => {
  return <p>{getMessage()}</p>;
};
```

### Example with Math Operations:

```jsx
const Counter = () => {
  const number = 5;
  return <p>{number * 2}</p>;
};
```

### Explanation:
- Inside JSX, expressions like `name`, `getMessage()`, or `number * 2` are evaluated and inserted into the rendered output.
- Expressions can be any valid JavaScript code (variables, functions, operations, etc.).

## Applying Styles in JSX

There are two common ways to apply styles in JSX:

### 1. **Inline Styles**

You can apply styles directly to elements using the `style` attribute, which takes an object with camelCased properties and string values for CSS properties.

```jsx
const StyledComponent = () => {
  const divStyle = {
    color: 'blue',
    backgroundColor: 'lightgray',
    padding: '10px'
  };

  return <div style={divStyle}>This is a styled div!</div>;
};
```

### Explanation:
- `divStyle` is an object where CSS property names are camelCased (e.g., `backgroundColor`, `fontSize`), and the property values are strings.
- The `style` attribute in JSX takes this object and applies the styles to the `div` element.

### 2. **CSS Classes**

You can also apply CSS classes using the `className` attribute (since `class` is reserved in JavaScript). This is the most common way to style React components.

```jsx
import './styles.css';

const StyledComponent = () => {
  return <div className="my-class">This is a div with a CSS class!</div>;
};
```

In the `styles.css` file:

```css
.my-class {
  color: red;
  background-color: yellow;
  padding: 10px;
}
```

### Explanation:
- You define the styles in a separate CSS file (`styles.css`).
- In JSX, you use the `className` attribute to reference the class in your CSS file.

## Combining Both: Inline and Class-based Styles

You can combine inline styles and CSS classes in the same component if needed:

```jsx
const StyledComponent = () => {
  const inlineStyle = {
    fontSize: '20px',
    color: 'green'
  };

  return (
    <div className="my-class" style={inlineStyle}>
      This div has both inline and class-based styles!
    </div>
  );
};
```

---

## Summary of JSX Features:

- **Writing JSX**: JSX allows you to write HTML-like syntax in JavaScript. It's transpiled into `React.createElement()` calls.
- **Rendering JSX**: JSX elements are rendered into the DOM using `ReactDOM.render()` or `ReactDOM.createRoot()`.
- **Embedding Expressions**: You can embed JavaScript expressions in JSX by wrapping them in curly braces `{}`.
- **Applying Styles**: Styles can be applied inline with the `style` attribute or through external CSS using the `className` attribute.

---



# React Hooks

React introduced **Hooks** in version 16.8 to allow functional components to manage state and side effects, which were previously only available in class components. Hooks enable cleaner, more readable, and reusable code.

## `useState`: Managing Component State

`useState` is a **Hook** that lets you add state to your functional components. It returns an array with two elements:
1. The current state value.
2. A function that allows you to update the state.

### Basic Syntax

```jsx
import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);  // Initial state value is 0

  const increment = () => {
    setCount(count + 1);  // Updates the count
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
};

export default Counter;
```

### Explanation:
- `const [count, setCount] = useState(0);`
  - `count` is the current state variable, and it is initialized to `0`.
  - `setCount` is the function used to update the state. When you call `setCount()`, React re-renders the component with the updated state.
  
- **How to Update State**: The `setCount` function is called with a new value to update the state (`setCount(count + 1)`).

### Multiple States in One Component

You can use `useState` multiple times in the same component to manage different pieces of state:

```jsx
import React, { useState } from 'react';

const UserProfile = () => {
  const [name, setName] = useState('');
  const [age, setAge] = useState('');

  return (
    <div>
      <input
        type="text"
        placeholder="Name"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
      <input
        type="number"
        placeholder="Age"
        value={age}
        onChange={(e) => setAge(e.target.value)}
      />
      <p>Name: {name}</p>
      <p>Age: {age}</p>
    </div>
  );
};

export default UserProfile;
```

---

## `useEffect`: Handling Side Effects

`useEffect` is a **Hook** that lets you perform **side effects** in your functional components. Side effects are operations like:
- Data fetching
- Subscriptions
- Manually changing the DOM

By default, `useEffect` runs **after every render**, but you can control when it runs by passing a dependency array as the second argument.

### Basic Syntax

```jsx
import React, { useState, useEffect } from 'react';

const DataFetcher = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    // Side effect: fetching data
    fetch('/api/data')
      .then((response) => response.json())
      .then((data) => setData(data));
  }, []);  // Empty array ensures this runs only once after the first render

  return <div>{data ? <p>{data}</p> : <p>Loading...</p>}</div>;
};

export default DataFetcher;
```

### Explanation:
- **Effect Function**: The function inside `useEffect` is the side effect function. In this case, it's fetching data from an API.
- **Dependency Array**: `[]` is the second argument to `useEffect`. This tells React to run the effect **only once** after the first render, similar to `componentDidMount` in class components.

### `useEffect` with Dependencies

If you want the effect to run whenever specific state or props change, you can pass them in the dependency array.

```jsx
import React, { useState, useEffect } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `Count: ${count}`;  // Side effect: update the document title
  }, [count]);  // The effect runs only when `count` changes

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};

export default Counter;
```

### Explanation:
- **Dependency Array `[count]`**: This ensures the effect runs only when the `count` value changes. If no dependencies are provided, the effect runs after every render.
  
### Cleanup in `useEffect`

If your effect creates any side effects that need cleanup (e.g., subscriptions or timers), you can return a cleanup function from the effect.

```jsx
import React, { useState, useEffect } from 'react';

const Timer = () => {
  const [time, setTime] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => setTime(time + 1), 1000);

    // Cleanup function to clear the interval when component unmounts or before the next effect
    return () => clearInterval(interval);
  }, [time]);

  return <p>Time: {time} seconds</p>;
};

export default Timer;
```

### Explanation:
- **Cleanup**: The function returned by `useEffect` is used for cleanup. In this case, it clears the interval when the component unmounts or before the effect runs again.

---

## Summary of `useState` and `useEffect`

- **`useState`**:
  - Adds state to functional components.
  - Returns an array with the current state and a function to update it.
  - Allows you to manage multiple pieces of state.

- **`useEffect`**:
  - Handles side effects like data fetching, DOM manipulation, and subscriptions.
  - Runs after each render by default, but you can control when it runs using the dependency array.
  - Can perform cleanup operations to avoid memory leaks.

---


# Practice: Building a Simple Counter App with `useState` and `useEffect`

In this practice exercise, we will build a simple counter application that allows users to increment a counter and see the updated count. Additionally, we will update the document title each time the counter value changes, using the `useEffect` hook.

## Step-by-Step Guide

### 1. **Setup the React App**

First, ensure that you have a React app set up. If you don't have one, you can create a new React app using **Create React App**:

```bash
npx create-react-app counter-app
cd counter-app
npm start
```

### 2. **Create the Counter Component**

Now, let's create the counter component that will display the current count, allow the user to increment it, and update the document title.

```jsx
import React, { useState, useEffect } from 'react';

const Counter = () => {
  // Step 1: Declare a state variable to store the count value
  const [count, setCount] = useState(0);

  // Step 2: Use useEffect to update the document title when count changes
  useEffect(() => {
    document.title = `Count: ${count}`;
  }, [count]);  // This effect runs whenever the count changes

  // Step 3: Handle button click to increment the count
  const incrementCount = () => {
    setCount(count + 1); // Updates the state with the new count value
  };

  return (
    <div>
      <h1>Counter App</h1>
      <p>Current Count: {count}</p>
      <button onClick={incrementCount}>Increment</button>
    </div>
  );
};

export default Counter;
```

### 3. **Explanation of the Code**

- **`useState` Hook**: 
  - `const [count, setCount] = useState(0);` initializes the `count` state variable with a value of `0`.
  - `setCount` is the function that updates the state, and `count` holds the current value of the state.

- **`useEffect` Hook**: 
  - The `useEffect` hook is used to update the **document title** every time the `count` state changes.
  - The second argument `[count]` is a dependency array that ensures the effect runs only when `count` changes.

- **Incrementing the Count**: 
  - The `incrementCount` function is called when the button is clicked. It increments the count by `1` using the `setCount` function.

### 4. **Adding the Counter to Your App**

To display the `Counter` component, import it into your `App.js` file and render it.

```jsx
import React from 'react';
import Counter from './Counter';

const App = () => {
  return (
    <div className="App">
      <Counter />
    </div>
  );
};

export default App;
```

### 5. **Running the App**

Once you've added the `Counter` component, you can start your app using `npm start` or `yarn start`. The app will render the `Counter` component, displaying the current count and a button to increment the count.

### 6. **Final Result**

When you click the "Increment" button:
- The counter will increase by `1` with each click.
- The document title will update to reflect the current count, like `"Count: 1"`, `"Count: 2"`, etc.

---

## Final Code:

Here is the final code for the `Counter` component:

```jsx
import React, { useState, useEffect } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `Count: ${count}`;
  }, [count]);

  const incrementCount = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <h1>Counter App</h1>
      <p>Current Count: {count}</p>
      <button onClick={incrementCount}>Increment</button>
    </div>
  );
};

export default Counter;
```

---

## Summary

- **`useState`**: Manages the count state in the functional component.
- **`useEffect`**: Updates the document title each time the count changes.
- The app provides a button to increment the count and automatically reflects this change in both the UI and the document title.

This simple counter app demonstrates how to use React's `useState` and `useEffect` hooks effectively in functional components.
