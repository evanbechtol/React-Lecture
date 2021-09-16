# Hooks

Hooks are a powerful feature that you will need to know in order to effectively create functional components in react.

## Table of contents

* [What are hooks?](#what-are-hooks)
* [Rules of hooks](#rules-of-hooks)
* [State Hook](#state-hook)
* [Effect Hook](#effect-hook)

### <a name="what-are-hooks">What are hooks?</a>

Hooks allow you to use state and other features of React without being required to write a class component. They are
functions that "hook" into React state and lifecycle features from functional components. They were introduced to React
in version 16.8.

Without hooks, we had to rely on different patterns of component composition and development to achieve the same
results. Hooks allow us to extract stateful logic from a component, so that it can be tested independently and reused!
This also means that we can reuse stateful logic without having to change our component hierarchy (we don't need to
create higher-order components to have state anymore).

#### Common naming convention for hooks

All hooks in react start with `use`, followed by a descriptor word. For example the hook that provides state to our
functional components is called `useState`. We can even make our own custom hooks, but it is important that our custom
hooks follow this same naming convention.

### <a name="rules-of-hooks">Rules of hooks</a>

Before you get started, there are some very important rules that you must follow when using hooks.

#### 1) Only call hooks at the top level

Don't call them inside of loops, conditions, or nested functions. React needs the order of the calls to hooks to be the
same for each render. This is how it preserves state between multiple hook calls. If we use hooks inside conditional
statements, the order can be different each render depending on the state of our component.

#### 2) Only call hooks from react functions

This just means that you can't call hooks from normal JavaScript functions. They should be called from a React
functional component, or from a custom React hook.

### <a name="state-hook">State hook</a>

The `useState` hook is what provides state to our component, and persists values between component renders. A call to
the `useState` hook returns a pair: the current state value, and a function that lets you update that value. You can
have as many states as you want, and it is very common for there to be a state for each specific data point, although
the implementation is entirely up to you.

> **IMPORTANT:**
> Calling the updater method will *always* overwrite the previous state value. This is necessary to keep in mind when
> updating state values, such as objects and arrays.
>
> We'll show an example of how to handle that soon

```javascript
import { useState } from "react";

const MyComponent = ( props ) => {
  const [ count, setCount ] = useState( 0 ); // This is how we initialize a state
  
  const handleButtonClick = (e) => setCount(count++);
  
  return (
    <div>
      <p>The count is: {count}</p>
      <button onClick={handleButtonClick}>Click Me</button>
    </div>
  );
};

export default MyComponent;
```

### <a name="state-hook">Effect hook</a>
