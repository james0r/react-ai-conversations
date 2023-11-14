React Hooks are a feature introduced in React version 16.8 that allow you to use state and other React features without writing a class. They are JavaScript functions that let you "hook into" React state and lifecycle features from function components [Source 3](https://legacy.reactjs.org/docs/hooks-overview.html).

There are two main rules for using hooks in React:

1. **Only call hooks at the top level**: Don't call hooks inside loops, conditions, or nested functions. Instead, always use hooks at the top level of your React function, before any return keyword [Source 2](https://www.freecodecamp.org/news/the-beginners-guide-to-react-hooks/).

2. **Only call hooks from React function components or custom hooks**: You should never call hooks from regular JavaScript functions. However, you can call hooks from React functional components and custom hooks [Source 2](https://www.freecodecamp.org/news/the-beginners-guide-to-react-hooks/).

These rules are enforced by the ESLint plugin called `eslint-plugin-react-hooks`. You can add this plugin to your project to enforce these rules [Source 0](https://legacy.reactjs.org/docs/hooks-rules.html).

```javascript
// Your ESLint configuration
{
 "plugins": [
   // ...
   "react-hooks"
 ],
 "rules": {
   // ...
   "react-hooks/rules-of-hooks": "error", // Checks rules of Hooks
   "react-hooks/exhaustive-deps": "warn" // Checks effect dependencies
 }
}
```

React also provides a few built-in hooks like `useState`, `useEffect`, and others. You can also create your own custom hooks to reuse stateful behavior between different components [Source 3](https://legacy.reactjs.org/docs/hooks-overview.html).

For example, a custom hook could look like this:

```javascript
//useFetch.js
import { useState, useEffect } from "react";
export function useFetch(url) {
   const [data, setData] = useState(null);
   const [error, setError] = useState("");
   useEffect(() => {
       fetch(url)
       .then(res => {
           if (!res.ok) {
           throw Error("something wrong, çould not connect to resource");
       }
       setData(res.json());
       })
       .then(() => {
       	setError("");
       })
       .catch( error => {
           console.warn(`sorry an error occurred, due to ${error.message} `);
           setData(null);
           setError(error.message);
       });
   }, [url]);
   return [data, error];
}
```

This custom hook `useFetch` can be used anywhere in your app simply by importing the function and passing an API path as an argument [Source 2](https://www.freecodecamp.org/news/the-beginners-guide-to-react-hooks/).