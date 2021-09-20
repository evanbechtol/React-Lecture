# List and Conditional Content

Displaying lists of data, and rendering specific content, conditionally is a common pattern in any web application.
React makes it easy for us to handle both of these scenarios!

## Table of contents

* [Lists](#lists)
    * [Keys](#keys)
        * [Selecting A Good Key](#selecting-a-good-key)
* [Conditional Content](#conditional-content)

### <a name="lists">Lists</a>

You can easily create lists of components, and put them inside JSX by using curly braces `{}`. In the example below, we
can create a list of elements using the array `map()` function.

```javascript
import React from "react";

const ListComponent = () => {
    const data = [
        {id: 1, name: "Evan", age: 31},
        {id: 2, name: "Morgan", age: 30},
        {id: 3, name: "Alex", age: 26},
        {id: 4, name: "Taylor", age: 30}
    ];

    /* 
    This is an array of elements
    
    IMPORTANT: Take note of the key attribute! We'll talk about the 
    significance in the next section
     */
    const listOfDataElements = data.map(elem => {
        return (
            <li key={elem.id}>
                <h3>{elem.name}</h3>
                <p>Age: {elem.age}</p>
            </li>
        );
    });

    return (
        <ul>
            {listOfDataElements}
        </ul>
    );
};

export default ListComponent;
```

#### <a name="keys">Keys</a>

Keys are used by React to identify which items in a list have changed, been added, or removed. They are important
because they provide a stable identity to each element. We add a key to a list element by using the `key` attribute on
the element.

#### <a name="selecting-a-good-key">Selecting A Good Key</a>

It's recommended to use a unique value for the key, such as an ID.

> **IMPORTANT:** You should only use the index of the list element, as the key, as a last resort.
>
> Using the index of the element as a key can cause performance issues and cause data
> to be incorrectly mapped to the wrong list elements. For example, if we have a list of 3 items
> and we add an item to the list, the index for an item could now reference an entirely different element.

### <a name="conditional-content">Conditional Content</a>

It's very common to only want to render content when specific conditions are met. For example, you may need to display
different content depending on whether the user is authenticated or not.

```javascript
const LoginButton = (props) => {
    return (
        <button onClick={props.onClick}>
            Login
        </button>
    );
};

const LogoutButton = (props) => {
    return (
        <button onClick={props.onClick}>
            Logout
        </button>
    );
};

const LoginControl = (props) => {
    const [isLoggedIn, setIsLoggedIn] = useState(false);

    const handleLoginClick = () => {
        setIsLoggedIn(true);
    };

    const handleLogoutClick = () => {
        setIsLoggedIn(false);
    };

    const button = isLoggedIn
        ? <LogoutButton onCick={handleLogoutClick}/>
        : <LoginButton onCick={handleLoginClick}/>

    return (
        <div>
            <h1>Hello, World!</h1>
            {button}
        </div>
    );
};

export default LoginControl;
```

#### Preventing Components From Rendering

Often times, we want to prevent a component from rendering. We can achieve this by having a component return `null`
instead of the component JSX. This is a very common pattern for components; toasts, warning messages, modals/dialogs.

Let's take a look at an example below:

```javascript
import Post from "../Post/Post";
import {useEffect, useState} from "react";
import httpService from "../../services/httpService";

const Feed = (props) => {
    const [refreshFeed, setRefreshFeed] = useState(true);
    const [posts, setPosts] = useState([]);
    const [isLoading, setIsLoading] = useState(false);

    useEffect(() => {
        setIsLoading(true);
        setTimeout(() => {
            httpService.get("https://jsonplaceholder.typicode.com/posts")
                .then(response => {
                    setPosts(response.data);
                    console.log(response.data);
                })
                .catch(err => {
                    console.error(err);
                })
                .finally(() => setIsLoading(false));
        }, 2000);
    }, [refreshFeed]);

    const ListOfPosts = () => {
      return !posts.length 
          ? "No posts to display"
          : posts.map(post => {
              return (
                  <div key={post.id} className="feed__post">
                      <Post post={post}/>
                  </div>
              )
          });
    };
    
    return (
        <div className="feed__container justify-center align-content-center">
            {
                isLoading
                    ? "Loading...."
                    : <ListOfPosts />
            }
        </div>
    );
};

export default Feed;
```

In the example above there is quite a bit going on. Let's break it down step-by-step:

    1. We retrieve some data from an API
    2. Create a list of elements
        a. If the list has at least one element, we render that list
        b. Else, we return "No posts to display" 
    3. Conditionally render the main content
        a. If `isLoading` is true, we render some text, "Loading..."
        b. Else, we render the content of `<ListOfPosts/>`