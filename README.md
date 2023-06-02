# use-context-selector-v2: Solving Rerender Issues

This custom hook aims to address a common problem encountered when using React context. By default, when a component consumes context using `useContext`, any changes to the context will cause the component to rerender. This behavior can lead to unnecessary rerenders, especially when the component only relies on a single state variable or a specific function from the context.

Inspired by Redux selectors, this select hook provides a solution to this issue. It allows you to selectively watch and import only the required state variables or functions from the context. By doing so, the component will only rerender when the specifically imported state or function changes, optimizing performance and reducing unnecessary rerenders.

With this select hook, you can achieve the same benefits as using Redux selectors in a React context. It offers granular control over which parts of the context your component depends on, ensuring efficient updates and improving overall performance.

By adopting this hook in your application, you can effectively overcome the rerender problem associated with using React context. The select hook behaves similar to Redux selectors, enabling you to watch specific context elements and trigger rerenders only when necessary.

Make the most out of this select hook and enjoy optimized rendering in your React components that consume context!

## Installation

Before using this context, make sure you have the `use-context-selector-v2` package installed in your project. You can install it by running the following command:

```bash
npm install use-context-selector-v2
```

## Usage

To create and use the context in your React application, follow these steps:

1.  Import the necessary dependencies:

    ```js
    import React, { useState } from "react";
    import { createContext } from "use-context-selector-v2";
    ```

2.  Create the context:

    ```js
    export const Context = createContext(context);
    ```

3.  Create a provider component:

    ```js
    export function ContextProvider(props) {
      const [count, setCount] = useState(0);
      const [text, setText] = useState("");

      return (
        <Context.Provider
          value={{
            count,
            setCount,
            text,
            setText,
          }}
        >
          {props.children}
        </Context.Provider>
      );
    }
    ```

4.  Wrap your application with the provider component:

    ```js
    function App() {
      return (
        <ContextProvider>
          <ComponentA />
          <ComponentB />
        </ContextProvider>
      );
    }
    export default App;
    ```

5.  Use the context in your components:

    ```js
    import React, { memo } from "react";
    import { useContextSelector } from "use-context-selector-v2";
    import { Context } from "../../context";

    export default memo(
    function ComponentA() {
     const { count, setCount } = useContextSelector(Context, [
       "count",
       "setCount",
     ]);

     return (
         <div>
          <br />
          <br />
          <div>This is Component A: {(Math.random() * 10000).toFixed(0)}</div>
          <div>Count: {count}</div>
          <onClick={() => setCount(count + 1)}>Increment</button>
          <br />
          <br />
         </div>
       );
     },
     () => true
    );
    ```

6.  Use the context in your components:

    ```js
    import React, { memo } from "react";
    import { useContextSelector } from "use-context-selector-v2";
    import { Context } from "../../context";

    export default memo(
      function ComponentB() {
        const { text, setText } = useContextSelector(Context, (_) => ({
          // redux pattern
          text: _.text,
          setText: _.setText,
        }));

        return (
          <div>
            <div>This is Component B: {(Math.random() * 10000).toFixed(0)}</div>
            <div>Text: {text}</div>
            <input value={text} onChange={(e) => setText(e.target.value)} />
          </div>
        );
      },
      () => true
    );
    ```

## Using the Hook in Various Ways

The select hook in React allows you to conveniently access specific values from a context object. Here are several examples demonstrating different ways you can utilize the select hook in your application:

1.  Single String Approach:

```js
const count = useContextSelector(Context, "count");
const setCount = useContextSelector(Context, "setCount");
```

2. Array Approach:

```js
const [count, setCount] = useContextSelector(Context, ["count", "setCount"]);
```

3. Object Approach:

```js
const { count, setCount } = useContextSelector(Context, {
  count: 1,
  setCount: 1,
});
```

4. Redux Selectors Pattern::

```js
const { count, setCount } = useContextSelector(Context, (_) => ({
  count: _.count,
  setCount: _.setCount,
}));
```

In this pattern, you pass a function that takes the entire context object as an argument and returns an object with the desired context values. This allows for more complex logic or transformations to be applied before retrieving the values.

Additionally, the Redux Selectors Pattern can be simplified for a single context value:

```js
const count = useContextSelector(Context, (_) => _.count);
```

This concise form extracts a single value directly from the context object based on the provided function.

These examples showcase the flexibility of the select hook in accessing context values in various scenarios. Feel free to choose the method that best suits your application's needs.

## Repository

This package is hosted on GitHub. You can find the repository at [https://github.com/HussnainQuresshi/use-context-selector](https://github.com/HussnainQuresshi/use-context-selector).

Feel free to explore the repository to find more information, contribute, or report any issues you encounter.

## Acknowledgements

This package was created with the help and inspiration from the article ["Use Context Selector Demystified"](https://dev.to/romaintrotard/use-context-selector-demystified-4f8e) by Romain Trotard. The article provides valuable insights into the usage of `use-context-selector` and served as a reference during the development of this package. I would like to express my gratitude to Romain Trotard for sharing their knowledge and contributing to the community.
