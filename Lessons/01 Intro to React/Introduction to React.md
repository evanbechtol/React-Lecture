# Introduction to React ⚛

Learn what React is, why we use it, and a high-level overview of how it works.

## Table of contents

* [What is React?](#what-is-react)
* [Imperative vs Declarative Programming](#imperative-vs-declarative-programming)
* [Library vs Framework](#library-vs-framework)
* [JSX](#jsx)
* [Components](#components)
* [Rendering](#rendering)

### <a name="what-is-react">What is React?</a>

From the [Official React documentation](https://reactjs.org/tutorial/tutorial.html):
> React is a **declarative**, efficient, and flexible JavaScript **library** for building user interfaces. It lets you compose complex UIs from small and isolated pieces of code called “components”.

React's power comes from allowing us to create reusable components, composing those components, and handles rendering
those components and an efficient and optimized way (we'll get more into that in a bit).

Because React is (partially) built
with [functional programming](https://opensource.com/article/17/6/functional-javascript)
concepts in mind, and we are going to making functional components, we need to keep FP concepts in mind. A side effect
can be any change from inside the component, which alters the global environment, or anything outside the scope of a
component. *Side effects can cause bugs, and make testing difficult.*

> **What is a pure function?**
>
>* Its return value is only determined by its input values
>* Its return value is always the same for the same input values

### <a name="imperative-vs-declarative-programming">Imperative vs Declarative Programming</a>

![Imperative versus declarative programming](../../assets/images/imperative%20vs%20declarative.jpeg)

Imperative code uses statements and declarative code uses expressions. Expressions evaluate to a value while statements
tell the computer to do something.

In **imperative programming**, your code is based on statements that change the program state by telling the computer
how to do things. In other words, your code is based on defining variables and changing the values of those variables.

In **declarative programming**, your code is based on expressions that evaluate their result based on their input by
telling the computer what you want.

Expressions focus on taking input and providing output while relying only on the input itself. Such expression is called
pure function in functional programming.

Statements don’t necessarily need any input or output, they can just call other functions or change some value somewhere
outside their internal state. In declarative functional programming, changing the external state or causing external
actions such as console log, saving a file, or loading database record is called a side effect. Changing a value of
anything is called a mutation. In functional programming, we prefer to always stick to constants.

When we talk about imperative code telling the computer how to do things, we mean that it focuses on creating statements
that tell the computer how to do its thing.

When we talk about declarative code focusing on telling a computer what to do, we mean working with expressions that map
inputs into outputs.

### <a name="library-vs-framework">Library vs Framework</a>
![Library versus framework](../../assets/images/library%20vs%20framework.png)

### <a name="jsx">JSX</a>

### <a name="components">Components</a>

### <a name="rendering">Rendering</a>
