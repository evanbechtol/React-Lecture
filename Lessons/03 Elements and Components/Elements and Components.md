# Elements and Components

Learn about the building blocks that make a React application work, and their differences.

## Table of contents

* [Elements](#elements)
* [Components](#components)
    * [Stateless Components](#stateless-components)
    * [Stateless and Stateful Components](#stateless-and-stateful-components)
    * [Component Composition](#component-composition)

### <a name="elements">Elements</a>

* Elements are the smallest building block of any React application
* They are plain objects, making them much lighter and quicker to render, than components
* Element make up components, as part of application composition

#### What does an element look like?

    const element = <h1>Hello, world!</h1>;
    ReactDOM.render(element, document.querySelector("#root"));

It's really that simple! In the above example, we create an element, and then render it to a DOM node identified by the
id "root".

#### Updating rendered Elements

* React Elements are *immutable*. Once they are rendered, their children and attributes are unable to be changed.
* React will only update what is necessary, in order to bring the DOM to the desired state. This is done by comparing
  the previous state, and the updated state of the node. React then identifies what changes must be made in order to
  bring the UI to the correct state.
    * **React will still create the entire element**, but only apply the required updates to the DOM.

### <a name="components">Components</a>

Components are essentially just JavaScript functions or classes, which return React elements. They separate/encapsulate
related logic and functionality from other parts of the application, in order to improve reusability, testability, and
readability (among other things).

#### A component should...

* Avoid creating side effects by modifying the environment outside itself. This is a principle
  of <a href="https://opensource.com/article/17/6/functional-javascript" target="_blank">functional programming</a>,
  which is an important aspect of React.
* Always return the same output, given the same input.
* Never attempt to modify its properties. Instead, it should modify its own internal state.

#### <a name="stateless-and-stateful-components">Stateless and Stateful Components</a>

Stateless components, also known as container or presentational components, only differ from stateful components in that
they do not utilize an internal state. This means that stateful components are keeping track of changes to their data,
which stateless components present the data that is provided to them via their "props".

An example of a **stateless component** could be a card or tile header:

    import React from "react";

    const CardHeader = (props) => {
        return (
            <div className="header__container">
                <h1 className="header__title">{props.title}</h1>
                <small className="header__subject">{props.subject}</small>
            </div>
        );
    };

    export default CardHeader;

In the example above, we are creating a stateless component, which will only present the data that is passed in. We do
not have any internal state, and we are not modifying anything in the component.

Now let's take a look at an example of a **stateful component:**

    import React, {useState} from "react";

    const Counter = (props) => {
        const [count, setCount] = useState(0);

        const handleClickCount = (e) => setCount(count++)

        return (
            <div className="counter__container">
                <p className="counter__count">{count}</h1>
                <button onClick={handleClickCount}>Increase Count</button>
            </div>
        );
    };

    export default Counter;

In that example, we initialize an internal state with the call to `useState`. Don't worry if you haven't seen this
before, it's a React Hook (we'll get more into hooks in another section). `useState` is a function call that returns two
properties:

* The item in the first index is the current value of the state variable
* The second item is an updater function. We will call this function each and every time we need to make an update to
  our state variable.
    * **IMPORTANT:** Whenever you call the updater function, it will *overwrite* the previous state. This needs to be
      taken into consideration when updating your variables. Specifically in the case where your variable is an object.

#### <a name="component-composition">Component Composition</a>

The intent of creating your components is to use them inside other components. Our components encapsulate and separate
related-functionality from other pieces of the application, make it easier to read, and work with overall. Component
composition allows us to pass React components *into* other React components. You can think of component composition as
creating components which are more generic at a high-level, and use specialized components inside them.

One such example is creating a container component, which can accept child components. Those child components are
accessed from the container component through a special prop called `children`. Let's take a look at how this works:

    import React from "react";

    const Card = ( props ) => {
      return (
        <div className="card">
          {props.children}
        </div>
      );
    };

    const MyApp = ( props ) => {
      return (
        <Card>
          <h1>Card header</h1>
          <div>
            <p>
              I can put anything here, and it will be accessible in the
              card by accessing props.children
            </p>
          </div>
        </Card>
      );
    };

export default App;

    export default MyApp;

Here, we are creating a *very* basic card component. Imagine that this card has some styles that we wish to reuse, and
we just want to accept whatever the user puts into this card, then render it.

We then use our card, and pass in the `children` to the `Card` component, by simply writing HTMl as we normally would.
Whatever we pass in between the opening and closing tags of our component, will be passed to that component as children!

This is how we can leverage the composition model of React to make both specialized and generic components.
