# Elements and Components

Learn about the building blocks that make a React application work, and their differences.

## Table of contents

* [Elements](#elements)
* [Components](#components)
    * [Stateless Components]()
    * [Stateful Components]()

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
