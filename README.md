# beginners-guide-to-react

## A Beginners Guide to React Introduction

### final/01-document-create-element.html

We're using a tool called Browsersync. We're using npx to get that running. npx comes bundled with Node. If you get Node.js installed, then you can use npx. Open the dev tools in your browser to inspect the HTML code. We have two scripts in here that you don't find in the source code. That's added by Browsersync. The cool thing about Browsersync is that you don't have to manually hit the reload button, you just go ahead and change something, hit save and it will automatically reload for you. That's why we're going with Browsersync. It's really nice for this.

## Create a User Interface with Vanilla JavaScript and DOM

### setup/01-document-create-element.html

You can create a simple user interface on the web using HTML and CSS. But as soon as you want to make your application interactive, you need to use JavaScript to manipulate the DOM (Document Object Model) to listen to user events and make updates to the user interface. In this lesson we'll learn how to create a 'div' element using raw JavaScript and browser APIs.

In review, to create a user interface in JavaScript, you're going to need to have a place where you append your JavaScript-generated DOM elements. We're going to get access to that element from the document APIs. Then we'll create our own element. We'll add some properties onto that element. Then we'll append that element to our rootElement.

```html
<body>
  <div id="root"></div>
  <script type="text/javascript">
    const rootElement = document.getElementById('root')
    const element = document.createElement('div')
    element.textContent = 'Hello World'
    element.className = 'container'
    rootElement.appendChild(element)
  </script>
</body>
```

## Create a User Interface with React’s createElement API

### setup/02-react-create-element.html

React uses the same APIs to control and update the DOM that we did in the previous lesson. But it offers so much to the table that we’re going to introduce it into the project and rewrite what we’ve written to React code. Instead of creating DOM elements, we’ll create React elements and then hand those off to react-dom to handle turning those into DOM elements and putting them into the page.

If you’ve ever learned or used React before, you’re probably more familiar with JSX than React’s createElement API, but it’s important to understand the createElement API first so you understand the magic and can become a code magician yourself. Not to worry, we’ll get to JSX soon enough!

To use React to create this user interface, we're going to need to have React on the page. We can get React from npm, but there's a service called unpackage that we're going to use. If I go to unpackage.com that will show me how to use unpackage to get any file that is distributed on npm. It has these files for React. If I go to that file, then I'll see a minified version of React.

With React and ReactDOM both on the page, I can now create React elements and then use ReactDOM to render those elements to the page. The API is not exactly the same as the one that we get with document. We do get to specify the type of element as the first argument, but instead of getting the element and attaching properties to it, we specify those properties on creation as an object.

Let's take a look at what this element is. If it's not a DOM node, then what is it? We'll console.log(element), save that, and then we'll come over here to our console. We'll see that we have a $$ type of property. That's a symbol and that's something for React to know that this object is a legitimate React element. We know that the type is a div and there are a couple other properties that are used by React internally. Then this props object is what we passed as our second argument here with the children and the class name.

There's something interesting about this children prop that I want to show you here. You can write this same thing as a third argument to React.createElement by simply providing the value for the children prop. Here we can provide Hello World. Those are functionally equivalent. We can continue going on through children forever and ever. Or we could take these and use the children prop directly like this, specifying it as an array ourselves. You'll see that the result here is the same.

This also gives us the flexibility of creating additional React elements to be children. Here I could say React.createElement("span"). We could say we want no props for this span, and we want the children to be Hello and World. We have the type of span, the props are null, the children are an array of "Hello" and "World". If we expand this, we'll see props, children, and children is just another React element that itself has props. And that children is an array of two strings.

In review, to create React elements and render them to the page, you need to include React and ReactDOM, React for creating the elements and ReactDOM for rendering those elements to the page. Then we still need to get access to some element that's on the page so we can render our elements to that DOM node. Then we create our React elements and we use ReactDOM.render to render our element to the root DOM node.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script type="text/javascript">
    const rootElement = document.getElementById('root')
    const element = React.createElement('div', {
      children: React.createElement('span', null, 'Hello', ' World'),
      className: 'container'
      //children: ['Hello World', ', Welcome world']
    }, /*'Hello World', ', Welcome world'*/)

    console.log(element)
    //Output
    // $$typeof: Symbol(react.element)
    // key: null
    // props:
    // children: (2) ['Hello World', ', Welcome world']
    // className: "container"
    // [[Prototype]]: Object
    // ref: null
    // type: "div"

    ReactDOM.render(element, rootElement)

    // const element = document.createElement('div')
    // element.textContent = 'Hello World'
    // element.className = 'container'
    // rootElement.appendChild(element)
  </script>
</body>
```

## Create a User Interface with React’s JSX syntax

### setup/03-jsx.html

It’s awesome that we can interact directly with React’s createElement API to create React elements and then hand those off to ReactDOM to get them to show up on the screen. But it’s not the most ergonomic API to write our UI code in. It’s hard to track when one element starts and the next one ends.

If I were to create this same React element using JSX, I would make it like this. We'll say element is a div. Our children are Hello World. Then we had a className, which is a prop. That'll go as an attribute on our div here, with className='container'.

```jsx
const element = <div className="container">Hello World</div>
```

If we save that, we'll get a refresh. We'll get a white screen here. That's because we have a syntax error in our JavaScript. That's because this is not JavaScript code. This is JSX. The browser does not understand this natively. It needs to be compiled from this to something that the browser can understand. That's where Babel comes in.

Babel is a JavaScript compiler supporting the next generation of JavaScript as well as non-standard features like JSX. If we go to this 'Try It Out' page and then go over here and copy our code and paste it in here, then we'll see that our code is being compiled to something that's very familiar to us.

```javascript
const element = React.createElement("div", {
  className: "container"
}, "Hello World");
```

React.createElement. The type is div. Here are the props, className is container, then all of the children come hereafter. I would recommend that you spend some time playing around in this tool. Understanding how JSX is compiled will make you more effective at using JSX.

In a typical application, you're going to be using a tool that will use Babel to compile JSX to JavaScript for you. For our purposes, we're going to use Babel in the browser to get this compiling our JavaScript right here without having to install any other tools. I'm going to add a script tag here to include Babel standalone. That will compile any script tag that has the type of text/babel. Then it will create a new script tag with the compiled code with the type as text/JavaScript so that the browser can evaluate it.

With that, if I save this, we'll get Babel downloaded. It will compile our JavaScript and allow the browser to evaluate it so we can use JSX in the browser. We'll also get this warning that we're using the in-browser Babel transformer, which is not something that you'd want to do in production, but it makes it easy for us to iterate quickly right here in this index.html file. In review, what we wanted to do here was make it so that we can author our UI without using the React createElement API and instead use JSX, which is an HTML-like syntax for authoring UI.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.17.8/babel.js"></script>
  <script type="text/babel">
    const rootElement = document.getElementById('root')
    // const element = React.createElement('div', {
    //   children: ['Hello World'],
    //   className: 'container'
    // })

    const element = <div className="container">Hello World</div>

    ReactDOM.render(element, rootElement)
  </script>
</body>
```

## Use JSX effectively with React

### setup/04-jsx-tricks.html

JSX is not an entirely different language, but it is a bit of an extension to the language, so knowing how you would express certain JavaScript things within the JSX syntax is important to using JSX effectively. In this lesson we’ll explore a few different things you can do with JSX, like interpolation, composition, and spreading props. And we’ll compare these syntaxes with what is generated by babel so we have a good understanding of how this translates to regular JavaScript calls into React.createElement.

If we wanted to create a variable for 'Hello World' and we wanted to interpolate that variable's value into the 'children' position, then I'm going to go ahead and copy this. We'll make this our 'children'. Then we'll come in here and to interpolate we're going to use curly braces and put 'children' in here. Anything you put between these two curly braces can be a JavaScript expression. Whatever that expression evaluates to is the value that gets placed into this position for the React.createElement call.

```jsx
const children = 'Hello World'
const element = <div className="container">{children}</div>
```

We can do the same thing for our className. If I copy the container and make a className variable, and instead of the quotes here, we'll put curly braces to suggest to the Babel compiler that we want this value to be evaluated as an expression, then we'll pass the className variable. If we save this, then we'll get the exact same result as we had before.

```jsx
const children = 'Hello World'
const className = "container"
const element = <div className={className}>{children}</div>
```

Babel compilled

```javascript
const children = 'Hello World';
const className = "container";
const element = /*#__PURE__*/React.createElement("div", {
  className: className
}, children);
```

You can see the compiled version of the code here in our script tag where you see we have our children as a variable, our className as a variable. Our element is an assignment to React.createElement with our div. Then our object where we have className being assigned to the variable className.

We can rename this to whatever we want. We could say myClassName and then copy this and paste it in there. If we save this, we'll get a refresh. There it is, myClassName is being assigned to the className property of our object here. Then children is the same thing. We could say myChildren. Save that. We'll get a refresh and there it is, myChildren being passed as my children. When you use the curly braces, that's basically telling Babel, "Leave this alone and pass it directly as the property that you pass for the props here and for the children arguments here."

```jsx
const myChildren = 'Hello'
const worldChild = ' World'
const myClassName = "container"
const element = (
    <div className={myClassName}>
        {myChildren}
        {worldChild}
    </div>
)
```

Babel compilled

```javascript
const myChildren = 'Hello';
const worldChild = ' World';
const myClassName = 'container';
const element = /*#__PURE__*/React.createElement("div", {
  className: myClassName
}, myChildren, worldChild);
```

This allows us to be expressive with the way that we're building our UI. If we want to add another React element in here, all we need to do is add a <span>Hello</span>. Then we could do a <strong>World</strong>. Then save that, and here we go. We get Hello World. Babel is managing, compiling that down to JavaScript that the browser can execute using React APIs.

```jsx
const myClassName = "container"
const element = (
    <div className={myClassName}>
        <span>Hello</span> <strong>World</strong>
    </div>
)
```

Babel compilled

```javascript
const myClassName = "container";
const element = /*#__PURE__*/React.createElement(
    "div", 
    {className: myClassName}, 
    /*#__PURE__*/React.createElement("span", null, "Hello"), 
    " ", 
    /*#__PURE__*/React.createElement("strong", null, "World")
);
```

There's another useful JSX trick that I want to show you. Let's come back to our children: 'Hello World'. We'll just call this className. We'll change this to className. Then we'll interpolate children here. One important thing to remember is that children is just a special prop that we could provide right here. Children is children. With that it works exactly the same way as it did before, except now instead of being compiled to add additional arguments, it's just using the shortcut here as one of the props.

```jsx
const children = 'Hello World'
const className = "container"
const element = <div className={className} children={children}></div>
```

Babel compilled

```javascript
const children = 'Hello World';
const className = "container";
const element = /*#__PURE__*/React.createElement("div", {
  className: className,
  children: children
});
```

In addition, because this is JSX and not HTML, we can have self-closing tags for divs. We can save that, and this is self-closing.

```jsx
const children = 'Hello World'
const className = "container"
const element = <div className={className} children={children} />
```

Another thing we can do is if I make an object here where we have our props, we're going to make children and className part of those props. Then I can come right here, remove all of those, and I can say, "Hey, Babel, I want you to take all of these props and pass them to the React.createElement call that you create for this div." Interpolate onto this div's prop's position a spread of that prop's object.

```jsx
const children = 'Hello World'
const className = "container"
const props = { children, className }
const element = <div {...props} />
```

Babel compilled

```javascript
const children = 'Hello World';
const className = "container";
const props = {
  children,
  className
};
const element = /*#__PURE__*/React.createElement("div", props);
```

Then I can add additional props if I want to. I could say id="app-root", save that. Then in this case we're going to get the extends helper, which is basically object.assign. Then Babel is going to extend the props that we provided with the props that we're spreading. We get a single combined object for the second argument of the React.createElement call. 

```jsx
const children = 'Hello World'
const className = "container"
const props = { children, className }
const element = <div id='app-root' {...props} />
```

Babel compilled

```javascript
function _extends() { _extends = Object.assign || function (target) { for (var i = 1; i < arguments.length; i++) { var source = arguments[i]; for (var key in source) { if (Object.prototype.hasOwnProperty.call(source, key)) { target[key] = source[key]; } } } return target; }; return _extends.apply(this, arguments); }

const children = 'Hello World';
const className = "container";
const props = {
  children,
  className
};
const element = /*#__PURE__*/React.createElement("div", _extends({
  id: "app-root"
}, props));
```

Because of the way that object.assign works, if we wanted to override one of the properties in this props object, then we could do so simply by providing it after we spread those props in the props position for this element.  We can say className="not-Container". Save that. Then if we look at the compiled version, we'll see our extends for the props that come before the spread. Then we'll see that object and then we'll see another object for the props that come after the spread.

```jsx
const children = 'Hello World'
const className = "container"
const props = { children, className }
const element = <div id='app-root' {...props} className='not-container' />
```

Babel compilled

```javascript
function _extends() { _extends = Object.assign || function (target) { for (var i = 1; i < arguments.length; i++) { var source = arguments[i]; for (var key in source) { if (Object.prototype.hasOwnProperty.call(source, key)) { target[key] = source[key]; } } } return target; }; return _extends.apply(this, arguments); }

const children = 'Hello World';
const className = "container";
const props = {
  children,
  className
};
const element = /*#__PURE__*/React.createElement("div", _extends({
  id: "app-root"
}, props, {
  className: "not-container"
}));
```

Then if we look at the results under our root, we'll see we have the id of app-root and the class of not-Container. App-root because it's not getting overwritten, so it appears as is. We get the children as they are because the children are not being overwritten, but then we get the className of not-Container because we are overwriting the className that's in the props which comes before a this className. Whatever comes last is the winner in the event of a conflict like we have here.

```javascript
//The results under our root.
<div id="root">
    <div id="app-root" className="not-container">Hello World</div>
</div>
```

In review, what we learned here is that we can interpolate values with these curly braces by putting any expression between the curly braces and have that expression passed along to the React.createElement API. We also learned that we can spread props in the props position of a JSX element and those props will be combined with the other props that are provided to that element in a declarative and deterministic way.

## Render two elements side-by-side with React Fragments

### setup/05-fragments.html

In React, you can’t render two React elements side-by-side (<span>Hello</span><span>World</span>). They have to be wrapped in another element (like a <div>). This may seem like an odd limitation, but when you think about the fact that JSX is compiled to React.createElement calls, it makes sense. In this lesson we’ll take a look at that and how to side-step this limitation with React Fragments.

Let's say that instead of rendering a div with the class name container and then "Hello, World," we wanted to render two spans side by side, one that says "Hello" and the other that says "World." Let's first do this with React createElement, and then we'll see how we could do this with JSX. I'm going to make my element React.createElement span. We don't need any props. Then we'll say, "Hello." We'll need another element. We'll call this our worldElement. Let's call this one our helloElement. This one will say, "World."

How do you put two variables side by side and pass them both as the first argument? It's impossible, but if we were to do this in HTML, it would be pretty straightforward. We'd just say <span>Hello and <span>World. That would work just fine. This is straightforward to do in HTML, but it's not possible to do with React, which is why the React team created a special type of element called a React fragment. We can say React.createElement. React fragment is a type. We don't need any props for it. We'll take our helloElement, pass that as the first child, and worldElement, pass that as the second child. Then this is going to get our element that we're going to render. With that, we have the output that we're expecting. We could also add an extra child in here to give us an extra space.

```html
<body>
  <div id="root"></div>

  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">

    //const element = <div className='container' >Hello World</div>
    // <div>
    //   <span>Hello</span>
    //   <span>World</span>
    // </div>

    const helloElement = React.createElement('span', null, 'Hello')
    const worldElement = React.createElement('span', null, 'World')
    const element = React.createElement(
      React.Fragment,
      null,
      helloElement,
      ' ',
      worldElement
    )

    ReactDOM.render(element, document.getElementById('root'))
  </script>
</body>
```

Again, nobody wants to use the React.createElement API directly. Let's comment this out and see what this would look like if we wanted to do it with JSX. Our root element is this React fragment. We'll do an open bracket and say React.Fragment. We'll close that off with React.Fragment. Then we'll want to create a span for hello, so <span>Hello</span>. Then we'll do a space and then <span>World and close that off. If we save this, we're going to get the exact same output, and we're using our React.Fragment element.

Let's take a look at the compiled JSX here. You notice that we get our element with React.createElement. It's just passing React.Fragment as a first argument to React.createElement, whereas this, the tag name, is being passed as a string. The React fragment allows us to put elements side by side without having to have some sort of container element like a div. This can be useful when you're creating things like tables that have a specific structure to them.

Because this is so common to do, JSX has a special syntax for React fragments. That is to simply remove the React fragment and have an open and closing angle bracket. This is functionally equivalent to what we had before. This syntax is typically what I use whenever I need React fragments.

```jsx
const element = (
    <React.Fragment>
        <span>Hello</span> <span>World</span>
    </React.Fragment>
)
//or
const element = (
    <>
        <span>Hello</span> <span>World</span>
    </>
)
```

Babel compilled

```javascript
const element = /*#__PURE__*/React.createElement(React.Fragment, null, 
    /*#__PURE__*/React.createElement("span", null, "Hello"),
    " ",
    /*#__PURE__*/React.createElement("span", null, "World")
);
```

## Create a Simple Reusable React Component

### setup/06-custom-component.html

One of the biggest paradigm shifts that React offered to the UI ecosystem was the component model. It allows you to package up all the logic, styling, and layout of a unit of UI into a box that you can easily move around and reuse without exposing any of the implementation details of the component. You don’t have to understand how a component works internally to use it effectively. With idiomatic component architecture, rendering a component in one place won’t impact other parts of your app. In this lesson we’ll learn how to create a React component and how to use it. You’ll learn why things work the way they do and how to use this to your advantage.

So, here we have this div with the class name "container," and we have this div with the class name "message" in here that says "Hello, World!" Let's say that I wanted to have, I don't know, maybe two of those. So now we have "Hello, World!" and "Hello, World!" and then I don't want to repeat myself. So I'm going to make a constant message here that is that "Hello, World!" and we'll put that in place of here "message," just interpolate that there. Now I'm not repeating myself, which is good.

```jsx
const message = <div className='message'>Hello World</div>

const element = (
    <div className='container'>
        {message}
        {message}
    </div>
)
```

Babel compilled

```javascript
const message = /*#__PURE__*/React.createElement("div", {
  className: "message"
}, "Hello World");
const element = /*#__PURE__*/React.createElement("div", {
  className: "container"
}, message, message);
```

But what if I wanted one of these to say, "Hello, World!" and the other to say, "Welcome World!" Well, we need to parameterize this somehow, and when we do that in JavaScript, we create a function. I'll make an arrow function here, and we'll accept an object. We'll call it "props," and then whatever that props.msg or props.message value is, is what we'll interpolate into the children prop for this div that we create.

Now, instead of just putting "message" in there directly, we're going to call it with an object, and we'll use msg as "Hello, World!" and then we'll do this one msg "Welcome World!" Save that. And we get "Hello World!" and "Welcome World!" which is awesome.

```jsx
const message = (props) => <div className='message'>{props.msg}</div>

const element = (
    <div className='container'>
        {message({msg: 'Hello World'})}
        {message({msg: 'Welcome World'})}
    </div>
)
```

Babel compilled

```javascript
const message = props => /*#__PURE__*/React.createElement("div", {
  className: "message"
}, props.msg);

const element = /*#__PURE__*/React.createElement("div", {
  className: "container"
}, message({
  msg: 'Hello World'
}), message({
  msg: 'Welcome World'
}));
```

But again, this is not really ergonomic. It doesn't look very good, and one of the benefits to using JSX is the ability for our UI to resemble the declarative nature of HTML. What I'd really like to be able to do is say "message" here and then "Hello, World!" and "message." But if I try to do that, you'll notice we actually do get the "Hello, World!" but we're going to get a console warning here saying, "The tag message is unrecognized in this browser. If you meant to render a React component, start its name in an upper case letter."

```jsx
const message = (props) => <div className='message'>{props.msg}</div>

const element = (
    <div className='container'>
        <message>Hello World</message>
        {message({msg: 'Hello World'})}
        {message({msg: 'Welcome World'})}
    </div>
)
```

Babel compilled

```javascript
const message = props => /*#__PURE__*/React.createElement("div", {
  className: "message"
}, props.msg);

const element = /*#__PURE__*/React.createElement("div", {
  className: "container"
}, /*#__PURE__*/React.createElement("message", null, "Hello World"), message({
  msg: 'Hello World'
}), message({
  msg: 'Welcome World'
}));
```

If we look at the compiled version of our code, we're going to see our message function that's returning a React element, that's creating a div. And then if we come down here, we're going to see React.createElement message as a string. That's problematic because we don't want to have the message as a string to create a DOM element that is a message type element. We actually wanted to use this function, so that we can use this function to create additional React elements.

So, as the warning suggests, we need to use an upper case letter, and so if instead, we say capital "Message," then we use capital "Message" here, and let's make sure we don't get errors here. So we'll say capital "Message" for these, and we can save that.

```jsx
const Message = (props) => <div className='message'>{props.msg}</div>

const element = (
    <div className='container'>
        <Message>Hello World</Message>
        {Message({msg: 'Hello World'})}
        {Message({msg: 'Welcome World'})}
    </div>
)
```

Babel compilled

```javascript
const Message = props => /*#__PURE__*/React.createElement("div", {
  className: "message"
}, props.msg);

const element = /*#__PURE__*/React.createElement("div", {
  className: "container"
}, /*#__PURE__*/React.createElement(Message, null, "Hello World"), Message({
  msg: 'Hello World'
}), Message({
  msg: 'Welcome World'
}));
```

Now, we're no longer getting that warning. If we look at our compiled code, we're going to see that capital "Message" here, and when we get past to React.createElement, we're going to get a capital Message right here, outside of a string. So, we're passing a reference to the function directly into the React.createElement(). And then if we ultimately look at what's rendered to the DOM, we come down here, we see our ID of root, our container, and then we see a div with the class of message.

```html
<div id="root">
    <div class="container">
        <div class="message"></div>
        <div class="message">Hello World</div>
        <div class="message">Welcome World</div>
    </div>
</div>
```

Now, let's take a look at what this Message element really is. It's console.log that Message element. We'll look at our console, and we'll see that it is a React element, and its type instead of being a div like we had before, let's take a look at that to compare, console.log div "Hello, World!" Save that and we'll get two console logs, so the first one being our div. The type is a string of div, whereas the type here is our Message function.

```javascript
//div
console.log(<div>Hello World</div>)

$$typeof: Symbol(react.element)
key: null
props: {children: 'Hello World'}
ref: null
type: "div"

//Message
console.log(<Message>Hello World</Message>)

$$typeof: Symbol(react.element)
key: null
props: {children: 'Hello World'}
ref: null
type: ƒ Message(props)
```

Here we get the props of "Children, Hello, World!" and we have "Children, Hello, World!" in this one as well. So, when you give a capital letter in JSX, that's the same as calling React.createElement with the function that you're referencing. That allows you to create a custom component that you can use to reuse code over and over again.

Let's rewrite this using JSX. We'll say Message, and then use the msg prop, because that's what we're expecting. And then we'll come back here, save that, and everything's working without any errors. If we look at our compiled version of our code, then we'll see that we're calling React.createElement with that Message function.

```html
<script type="text/babel">

    const Message = (props) => <div className='message'>{props.msg}</div>

    const element = (
      <div className='container'>
        <Message msg='Hello World' />
        <Message msg='Welcome World' />
      </div>
    )

    ReactDOM.render(element, document.getElementById('root'))
</script>
```

Babel compilled

```html
<script>
"use strict";

var Message = function Message(props) {
  return React.createElement("div", {
    className: "message"
  }, props.msg);
};

var element = React.createElement("div", {
  className: "container"
}, React.createElement(Message, {
  msg: "Hello World"
}), React.createElement(Message, {
  msg: "Welcome World"
}));
ReactDOM.render(element, document.getElementById('root'));
</script>
```

If we wanted to make it nice and declarative so that we could nest to these things as if it's the children prop, then, we just accept children for the name of the prop. Then we can rename this one to "children," and those two are functionally equivalent. If we save this, then we'll still get "Hello World!" and "Welcome World!"

```html
<script type="text/babel">

    const Message = (props) => <div className='message'>{props.children}</div>

    const element = (
      <div className='container'>
        <Message>Hello World</Message>
        <Message children='Welcome World' />
      </div>
    )

    ReactDOM.render(element, document.getElementById('root'))
  </script>
```

Babel compilled

```html
<script>"use strict";

var Message = function Message(props) {
  return React.createElement("div", {
    className: "message"
  }, props.children);
};

var element = React.createElement("div", {
  className: "container"
}, React.createElement(Message, null, "Hello World"), React.createElement(Message, {
  children: "Welcome World"
}));
ReactDOM.render(element, document.getElementById('root'));
</script>
```

But honestly, one of those looks a little bit nicer to me, so I'm going to switch both of these to use that syntax. What's cool about this is I'm also able to nest these together and pass anything that React can render, which includes the string here, or additional components here, or additional elements here.

```html
<script type="text/babel">

    const Message = (props) => <div className='message'>{props.children}</div>

    const element = (
      <div className='container'>
        <Message>
          Hello World
          <Message>Welcome World</Message>
          <span>Hey there</span>
        </Message>
      </div>
    )

    ReactDOM.render(element, document.getElementById('root'))
</script>
```

Babel compilled

```html
<script>"use strict";

var Message = function Message(props) {
  return React.createElement("div", {
    className: "message"
  }, props.children);
};

var element = React.createElement("div", {
  className: "container"
}, React.createElement(Message, null, "Hello World", React.createElement(Message, null, "Welcome World"), React.createElement("span", null, "Hey there")));

ReactDOM.render(element, document.getElementById('root'));
</script>
```

In review of what we did here was we had some code that was being duplicated, and we wanted to reuse that code in multiple places. So, we created our own custom function component which is a function that accepts a props object and returns more React elements. We had to make sure that our function component started with a capital letter so that Babel would compile this to pass the function itself to React.createElement rather than the string message to React.createElement. That way, when React renders our element, it knows what function to call.

## Validate Custom React Component Props with PropTypes

### setup/07-prop-types.html

When you create reusable React components, you want to make sure that people use them correctly. The best way to do this is to use TypeScript in your codebase to give you compile-time checking of your code. But if you’re not using TypeScript, you can still use PropTypes to get runtime validation. In this lesson we’ll learn how PropTypes work, why they’re not enabled in production, and how to use the pre-built prop-types package from the React team.

 <script src="https://unpkg.com/prop-types@15.6.1/prop-types.js"></script>
