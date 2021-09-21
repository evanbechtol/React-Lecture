# JSX ⚛

JSX powers our React applications and is a core technology for how React is able to provide some of the functionality
that it does. We are going to dive into what JSX is, the rules, and some tricks to mastering it!

## Table of contents

* [What is JSX?](#what-is-jsx)
* [Rules of JSX](#rules-of-jsx)
    * [01. Tags Are Elements](#tags-are-elements)
    * [02. JSX Children Are Child Elements](#children-are-child-elements)
    * [03. Booleans, Null, and Undefined Are Ignored](#booleans-null-and-undefined-ignored)
    * [04. Attributes Are Props](#attributes-are-props)
    * [05. JSX Prevents Injection Attacks](#prevents-injection-attacks)

### <a name="what-is-jsx">What is JSX?</a>

JSX is an HTML-like syntax used inside of React. It extends standard ECMAScript, so that we can write what looks like
HTML, inside of JavaScript/React code. It is used by preprocessors, like Babel, to transform what we provide it into
JavaScript to be parsed by the JavaScript engine.

Whenever we write JSX, it is parsed into a series of calls to `React.creteElement`, and our React element objects are
created. React then takes those objects and build the Virtual DOM (vDOM).

Don't think of JSX as a template, instead view it as a special or alternative JavaScript syntax that has to be compiled
into JavaScript (similar, in a way, to Typescript).

### <a name="rules-of-jsx">Rules of JSX</a>

Before you get started writing JSX, there are a few things that you should understand about it.

#### <a name="tags-are-elements">01. Tags Are Elements</a>

JSX tags map to calls to `React.createElement()`. Because of this, we need a way to differentiate between common HTML
tags, and our custom React Components/Elements.

> **REMEMBER:** Our React elements are just JavaScript objects!

The convention we use is:

* Use lowercase `<tags />` to create DOM elements

```javascript
const domElement = <h1>Hello, world!</h1> 
```

* Use capitalized `<Tags />` for component elements

```javascript
const HelloWorld = () => domElement;
const helloWorldElement = <HelloWorld/>
```

#### <a name="children-are-child-elements">02. JSX Children Are Child Elements</a>

Nesting JSX elements is possible, and these elements are called children. Children can have different types, so it is
possible to use a combination of string literals, expressions, and other elements in combination with one another.

```javascript
const MyComponent = (props) => {
    const listOfNumbersElements = [1, 2, 3].map(item => <li>Item {item}</li>);

    return (
        <div>
            <h1>Here is a list:</h1>
            This is a string literal

            {listOfNumbersElements}
        </div>
    );
};
```

#### <a name="booleans-null-and-undefined-ignored">03. Booleans, Null, and Undefined Are Ignored</a>

`false`, `null`, `undefined`, and `true` are valid children. JSX just doesn't render these children. We take advantage
of this in React to conditionally render content.

```javascript
const MyComponent = (props) => {
    // We added a variable that can be used to conditionally render content
    // When set to true, it will render the list
    const shouldShowItems = false;
    const listOfNumbersElements = [1, 2, 3].map(item => <li>Item {item}</li>);

    return (
        <div>
            <h1>Here is a list:</h1>
            {shouldShowItems && listOfNumbersElements}
        </div>
    );
};
```

#### <a name="attributes-are-props">04. Attributes Are Props</a>

Attributes in JSX are a bit different from HTML. One such example is the `class` attribute. In HTML this is fine. But in
JavaScript, `class` is a reserved word. Therefore, when we want to apply a class to an element, we must use `className`.

> **IMPORTANT:** Because JSX is closer to JavaScript than to HTML, ReactDOM uses camelCase naming convention instead of
> HTML attribute names.

You can specify attributes using string literals, or curly braces:

```javascript
const elem = <div className="my-class">...</div>

const imgElem = <img src={user.avatarUrl}/>
```

We can then access these attributes from our elements via their `props`.

```javascript
const MyComponent = (props) => {
    return (
        <div>
            <h1>{props.title}</h1>
            <p>{props.content}</p>
        </div>
    );
};

const App = () => {
    const someLongText = "asdasdasdasdasd";
    return (
        <div>
            <MyComponent title="Hello, World!" content={someLongText}/>
        </div>
    );
};
```

#### <a name="prevents-injection-attacks">05. JSX Prevents Injection Attacks</a>

The default behavior of ReactDOM is to escape any values that are inside our JSX. Because ReactDOM is interacting with
the DOM for us, this means that we don't have to worry about Cross-site Scripting attacks (XSS).
