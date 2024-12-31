### **React Hooks**

#### **useRef: Handling References and DOM Manipulation**

The `useRef` hook allows you to create a mutable reference that persists across renders. It is commonly used for:

1. Accessing and manipulating DOM elements directly.
2. Storing mutable values that do not trigger a re-render when changed.

---

#### **Key Features of `useRef`**
- Does not cause a component to re-render when updated.
- Can hold any mutable value or DOM reference.

---

#### **Example: Manipulating a DOM Element**

```jsx
import React, { useRef } from "react";

const FocusInput = () => {
  const inputRef = useRef<HTMLInputElement>(null);

  const handleFocus = () => {
    if (inputRef.current) {
      inputRef.current.focus(); // Focus the input element
    }
  };

  return (
    <div>
      <input ref={inputRef} placeholder="Type here..." />
      <button onClick={handleFocus}>Focus Input</button>
    </div>
  );
};

export default FocusInput;
```

---

#### **useMemo & useCallback: Optimizing Performance**

Both `useMemo` and `useCallback` are used for optimization in React by memoizing values or functions to avoid unnecessary re-computations or re-creations.

---

### **useMemo**

The `useMemo` hook memoizes a computed value, so it is only recomputed when its dependencies change. It is useful for optimizing expensive computations.

---

#### **Example: Memoizing a Value**

```jsx
import React, { useState, useMemo } from "react";

const ExpensiveComputation = () => {
  const [count, setCount] = useState(0);
  const [otherState, setOtherState] = useState(0);

  const computeExpensiveValue = (num) => {
    console.log("Computing...");
    return num * 10;
  };

  const memoizedValue = useMemo(() => computeExpensiveValue(count), [count]);

  return (
    <div>
      <p>Expensive Value: {memoizedValue}</p>
      <button onClick={() => setCount((prev) => prev + 1)}>Increment Count</button>
      <button onClick={() => setOtherState((prev) => prev + 1)}>
        Update Other State
      </button>
    </div>
  );
};

export default ExpensiveComputation;
```

---

### **useCallback**

The `useCallback` hook memoizes a function to ensure it is not re-created on every render unless its dependencies change. This is particularly useful when passing functions to child components to prevent unnecessary re-renders.

---

#### **Example: Memoizing a Function**

```jsx
import React, { useState, useCallback } from "react";

const Button = React.memo(({ onClick, label }) => {
  console.log(`Rendering ${label} button`);
  return <button onClick={onClick}>{label}</button>;
});

const UseCallbackExample = () => {
  const [count, setCount] = useState(0);
  const [otherState, setOtherState] = useState(0);

  const increment = useCallback(() => setCount((prev) => prev + 1), []);

  return (
    <div>
      <p>Count: {count}</p>
      <Button onClick={increment} label="Increment" />
      <button onClick={() => setOtherState((prev) => prev + 1)}>
        Update Other State
      </button>
    </div>
  );
};

export default UseCallbackExample;
```

---

### **When to Use**

| **Hook**      | **Use Case**                                                                 |
|---------------|------------------------------------------------------------------------------|
| `useRef`      | Accessing/manipulating DOM elements or storing mutable values.              |
| `useMemo`     | Optimizing expensive computations to prevent unnecessary recalculations.    |
| `useCallback` | Memoizing functions to prevent re-creation and unnecessary re-renders.      |

These hooks are essential for optimizing React applications by reducing unnecessary computations and improving rendering performance.


---

# **React Context API**

The React Context API is a powerful feature for managing and sharing state across components in a React application without the need for "props drilling" (passing props down through multiple levels of components). It provides a way to create global state and access it directly from any component in the tree.

---

### **Why Use Context API?**

- Avoids "props drilling," where data must be passed down through several nested components, even if only the child components need the data.
- Simplifies state management for data that needs to be accessible by multiple components (e.g., user authentication, themes, or language preferences).

---

### **How to Use Context API**

1. **Create Context**  
   Use `React.createContext` to create a new Context object.

   ```jsx
   import React from "react";

   const ThemeContext = React.createContext("light"); // Default value: "light"
   ```

2. **Provide Context**  
   Use the `Provider` component to supply the context value to the component tree.

   ```jsx
   import React from "react";

   const ThemeProvider = ({ children }) => {
     const theme = "dark"; // Example context value
     return <ThemeContext.Provider value={theme}>{children}</ThemeContext.Provider>;
   };

   export { ThemeContext, ThemeProvider };
   ```

3. **Consume Context**  
   Access the context value using:
   - The `useContext` hook in functional components.
   - The `Context.Consumer` component in class components or older implementations.

   ```jsx
   import React, { useContext } from "react";
   import { ThemeContext } from "./ThemeProvider";

   const ThemedComponent = () => {
     const theme = useContext(ThemeContext);
     return <div>The current theme is {theme}</div>;
   };
   ```

---

### **Example: Sharing State Without Props Drilling**

```jsx
import React, { useState, useContext } from "react";

// Create Context
const UserContext = React.createContext(null);

const UserProvider = ({ children }) => {
  const [user, setUser] = useState({ name: "John", age: 30 });
  return (
    <UserContext.Provider value={{ user, setUser }}>
      {children}
    </UserContext.Provider>
  );
};

const UserInfo = () => {
  const { user } = useContext(UserContext);
  return (
    <div>
      <p>Name: {user.name}</p>
      <p>Age: {user.age}</p>
    </div>
  );
};

const UpdateUser = () => {
  const { setUser } = useContext(UserContext);
  return (
    <button onClick={() => setUser({ name: "Jane", age: 25 })}>
      Update User
    </button>
  );
};

const App = () => (
  <UserProvider>
    <h1>React Context API Example</h1>
    <UserInfo />
    <UpdateUser />
  </UserProvider>
);

export default App;
```

---

### **Key Points**
- **Provider**: Supplies the context value.
- **Consumer**: Retrieves the context value (via `useContext` or `Consumer`).
- Context is suitable for:
  - Themes (dark/light mode).
  - User authentication and profile data.
  - Application-wide settings (e.g., localization, language).
  
For complex state management, consider combining Context with state management libraries like Redux or Zustand.
