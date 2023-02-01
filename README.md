# Learning React

Using [official](https://reactjs.org/docs/) documentation

## Installation

- Before starting make sure your systems has node, npm, IDE(VSCode), git.
- Steps for creating a new react app [here](https://reactjs.org/docs/create-a-new-react-app.html).
- Create a new react app by `npx create-react-app learning-react`.

## Main concepts

### 1. Hello World

- A simple hello world app using react.
- `git checkout hello-world`.
- Everything starts with `public/index.html` in `<div id="root"></div>`
- In `src/index.js` the `ReactDOM.createRoot()` creates a root of the document.
- `root.render()` is used to render the react contents in the html file.

### 2. Introducing JSX

- JSX produces React "elements".
- `const element = <h1>Hello, world!</h1>` is a combination of JavaScript and HTML.
- JSX is a syntax extension to JavaScript, JSX produces react "elements".

#### Why JSX?

- React embraces the fact that rendering logic is inherently coupled with other UI logic:
- React separates concerns with loosely coupled units called “components” that contain both.
- React doesn’t require using JSX, it helps as a visual aid when working with UI inside the JavaScript code, allows react to show useful error ad warning messages.

#### Embedding Expressions in JSX

- Use curly brace to use it inside JSX

  ```jsx
  const name = "Sinku Kumar";
  const element = <h1>Hello, {name}</h1>;
  ```

- You can put any valid JavaScript expression inside the curly braces in JSX.

  ```jsx
  function formatName(user) {
    return user.firstName + " " + user.lastName;
  }
  const user = {
    firstName: "Harper",
    lastName: "Perez",
  };
  const element = <h1>Hello, {formatName(user)}!</h1>;
  ```

##### Warning:

Since JSX is closer to JavaScript than to HTML, React DOM uses camelCase property naming convention instead of HTML attribute names.

For example, class becomes className in JSX, and tabindex becomes tabIndex.

#### JSX is an Expression Too

- After compilation, JSX expression become regular JavaScript function calls and evaluate to JavaScript objects.

  ```jsx
  function getGreeting(user) {
    if (user) {
      return <h1>Hello, {formatName(user)}!</h1>;
    }
    return <h1>Hello, Stranger.</h1>;
  }
  ```

### Specifying Attributes with JSX

- You may use quotes to specify string lterals as attributes:

  ```jsx
  const element = <a href="https://www.reactjs.org">link</a>;
  ```

- You may also use curly braces to embed a JavaScript expression in an attribute:
  ```jsx
  const element = <img src={user.avatarUrl}></img>;
  ```
- Don't get confused with `{element}` or `"{element}"`

#### Specifying Children with JSX

- If a tag is empty, you may close it immediately with />, like XML.

  ```jsx
  const element = <img src={user.avatarUrl} />;
  ```

- JSX tags may contain children.
  ```jsx
  const element = (
    <div>
      <h1>Hello!</h1>
      <h2>Good to see you here.</h2>
    </div>
  );
  ```

#### JSX Prevents Injection Attacks

- It is safe to embed user input in JSX.
- By default, React DOM escapes any values embedded in JSX before rendering them.
- Everything is converted to a string before being rendered.

  ```jsx
  const title = response.potentiallyMaliciousInput;
  //This is safe:
  const element = <h1>{title}</h1>;
  ```

#### JSX Represents Objects

- Babel compiles JSX down to `React.createElement()` calls.
- Below two examples are identical
  ```jsx
  const element = <h1 className="greeting">Hello, world!</h1>;
  ```
  ```jsx
  const element = React.createElement(
    "h1",
    { className: "greeting" },
    "Hello, world!"
  );
  ```
- `React.createElement()` performs a few checks to help you write bug-free code but essentially it creates an object like this

  ```jsx
  // Note: this structure is simplified
  const element = {
    type: "h1",
    props: {
      className: "greeting",
      children: "Hello, world!",
    },
  };
  ```

##### Tip:

React recommends using the “Babel” language definition for your editor of choice so that both ES6 and JSX code is properly highlighted.

### 3. Rendering Elements

- Elements are the smallest building blocks of React apps.
- An element desribes what you want to see on the screen.

#### Rendering an Element into the DOM

- Same as rendering hello world.

#### Updating the Rendered Element

- React elements are immutable. The only way to update the UI is to create a new element, and pass it to `root.render()`.

  ```jsx
  const root = ReactDOM.createRoot(document.getElementById("root"));

  function tick() {
    const element = (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {new Date().toLocaleTimeString()}.</h2>
      </div>
    );
    root.render(element);
  }

  setInterval(tick, 1000);
  ```

##### Note:

In practice, most React apps only call root.render() once. In the next sections we will learn how such code gets encapsulated into stateful components.

We recommend that you don’t skip topics because they build on each other.

#### React Only Updates What's Necessary

- React DOM compares the element and its children to the previous one, and only applies the DOM updates necessary to bring the DOM to the desired state.
