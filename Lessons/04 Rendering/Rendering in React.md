# Rendering in React

So up to this point, we have an understanding of what JSX is, the differences between elements and components, and how
to use them. But how does React actually put all of this information into the DOM? How does it update the DOM at the
right time, with the right information? Those are the exact questions (and more) that we will be answering here.

Understanding how React handles rendering components and elements will help you to make your applications faster, and
avoid making mistakes which can lead to slow rendering, unexpected behavior, or bottlenecks for your end-users.

## Table of contents
* [Virtual DOM and Internals](#virtual-dom-and-internals)
* [Reconciliation](#reconciliation)
  * [Elements of Different Types](#elements-of-different-types)
  * [DOM Elements of The Same Type](#dom-elements-of-the-same-type)
  * [Component Elements of The Same Type](#component-elements-of-the-same-type)
  
### <a name="virtual-dom-and-internals">Virtual DOM and Internals</a>

React keeps a virtual representation of the DOM (VDOM) in memory. This virtual representation is kept in sync with the
actual DOM by utilizing a library called ReactDOM, and a process
called <a href="https://reactjs.org/docs/reconciliation.html" target="_blank">Reconciliation<a/>.

Because React is declarative, we are telling it what state we want the UI to be in, and let React handle getting it to
that desired state. This is why you don't have to worry about manual DOM updates with React, setting up event handlers
with `document.addEventListener()`, or manual attribute manipulation.

### <a name="reconciliation">Reconciliation</a>

Reconciliation is the process by which React determines what needs to be updated to bring the DOM to the desired state.
It utilizes a diffing algorithm, which compares two tress. Starting at the root node, it will determine what needs to be
done based on the type of element in that node. It will then recurse through the children of the node, and compare them.

#### <a name="elements-of-different-types">Elements of Different Types</a>

For example, let's say that you have made an update to state or props for a component:

```javascript
// Old Component
<div>
  <h1>Hello, World!</h1>
</div>

// New Component
<span>
  <h1>Hello, World!</h1>
</span>
```

In this example, because the root nodes of our component are a different type (one is a div, the other is a span), the
component will be torn down by calling the React lifecycle method `componentWillUnmount()`. This means that the entire
tree is torn down, and rebuilt. As you could imagine, this can be an expensive process if the component becomes
complicated, or this component is being rendered as part of a list of items.

#### <a name="dom-elements-of-the-same-type">DOM Elements of The Same Type</a>

When two React DOM elements of the same type are compared, their attributes are compared instead. This alleviates the
need to tear down the entire node, and instead only updates the changed attributes. This is a much more efficient
update! Once the reconciliation is done on those nodes, the algorithm recurses on the child nodes.

#### <a name="component-elements-of-the-same-type">Component Elements of The Same Type</a>

When a component updates, the instance remains the same (think of your state persisting inside your component between
renders). React will update the props of the underlying component instance to match the new element and
calls `componentDidUpdate()`. This triggers a call to the `render()` method, which invokes our reconciliation process
and thus the diffing algorithm to execute.
