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

When you start creating custom function components, you're going to have people using those function components and they may not use it quite right. For example, here, we have this, "Say Hello!" that's accepting a props object we're destructuring right here.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.production.min.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script src="https://unpkg.com/prop-types@15.8.1/prop-types.js"></script>
  <script type="text/babel">
    
    const rootElement = document.getElementById('root')

    function SayHello({firstName, lastName}) {
      return (
        <div>
          Hello {firstName} {lastName}!
        </div>
      )
    }

    // const propTypes = {
    //   string(props, propName, componentName) {
    //     if (typeof props[propName] !== 'string') {
    //       return new Error(
    //         `Hey, the component ${componentName} needs the prop ${propName} to be a string, but you passed a ${typeof props[
    //           propName
    //         ]}`,
    //       )
    //     }
    //   }
    // }

    SayHello.propTypes = {
      firstName: PropTypes.string.isRequired,
      lastName: PropTypes.string.isRequired,
    }

    const element = <SayHello firstName={false} />

    ReactDOM.render(element, rootElement)
  </script>
</body>
```

We're getting a first name and a last name prop and expecting to be able to render those out, but the way that it's being used is we have that first name prop being assigned to false and we're not providing the last name prop at all. The end result is not exactly what we're looking for.

The React team has developed a package called PropTypes that allows you to add run time validation of the props that are passed to your components. This is why React supports a feature called prop-types that allows you to validate the types of props that are being passed to your components when they're rendered.

To add support for that, we're going to have SayHello.PropTypes equals this object. We'll have a key for the prop that we want to validate. That's going to be a function that takes the prop name and the component name. Any time our SayHello component is rendered, we can check that the first name prop was passed properly.

We can say, "If type of props at prop name is not equal to a string, then we can return a new error that says, 'Hey, the component name needs the prop name to be a string, but you passed a type of props at prop name.'" If we save that, then we can see that warning shows up. Failed prop-type. Hey, the component "Say, Hello!" needs the prop first name to be a string, but you passed a boolean.

We could do the same thing for our last name prop. What I'm going to do is pull this out. We'll create a last name prop here and I'm going to make a prop-types object here where we have a string that is that validator that we just created. Then here, we can say first name is PropTypes.string and last name is PropTypes.string. We could add a bunch more validators to the prop-types, for numbers and whatever else you could imagine. With that, we get a warning for both of these. This is so common that the React team created a package on npm that we can use and I'm going to pull it in from unpackage.

I'll paste that right in here and it's called prop-types. With that, it actually creates a global variable here for us called prop-types when we're using it as a script like that. It has the same API that we just created, what foresight. We'll save that. We'll get a refresh and things are working a little differently. Before, we were getting a warning for both the first name and the last name, but now we're just getting one for the first name.

The reason for that is that prop-types by default are not required. Because the last name wasn't provided, we're not getting the last name validated in this case. That works out nicely if you provide a default for the last name, like if we were to say unknown here. But if you want to make sure that it's required, then you can add "a dot is required on both of these." Save that and now you'll get a warning saying that the first name is the wrong type and the last name is required but wasn't provided.

One reasonable concern you might have about prop-types is that it adds a fair amount of code that needs to be run whenever React is rendering your components which may impact performance. Let's take a look at the production.minified version of React and we'll notice that everything is working exactly as it was before but we're no longer getting those warnings. That's because in production prop-types are not applied.

If you want to take things a step further, then you can actually get a Babel plugin that will remove the prop-types from your source code for production. That plugin is called Babel-plugin-transform-remove-prop-types. You could install that and use that in your production build, or many tool kits install and use this by default.

If you want to learn more about the prop-types that are available, you can go to the prop-types page on npm. There are a lot of different types that you can use for your components to validate that people are using your components properly.

## Understand and Use Interpolation in JSX

### setup/08-jsx-interpolation.html

Now that we have a good foundation on React elements, JSX, custom elements, and props, let’s write a React component that has some conditional logic in it to explore the interpolation characteristics of JSX syntax. We’ll learn that interpolation is not unique to JSX and we’ll learn the limitations and capabilities of interpolation in JSX. With this knowledge, we’ll be more productive using JSX.

Here we have a React element that is a React fragment. As its children, we have a character count with the text of "hello world," and a character count with the text of "empty string." Ultimately, we want this to render the text "hello world has 11 characters," and the text "empty string has no characters."

```jsx
const element = (
  <>
    <CharacterCount text="Hello World" />
    <CharacterCount text="" />
  </>
)
```

Let's go ahead and implement this. We already have our function component here. We're accepting the text prop and destructuring it right there. What we're going to do is I want to wrap this in a div, and then we want to say the text and text has text.length characters. That's for this first case. We need to interpolate some stuff here. For this text right here, I think it would be easiest to interpolate all of this as a template literal, so we'll do that. We'll put this inside of curly braces inside of that template literal. Then we'll put an extra space after this.

For the text length, we can interpolate that right there. We'll save this, and here we have the text "hello world has 11 characters." Let's go ahead and put this text length in a strong element so that it's bold. We'll say strong, text length, strong, save that. Now it's bolded.

```javascript
// The text "hello world" has 11 characters
// the text "" has no characters

function CharacterCount({text}) {
  return (
    <div>
      {`The text "${text}" has `} {text.length} characters
    </div>
  )
}
```

We don't want to say text length for zero characters. We want it to say no characters. Let's go ahead and say our length is equal to, if there is a text length, then we'll say the text length. Otherwise, we'll say no. Then we can interpolate that directly into here. Now we're getting 11 characters and no characters.

```javascript
// The text "hello world" has 11 characters
// the text "" has no characters

function CharacterCount({text}) {
  const length = text.length ? text.length : 'No'
  return (
    <div>
      {`The text "${text}" has `} {length} characters
    </div>
  )
}
```

Thanks to this curly braces allowing interpolation, we could take this whole expression, paste it directly into there, and get rid of that variable altogether. That will work just as well. Now let's say we don't want "no" to be inside of this strong. We only want this strong to be wrapped around an actual number. That will require us to change things up a little bit. I'll add that right here. We'll say text.length, so if there is a length, then we want that in a strong with text.length. Otherwise, we'll just use the string no. With that, let's go ahead and interpolate this character string as a string so we can have an explicit space right there. Then we'll save this. Now we get 11 as bolded, and "no" as not bolded.

```javascript
// The text "hello world" has 11 characters
// the text "" has no characters

function CharacterCount({text}) {
  return (
    <div>
      {`The text "${text}" has `}
      {text.length ? <strong>{text.length}</strong> : 'No'}
      {' characters'}
    </div>
  )
}
```

The reason that I wanted to show you this was to demonstrate what it's like to go between JSX land and JavaScript land and back again. Let's follow the flow of this syntax. When we start in the function, this is JavaScript land. We can do JavaScript functions, if statements, all of that stuff. Then when we do the return and this open parentheses, that's still JavaScript land. We enter JSX land by doing this open-angle bracket with the tag. Now we're in JSX land, and we have prop syntax, we have children syntax, and then we have our closing tag, and we enter JavaScript land again. Inside of the opening and closing tag, we're in JSX land.

Once we do an opening curly brace, we're now in JavaScript land again. This is a limited JavaScript land because we can only do expressions. We're not allowed to do things like for loops, if statements, or any of that. It has to be an expression of JavaScript that evaluates to some value. A string like this or a ternary like this, those are expressions, and those are allowed within the curly braces.

If you want to comment something in JSX you need to use JavaScript comments inside of Curly braces like {/*comment here*/}.

```javascript
// The text "hello world" has 11 characters
// the text "" has no characters

function CharacterCount({text}) {
  // js - We can do JavaScript functions, if statements, all of that stuff.
  return (
    //js
    <div /*Now we're in JSX land, and we have prop syntax here*/>
      {/*Between opening and closing of this div tag, we have children syntax*/}
      {/*Once we do an opening curly brace, we're now in JavaScript land again*/}
      {/*This is a limited JavaScript land because we can only do expressions. We're not allowed to do things like for loops, if statements, or any of that*/}
      {/*A string like this or a ternary like this, those are expressions, and those are allowed within the curly braces.*/}
      {`The text "${text}" has `}
      {text.length ? <strong>{text.length}</strong> : 'No'}
      {' characters'}
    </div>
    // js
  )
}
```

If you stop to consider what this JSX is compiled to, this should all make sense. Let's take a look at the JavaScript code that Babel generates for us. Here we have our character counter. We're calling react.createElement. We pass the div that's representing this div right here. It's not taking any props, so we get null.

Babel compilled

```html
<script>"use strict";

// The text "hello world" has 11 characters
// the text "" has no characters
function CharacterCount(_ref) {
  var text = _ref.text;
  return React.createElement("div", null, "The text \"".concat(text, "\" has "), text.length ? React.createElement("strong", null, text.length) : 'No', ' characters');
}

var element = React.createElement(React.Fragment, null, React.createElement(CharacterCount, {
  text: "Hello World"
}), React.createElement(CharacterCount, {
  text: ""
}));
ReactDOM.render(element, document.getElementById('root'));
</script>
```

Then as the third argument, we get this string. Let's go ahead and write this over here. We have react.createElement div, null for the props, and then the string, the text, and so on. If we wanted to, instead of passing this string, do some sort of if statement, that wouldn't work at all. It doesn't make any sense to pass a statement as an argument to a function. For the same reason, you can't use statements inside of the curly braces of JSX because the curly braces basically are saying, "Hey, Babel, as you get to this part, I want you to take everything between these two curly braces and then just stick it in this argument of the createElement call." Having a good understanding of how Babel is compiling your JSX will help you use JSX more effectively.

Once we enter that closing curly brace, we're back in JSX land. Then we come back to this curly brace, and we're now in JavaScript land again. We have this expression. While we're in the middle of this JavaScript land with the ternary expression, we actually enter JSX land again, so we're a couple layers into this. We start out in JavaScript. Then we go into JSX, then we go into JavaScript, then we go into JSX again, and then we go into JavaScript. We exit JavaScript, we enter JSX, we exit JSX, and we're back into JavaScript. Then we exit JavaScript and go into JSX. This back and forth between JavaScript and JSX is really common.

```html
<script type="text/babel">

  // The text "hello world" has 11 characters
  // the text "" has no characters

  function CharacterCount({text}) {
    React.createElement("div", null, if (statement) {})
    return (
      <div>
        {`The text "${text}" has `}
        {text.length ? <strong>{text.length}</strong> : 'No'}
        {' characters'}
      </div>
    )
  }

  const element = (
    <>
      <CharacterCount text="Hello World" />
      <CharacterCount text="" />
    </>
  )

  ReactDOM.render(element, document.getElementById('root'))
</script>
```

This type of interpolation is not unique to just JSX. In fact, we have a couple other examples of interpolation right here. This file is an HTML file, and we start with HTML all right here. We're still going through HTML until we hit the end of this opening script tag. Now we're in JavaScript land. We also have style tags, and now we're in CSS land. HTML has always had this type of interpolation. JavaScript also has built-in interpolation when we're talking about template literals. Right here, we have this template literal. We're in string land. Then when we do the $ {, now we're in JavaScript land. In fact, this has the same limitations that JSX has for its interpolations.

 Specifically, you can't use if statements, for loops, or switch statements in here. Whatever you put in here has to be an expression. That expression can be complex. We can put ternaries in there. We could even put an immediately invoked function expression, though I don't advise that. Having a strong understanding of JSX and interpolating JavaScript expressions is key to using JSX well. It's something that you'll get better with over time as you're using JSX.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <style>
    /* css */
  </style>
  <script type="text/babel">

    // The text "hello world" has 11 characters
    // the text "" has no characters

    function CharacterCount({text}) {
      return (
        <div>
          {`The text "${text}" has `}
          {text.length ? <strong>{text.length}</strong> : 'No'}
          {' characters'}
        </div>
      )
    }

    const element = (
      <>
        <CharacterCount text="Hello World" />
        <CharacterCount text="" />
      </>
    )

    ReactDOM.render(element, document.getElementById('root'))
  </script>
</body>
```

## Rerender a React Application

### setup/09-re-render.html

Applications aren’t really applications if they don’t change over time to represent changes in the application over time. Normally in React you’ll use state to manage this, but before we get to that, we’ll just call ReactDOM.render on the same element so you get an understanding of what React is doing for you. So we’ll learn how React deals with the new elements you give it, compare it to the previous elements, and make surgical updates to the DOM to give you the fastest and best user experience possible (because updating the DOM is typically the slowest part in the whole process).

We made a clock application. Here, it's rendering out the time and we get that time with new date toLocaleTimeString, and then we put that inside of a div and render that. The problem is that it gets out of date as soon as you refresh the page. Every time you refresh the page or get that updated, but you have to keep on refreshing the page, and what a pain that is.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    const rootElement = document.getElementById('root')

    const time = new Date().toLocaleTimeString()
    const element = <div>{time}</div>

    
    ReactDOM.render(element, rootElement)
  </script>
</body>
```

What I want to do instead is I'm going to put this into a function and have that function called every second. Let's go ahead and make that function called tick. We'll put all this inside of tick, and then we'll call tick. We just refactored, just put something in a function. That's a very normal thing to do. Now I'm going to say set interval, tick, every 1,000 milliseconds. I'm getting that update.

```javascript
const rootElement = document.getElementById('root')

function tick() {
  const time = new Date().toLocaleTimeString()
  const element = <div>{time}</div>

  ReactDOM.render(element, rootElement)
}
tick()
setInterval(tick, 1000)
```

The thing that I want to show you about the way that this is working is if we look in the body and then come down here to our app. We're going to see that update happening on our string right here. If I were to add something in here, like we put another div, hello, and another div right there, and then paste that time in there, then we're going to notice that the only thing that's updating is this clock time and not this div.

```javascript
const rootElement = document.getElementById('root')

function tick() {
  const time = new Date().toLocaleTimeString()
  const element = (
    <div>
      <div>Hello</div>
      {time}
    </div>
  )

  ReactDOM.render(element, rootElement)
}
tick()
setInterval(tick, 1000)

// app
<div id="root">
  <div>
    <div>Hello</div>
    "12:27:20"
  </div>
</div>
```

Let's see how this differs if we were to just turn this into an HTML string, and we'll interpolate that. Then instead of ReactDOM.render, we're going to say root element.innerHTML equals that element. We're getting that same behavior that we had before, except the way that it works is it's updating the entire contents of our application every time, starting from this root element. That's not optimal, because it causes a couple of problems.

```javascript
const rootElement = document.getElementById('root')
function tick() {
  const time = new Date().toLocaleTimeString()
  const element = `
    <div>
      <div>Hello</div>
        ${time}
    </div>
  `
  rootElement.innerHTML = element
  //ReactDOM.render(element, rootElement)
}
tick()
setInterval(tick, 1000)
```

Let's take a look at an example. If I make an input and set the value to that time, and let's go ahead and we'll put two in here, then we'll save that, and now we have two of those, and they are updating every second, but as I click in here, my focus is going away. That's because the old elements that were the inputs there are getting totally removed from the DOM, and the new elements are getting put in their place.

```javascript
const rootElement = document.getElementById('root')
function tick() {
  const time = new Date().toLocaleTimeString()
  const element = `
    <div>
      <input value="${time}" />
      <input value="${time}" />
    </div>
  `
  rootElement.innerHTML = element
  //ReactDOM.render(element, rootElement)
}
tick()
setInterval(tick, 1000)
```

React doesn't have this problem. Let's go ahead and turn this back into JSX. Just take away the opening and closing brackets, and the closing quotes, and then we'll remove this and comment that out. Now we're back, and all that we're getting is an update to the values that actually matter for our application, which are the properties for both of these inputs.

```javascript
const rootElement = document.getElementById('root')
function tick() {
  const time = new Date().toLocaleTimeString()
  const element = (
    <div>
      <input value={time} />
      <input value={time} />
    </div>
  )
  ReactDOM.render(element, rootElement)
}
tick()
setInterval(tick, 1000)
```

This has great implications for the performance of our applications, as well as the accessibility, because React is keeping track of our focus for us. This isn't how you normally re-render new application. Typically, whenever state changes, you don't have to re-render your entire application, but I wanted to show you this so you have an understanding of what React is really doing for you.

When you create these React elements, you give that to ReactDOM.render or you trigger a re-render of a component, and React is going to compare the elements that you returned this time with the elements that you returned last time. It's going to do a div of those two elements, and then it will update the DOM surgically to only update the things that were different between the last time and this time you returned JSX.

## Style React Components with className and inline Styles

### setup/10-styling.html

Application layout is only one part of the user interface equation. Another part is styling. In this lesson we’ll explore the className and style prop for styling our components. This lesson goes much deeper than that. We’ll learn why className is className and not class (like it is in HTML), and we’ll learn why the style prop accepts an object of camelCase styles rather than a string of css (like it does in HTML). We’ll take it even further by creating a reusable component that encapsulates these styles and composes the given className and style prop together. You’re going to love this one. Finally, when you actually build a full application, a tool you’ll find invaluable is Tailwind.css.

We have a bunch of CSS in our HTML document, and we want to style this div with that CSS. To apply that CSS, we're going to add a className of Box to get that box around this small, light-blue box. Because we want it to be small, let's also add a box--small, and we'll save that.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <style>
    .box {
      border: 1px solid #333;
      display: flex;
      flex-direction: column;
      justify-content: center;
      text-align: center;
    }
    .box--large {
      width: 270px;
      height: 270px;
    }
    .box--medium {
      width: 180px;
      height: 180px;
    }
    .box--small {
      width: 90px;
      height: 90px;
    }
  </style>
  <script type="text/babel">

    const element = (
      <div>
        <div className='box box--small'>Small lightblue box</div>
      </div>
    )

    ReactDOM.render(element, document.getElementById('root'))
  </script>
</body>
```

Then, I want it to be light blue, but we don't have any CSS for light blue. We could add it, but I want to show you the style prop which accepts an object rather than a string of styles. We're going to pass this object, and it will be the same property names that you get if you use getComputedStyle for this element, that is, CSS properties that are camel-cased instead of kebab-cased. For us to get a background color, we're going to say background color, and then we want lightblue. With that, we get a small, light-blue box. Let's also add a font style italic right there. Now we have a small, light-blue box in italics.

```html
<script type="text/babel">

  const element = (
    <div>
      <div className='box box--small' style={{fontStyle: 'italic', backgroundColor: 'lightblue'}}>Small lightblue box</div>
    </div>
  )

  ReactDOM.render(element, document.getElementById('root'))
</script>
```

We also have CSS for large and medium boxes, so let's go ahead and create some more of these boxes. We'll make this one be medium, and using our multiple cursors here, we'll use large for that one. Instead of light blue for our medium, let's do pink. Instead of the light blue of our large, we'll use orange. We'll save that, and we have this stack of boxes.

```html
<script type="text/babel">

  const element = (
    <div>
      <div className='box box--small' style={{fontStyle: 'italic', backgroundColor: 'lightblue'}}>small lightblue box</div>
      <div className='box box--medium' style={{fontStyle: 'italic', backgroundColor: 'pink'}}>medium pink box</div>
      <div className='box box--large' style={{fontStyle: 'italic', backgroundColor: 'orange'}}>large orange box</div>
    </div>
  )

  ReactDOM.render(element, document.getElementById('root'))
</script>
```

There's a fair amount of duplication in these, so what I'm going to do is make a new function component called Box. This is going to take some props, and then will return a div, and we'll spread all the props. Right now, this Box component basically functions as a div. We could replace all of these divs, with multiple cursors here, with a box. We save that, and we get the exact same result.

```html
<script type="text/babel">
 function Box(props) {
    return <div {...props} />
  }

  const element = (
    <div>
      <Box className='box box--small' style={{fontStyle: 'italic', backgroundColor: 'lightblue'}}>small lightblue box</Box>
      <Box className='box box--medium' style={{fontStyle: 'italic', backgroundColor: 'pink'}}>medium pink box</Box>
      <Box className='box box--large' style={{fontStyle: 'italic', backgroundColor: 'orange'}}>large orange box</Box>
    </div>
  )

  ReactDOM.render(element, document.getElementById('root'))
</script>
```

Now, let's make this box a little bit more useful by taking the repetition from each one of these and putting it within the Box component. First off, we have a className, and then it has a box--, but then the size is different. Let's go ahead and just take the className Box. We'll put className Box, we'll save that. Once we save that -- and we can get rid of these as well -- then we'll notice that the Box className is no longer being applied because we're not getting that border. We can verify that by inspecting this, looking our application. We see class Box small, but we don't see the Box className here. Think for a moment why that might be.

```html
<script type="text/babel">
 function Box(props) {
    return <div className='box' {...props} />
  }

  const element = (
    <div>
      <Box className='box--small' style={{fontStyle: 'italic', backgroundColor: 'lightblue'}}>small lightblue box</Box>
      <Box className='box--medium' style={{fontStyle: 'italic', backgroundColor: 'pink'}}>medium pink box</Box>
      <Box className='box--large' style={{fontStyle: 'italic', backgroundColor: 'orange'}}>large orange box</Box>
    </div>
  )

  ReactDOM.render(element, document.getElementById('root'))
</script>
```

The reason might be a little more clear if I take this spread of props and put it on the other side of the className. We save that, and now we get the opposite problem where we have the border the className Box provides, but we don't have the small, medium, or large classNames applies. The reason is, because of this spread of props, we're getting an override of the className prop that's being provided to the Box component.

```html
<script type="text/babel">
 function Box(props) {
    return <div  {...props} className='box' />
  }

  const element = (
    <div>
      <Box className='box--small' style={{fontStyle: 'italic', backgroundColor: 'lightblue'}}>small lightblue box</Box>
      <Box className='box--medium' style={{fontStyle: 'italic', backgroundColor: 'pink'}}>medium pink box</Box>
      <Box className='box--large' style={{fontStyle: 'italic', backgroundColor: 'orange'}}>large orange box</Box>
    </div>
  )

  ReactDOM.render(element, document.getElementById('root'))
</script>
```

What we can do is combine the classNames into a single className that will work for all of our boxes. Instead of just taking the props object as it is, I'm going to destructure it in-place, and we'll take the className out of here. Then I'll put a ...rest to say that these are the rest of the props. Then we'll remove this, and we'll put the spread at the end. Then we'll manually combine the className that we want to provide for boxes in general with the className that's provided to us through the props. We'll make a template literal here. We'll say box, and then we'll put className. We'll save that, and now everything's working as it should be.

```html
<script type="text/babel">

 function Box({className, ...rest}) {
    return <div  className={`box ${className}`} {...rest} />
  }

  const element = (
    <div>
      <Box className='box--small' style={{fontStyle: 'italic', backgroundColor: 'lightblue'}}>small lightblue box</Box>
      <Box className='box--medium' style={{fontStyle: 'italic', backgroundColor: 'pink'}}>medium pink box</Box>
      <Box className='box--large' style={{fontStyle: 'italic', backgroundColor: 'orange'}}>large orange box</Box>
    </div>
  )

  ReactDOM.render(element, document.getElementById('root'))
</script>
```

One problem here is that if I take off the className on one of these boxes, then I'm going to get "box undefined." That's probably not areally big issue, but it's pretty simple to fix by adding a default value for this className to be an empty string. Now we get Box with a space. I'm not as worried about the space. If you were, then you could add a .trim right here, and that would get rid of our space.

```html
<script type="text/babel">

 function Box({className, ...rest}) {
    return <div  className={`box ${className}`.trim()} {...rest} />
  }

  const element = (
    <div>
      <Box 
        //className='box--small' 
        style={{fontStyle: 'italic',
        backgroundColor: 'lightblue'}}
      >
        small lightblue box
      </Box>
      <Box className='box--medium' style={{fontStyle: 'italic', backgroundColor: 'pink'}}>medium pink box</Box>
      <Box className='box--large' style={{fontStyle: 'italic', backgroundColor: 'orange'}}>large orange box</Box>
    </div>
  )

  ReactDOM.render(element, document.getElementById('root'))

// Console app
<div id="root">
  <div>
    {/*<div class="box undefined" style="font-style: italic; background-color: lightblue;">small lightblue box</div>*/}
    {/*<div class="box " style="font-style: italic; background-color: lightblue;">small lightblue box</div>*/}
    <div class="box" style="font-style: italic; background-color: lightblue;">small lightblue box</div>
    <div class="box box--medium" style="font-style: italic; background-color: pink;">medium pink box</div>
    <div class="box box--large" style="font-style: italic; background-color: orange;">large orange box</div>
  </div>
</div>
</script>
```

I don't think that's a big deal, so we'll get rid of that. Let's restore this small box to its former glory. The other thing that's common across all these boxes is the font style italic. Let's have that be provided here. We'll say style fontStyle italic. With that, we can now remove the font style from all of these. We'll save that, and we've made things a lot more terse for users of this box component.

> Like vanilla JS functios, custom components are how you reduce repetition in your code.

```javascript
function Box({className='', ...rest}) {
  return (
    <div  className={`box ${className}`}
      style={{fontStyle: 'italic'}}
      {...rest}
    />
  )
}

const element = (
  <div>
    <Box 
      className='box--small' 
      style={{backgroundColor: 'lightblue'}}
    >small lightblue box</Box>
    <Box 
      className='box--medium' 
      style={{backgroundColor: 'pink'}}
    >medium pink box</Box>
    <Box
    className='box--large'
      style={{backgroundColor: 'orange'}}
    >large orange box</Box>
  </div>
)
```

You might notice we no longer have that font style of italic. The reason that's happening is the exact same as with the className. If I move this rest up here before the style, now we're going to get the italic, but we won't get the custom styles that the user of our box component is trying to specify.

```javascript
function Box({className='', ...rest}) {
  return (
    <div  className={`box ${className}`}
      {...rest}
      style={{fontStyle: 'italic'}}
    />
  )
}
```

Again, we do need to compose these manually. I'm going to pluck off the style prop from our props here, and we'll combine the style prop from those with the style prop that we specify by using object spread syntax. Then I'm going to put rest at the bottom here again. We'll save that, and we get our italics and we get our special color, which is exactly what we're looking for. Now anyone that wants to have a box can use this component, and it will have the Box className and italics applied automatically for them.

```javascript
function Box({className='', style, ...rest}) {
  return (
    <div  className={`box ${className}`}
      style={{fontStyle: 'italic', ...style}}
      {...rest}
    />
  )
}
```

One useful feature of creating components like this is we can use it to separate our user code from the styling concerns of our specific component. Rather than a className, it would actually be better to accept a size prop. We could say the size is small, medium, or large.

> This applies to more than styling. It is a great example of creating versatile components through abstraction.

Let's make that work. I'll remove the className here. We'll save this. Let's scroll up to the top, and we'll see that our small, light-blue box is no longer small. Now I'm going to take the size prop, and we're going to generate a size className. *If the size prop is specified, then we'll say box--size. Otherwise, we'll do an empty string.* Then we can put that size className inside of our className list here. If we save that, then we get a small, light-blue box, and users of our box component no longer need to concern themselves with the className that needs to be applied to create a small box.

This Box component can deal with the implementation details of what it takes to make a small box. This means that we could change the classNames that we use. We could use a third-party CSS library, and we could change that CSS library. Any component that's using the box just needs to follow the API that the box creates for it. We can separate our components from the classNames used to style them. That said, we can still apply our own classNames if we want to, and we can apply our styles if we want to because those are going to be combined with whatever is happening in the box. Let's go ahead and update the classNames for both of these because I like the size prop better.

We'll save that, and now we have a small, light-blue box, a medium pink box, and a large orange box with a reusable Box component that merges the className, the style prop, forwards along all of the props, like the children prop that we're passing for each one of these, and accepts a special size prop so that you can size the box appropriately.

```javascript
function Box({style, size, className = '', ...rest}) {
  const sizeClassName = size ? `box--${size}` : ''
  return (
    <div
      className={`box ${className} ${sizeClassName}`}
      style={{fontStyle: 'italic', ...style}}
      {...rest}
    />
  )
}

<Box size="small" style={{backgroundColor: 'lightblue'}}>
  small lightblue box
</Box>
<Box size="medium" style={{backgroundColor: 'pink'}}>
  medium pink box
</Box>
<Box size="large" style={{backgroundColor: 'orange'}}>
  large orange box
</Box>
<Box>sizeless box</Box>
```

One thing that I want to note here about the className prop in HTML. We would normally use class instead of className. ClassName is the dom property that you use to access the class attribute on dom nodes. If we go here and say $0 which will access the element that we have currently selected in our elements tab, then we can say .className, and that will give us that className list.

```javascript
// console
$0.className
'box  box--small'
```

In addition, if we were to take all of our props and make a props object here, we just move all of this right here, convert it to JavaScript rather than JSX syntax, and then spread those props. That will work just as well. Then let's say that this were class instead of className.

```javascript
function Box({style, size, className = '', ...rest}) {
  const sizeClassName = size ? `box--${size}` : ''
  const props = {
    className: `box ${className} ${sizeClassName}`,
    style: {fontStyle: 'italic', ...style},
    ...rest
  }
  return <div {...props} />
}

<Box size="small" style={{backgroundColor: 'lightblue'}}>
  small lightblue box
</Box>
<Box size="medium" style={{backgroundColor: 'pink'}}>
  medium pink box
</Box>
<Box size="large" style={{backgroundColor: 'orange'}}>
  large orange box
</Box>
<Box>sizeless box</Box>
```

If we wanted to extract this and use shorthand syntax here, then we'd make it class variable. This wouldn't work because class is a reserved word. In addition, if we wanted to leave this here and then destructure the class property from the props, then this also wouldn't work because class is a reserved keyword as well. For that reason and others, it is the className prop rather than the class prop.

One thing that I really like about this style prop being an object of styles rather than a string of styles is because it's a lot easier to combine objects of styles. With className, we have a string. I don't mind that because the order in which I apply these classNames has no bearing on which one of these is going to be applied. However, the order in which I apply these styles does have a bearing in what's going to be applied. If I were to apply ...style first, then there'd be no way for me, as a user of the box component, to override that to control what styles are actually going to be applied.

```javascript
const props = {
  className: `box ${className} ${sizeClassName}`,
  style: {fontStyle: 'italic', ...style},
  ...rest
}
```

Let's put everything back where it was and review. We had a bunch of CSS that we wanted to apply to our divs here to make a small, light-blue box, a medium pink box, and a large orange box. We did that manually by making divs for each one of these and applying the appropriate classNames and style value. Then, in an effort to reduce duplication, we created this function component called Box, which accepts a className, combines that with the className necessary to make a box, accepts a style prop, and combines that with the style necessary to make a box with a font style of italic.

Also accepting a size prop to separate the code for the users of the Box component from the code necessary to make a box of that specified style. Then we take the rest of the props, and spread that on the underlying div so that users can provide additional props like ID is root as well as the children prop for the contents of the box. One last thing that I want to show you is Tailwind CSS, which I recommend you take a look at for building consistent user interfaces. Definitely give this a look for building and styling your applications. You can apply the same principles that we learned to building custom components that utilize these classNames.

## Use Event Handlers with React

### setup/11-event-handlers.html

Application’s can be laid out and styled pretty, but if they don’t respond to interactions from the user then they’re just web pages, not apps. Let’s get an introduction to event handlers with React. There are a ton of supported events that you can find on the docs. We still haven’t gotten to state yet, so we’ve implemented our own little way of managing state and re-rendering our component so we can play around with event handlers.

One thing you’ll want to know is that events with React are very similar to working with events in regular DOM. React does have an optimization implementation on top of the event system called SyntheticEvents, but most of the time you won’t observe any difference with those events from regular DOM events (and you can always get access to the native event using the nativeEvent property).

Here we have an app component that is rendering some JSX here for there have been events, click me, you typed, and then an input here. We have some state that is running this application component. If I update the event count to 10, then we're going to see there have been 10 events. If I update the username to 'Hello there' and save that, then we're going to see you typed Hello there. The value of the input isn't getting updated and there have actually not been 10 events, so let's go ahead and wire up things so we can update our state and re-render the app.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    const rootElement = document.getElementById('root')

    const state = {eventCount: 10, username: 'hellothere'}

    function App() {
      return (
        <div>
          <p>There have been {state.eventCount} events.</p>
          <p>
            <button>Click Me</button>
          </p>
          <p>You typed: {state.username}</p>
          <p>
            <input />
          </p>
        </div>
      )
    }

    function setState(newState) {
      Object.assign(state, newState)
      renderApp()
    }

    function renderApp() {
      ReactDOM.render(<App />, document.getElementById('root'))
    }

    renderApp()
  </script>
</body>
```

We already have a function here called setState, which will update our state variable and then render the app. That will just call React.render on our root again. This is not typically how you re-render an application or manage state in a React application, but this will work for our purposes of learning how events work in React.

First let's deal with this button. We have on button's an onClick event that we can call. This we're going to provide a function. I can make this an inline arrow function here. We'll just say setState, calling this function down here with the new state of an object, eventCount. We want that eventCount to be the current state.eventCount + 1. If we save that and then I go over here and click, we're going to get an increment every single time I click.

There are a lot of different events that we can use here. We can have an onFocus and save that and every time I focus the input we're going to get an increment on that event. Or we could say onMouseOver, save that, and then every time I mouse over, we'll get an increment on that eventCount. There are a lot more events that are supported by React. Let's set this back to onClick and then we can also extract this to handleClick. We could put that right here. Function handleClick() and then we'll call setState there. That will work just as well. There we go.

```javascript
const state = {eventCount: 0, username: ''}

    function App() {
      function handleClick() {
        setState({eventCount: state.eventCount + 1})
      }
      return (
        <div>
          <p>There have been {state.eventCount} events.</p>
          <p>
            <button onClick={handleClick}>Click Me</button>
          </p>
          <p>You typed: {state.username}</p>
          <p>
            <input />
          </p>
        </div>
      )
    }

    function setState(newState) {
      Object.assign(state, newState)
      renderApp()
    }

    function renderApp() {
      ReactDOM.render(<App />, document.getElementById('root'))
    }

    renderApp()
```

Then let's take a look at this input. We want this you typed to get updated when we enter some new username. I'm going to say onBlur and we'll say setState('username'). Then we need to specify a value here. What we need is to get the value of the input that is receiving the onBlur event. As an argument to the event handler, we receive the event. Then we can use that event to get the target of the event, which will be our input. Then we'll get that value from the input. If we save that, then we can type in Kent C Dodds and then blur. Our state gets updated. If we want this to get updated as we're typing, then we can change this to onChange. As the user types in this input, we'll get that update to our state and we'll re-render the application.

```javascript
const state = {eventCount: 0, username: ''}

    function App() {
      function handleClick() {
        setState({eventCount: state.eventCount + 1})
      }
      return (
        <div>
          <p>There have been {state.eventCount} events.</p>
          <p>
            <button onClick={handleClick}>Click Me</button>
          </p>
          <p>You typed: {state.username}</p>
          <p>
            {/*<input onBlur={event => setState({username: event.target.value})}/>*/}
            <input onChange={event => setState({username: event.target.value})}/>
          </p>
        </div>
      )
    }

    function setState(newState) {
      Object.assign(state, newState)
      renderApp()
    }

    function renderApp() {
      ReactDOM.render(<App />, document.getElementById('root'))
    }

    renderApp()
```

Let's go ahead and pull this onChange handler out. We'll say handleChange. We'll bring it up here. Function handleChange will take the event. Let's go ahead and take a look at that event. We'll say console.log(event), save that. We'll pop open our Dev Tools here, look at the console, and then type in one character. We'll notice we get a synthetic event object here. That's not the native event. The native event is this property nativeEvent input event. React does some serious performance optimizations for our events and that's what this synthetic event thing is all about.

Most of the time you don't need access to the native event, but if you ever do then you can say event.nativeEvent and we'll hit save. We'll type in a character and we'll get that native input event. But the synthetic event has pretty much all the same properties as a regular event, so that's what you're typically going to use. One thing I like about React's event system is that you pass the event handler directly to the element that you want to attach the event to, so it makes following the flow of events and state updates really straightforward.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    const rootElement = document.getElementById('root')

    const state = {eventCount: 0, username: ''}

    function App() {
      function handleClick() {
        setState({eventCount: state.eventCount + 1})
      }

      function handleChange(event) {
        setState({username: event.target.value})
      }

      return (
        <div>
          <p>There have been {state.eventCount} events.</p>
          <p>
            <button onClick={handleClick}>Click Me</button>
          </p>
          <p>You typed: {state.username}</p>
          <p>
            <input onChange={handleChange} />
          </p>
        </div>
      )
    }

    function setState(newState) {
      Object.assign(state, newState)
      renderApp()
    }

    function renderApp() {
      ReactDOM.render(<App />, document.getElementById('root'))
    }

    renderApp()
  </script>
</body>
```

## Manage state in a React Component with the useState hook

### setup/12-state.html

An application that responds to user input is valuable, but what do we do with that data the user has given us? This is where component state comes in. We need a place to put data that can change in our application, and we need to let React know when that state changes so it can update (or re-render) our app for us.

In React, state is associated to components and when the state changes, the component is updated. To get access to this state and to update it, we use what is called a “React Hook” which allows us to call into React from within our component and let it know that we need to manage some state. In this lesson, you’ll learn how to use the useState hook to do this.

Let's start by making our form. Here we'll have our div and then we'll make a form. Then we'll have a label with the name and our input and we'll save that. We get that form.

```javascript
function Greeting() {
  return (
    <div>
      <form>
        <label>Name: </label>
        <input />
      </form>
    </div>
  )  
}

ReactDOM.render(<Greeting />, document.getElementById('root'))
```

Then we'll have this message, "Please type your name." Then we want to associate this label to this input so that it's properly associated and you can tell that by clicking on the label. If it doesn't focus the input, then it's not properly labeled.

```javascript
function Greeting() {
  return (
    <div>
      <form>
        <label>Name: </label>
        <input />
      </form>
      Please type your name
    </div>
  )  
}

ReactDOM.render(<Greeting />, document.getElementById('root'))
```

Let's add an ID to our input of name and an htmlFor of name. htmlFor is like the for attribute in HTML but in JSX you need to use htmlFor. That's one of the few differences between JSX and regular HTML. Let's save that, come back here. When I click on name, it now focuses the input. Great.

```javascript
function Greeting() {
  return (
    <div>
      <form>
        <label htmlFor='name'>Name: </label>
        <input id='name' />
      </form>
      Please type your name
    </div>
  )  
}

ReactDOM.render(<Greeting />, document.getElementById('root'))
```

Now, we're going to have some state here for the name. If there is a name, then we'll have it say strong, "Hello, Name!" Otherwise we'll have it say, "Please type your name." Great. Then if we say Kent, save that. It will say, "Hello, Kent!" By default it doesn't say anything.

```javascript
function Greeting() {
  const name = ''
  return (
    <div>
      <form>
        <label htmlFor='name'>Name: </label>
        <input id='name' />
      </form>
      {name ? <strong>Hello {name}</strong> : 'Please type your name'}
    </div>
  )  
}

ReactDOM.render(<Greeting />, document.getElementById('root'))
```

Now, let's wire up an onchange handler for this input. We'll call that handle change. I'll bring that up here and say handle change is an arrow function that accepts an event and it needs to update the state of the name. We need to have some way to update that and we can't simply say name = event.target.value. That's not going to work because that won't trigger a re-render and, even if it were to trigger a re-render, this whole function would be recalled. Then the name that we would be setting would get garbage collected and we'd create a new name variable.

> Unless a rerender is triggered and your function is called, the DOM isn't going to update.

```javascript
function Greeting() {
  const name = ''
  const handleChange = event => name = event.target.value
  return (
    <div>
      <form>
        <label htmlFor='name'>Name: </label>
        <input onChange={handleChange} id='name' />
      </form>
      {name ? <strong>Hello {name}</strong> : 'Please type your name'}
    </div>
  )  
}

ReactDOM.render(<Greeting />, document.getElementById('root'))
```

Instead, React has what's called a *React hook* for maintaining state for a component. We're going to use that with react.useState. We'll pass it the default value of an empty string and react.useState returns an array, we'll call this our state array, and we'll get our name from state array at index zero and our set name from state array at index one. Here instead of trying to reassign that variable, we'll call setName with the event.target.value. If we save that, now everything is working, but nobody wants to write their code like this every time they want to use state, so we're going to destructure this to be name and setName. Then we can delete those lines and save that and it's still working.

```javascript
function Greeting() {
  // const stateArray = React.useState('')
  // const name = stateArray[0]
  // const setName = stateArray[1]
  const [name, setName] = React.useState('')
  const handleChange = event => name = event.target.value
  return (
    <div>
      <form>
        <label htmlFor='name'>Name: </label>
        <input onChange={handleChange} id='name' />
      </form>
      {name ? <strong>Hello {name}</strong> : 'Please type your name'}
    </div>
  )  
}

ReactDOM.render(<Greeting />, document.getElementById('root'))
```

Woo! React rocks! In review, to use state in a React function component, you use the *useState hook from React*. The useState hook accepts the initial value, so when this greeting component is initially rendered, that is going to be the value of our name variable. Any time we call this second element of the array, our updater function will trigger a re-render of this entire function component. When React useState is called again, it will ignore the initial value and instead give us the current value of that name.

> useState's updater function triggers a re-rendering. Use this with events to easily update your application.

Because React keeps track of the order in which these are called, we could add a second one. Here we'll call this name two and set name two. We'll make another handle change to handle change two. We'll have that call set name two. Then we'll just duplicate all this stuff, put that inside of another div here, and then we'll reference name two and name two. This will be handle change two.

Now we can say Kent 1 and Kent 2. Those states are managed independently of one another because React keeps track of the order in which these are going to be called, allowing you to use state as much as you need for your component. The values in here can be anything. You can make it a Boolean or you can make it a number or you can make it an object or an array -- whatever makes sense for the state that you're trying to manage.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">

    function Greeting() {
      // const stateArray = React.useState('')
      // const name = stateArray[0]
      // const setName = stateArray[1]
      const [name, setName] = React.useState('')
      const [name2, setName2] = React.useState('')

      const handleChange = event => setName(event.target.value)
      const handleChange2 = event => setName2(event.target.value)
      return (
        <div>
          <div>
            <form>
              <label htmlFor='name'>Name: </label>
              <input onChange={handleChange} id='name' />
            </form>
            {name ? <strong>Hello {name}</strong> : 'Please type your name'}
          </div>
          <div>
            <form>
              <label htmlFor='name'>Name2: </label>
              <input onChange={handleChange2} id='name' />
            </form>
            {name2 ? <strong>Hello {name2}</strong> : 'Please type your name'}
          </div>
        </div>
      )  
    }

    ReactDOM.render(<Greeting />, document.getElementById('root'))
  </script>
</body>
```

## Manage side-effects in a React Component with the useEffect hook

### setup/13-side-effects.html

Another piece to the web application puzzle is managing side-effects of our user’s interactions. In this lesson we’ll be interacting with the browser’s localStorage API, but this same thing would apply if we’re interacting with a backend server, or the geolocation API, or anything else that needs to happen when the state of our component changes. You’ll learn how to use React’s useEffect hook to manage the side-effect of saving state into localStorage, and also how to re-synchronize our application with the stored value in localStorage. Learn more about viewing localStorage in the Chrome DevTools.

I want to be able to type in here some value and have that saved in localStorage so that when I refresh the page, that value will be retrieved from localStorage and be loaded into the input. This is called a side effect, and in react, to do this, you use react useEffect. This is another hook, like useState. This function will be called every time the greeting component is rendered.

Anytime the greeting component is rendered, we're going to say window.localStorage.setItem -- we'll call it name in localStorage, and we'll set it to the value of name. If we save that, and then open our dev tools and in the application tab here, we can go to localStorage, and we'll see that there's nothing in there. Then we can type a name, and we'll see that the name gets updated in localStorage with whatever the current value for that name variable is.

You'll notice that if I refresh here, I'm not getting that name value loaded into my input, and the value in localStorage is getting cleared. This is because we initialize our state to an empty string, and we don't take the localStorage value into account. Then, because we've rendered, we run this callback, updating the localStorage item for name to that new empty string name. We need to initialize that value to whatever's in localStorage if it's there, and an empty string if it's not.

Here we'll say window.localStorage.getItem(name), and if that returns null because there's nothing in there, then we'll default that to an empty string. We save that. We type a name. We hit refresh, and we notice that the value in localStorage is still consistent. We notice the value right here is correct, but the name input does not have the name in there. We need to specify what the value for the input should be. We specify a value of name.

Now when we save this, we'll get a refresh, and now the value is the same value that's in localStorage and in memory for the state of our react component. We'll notice that as we change this and refresh, we always get that value from localStorage, and we keep that value updated in localStorage as well.

In review, to make all this work, we first used react useEffect to set the name value in localStorage to the name value in our state in memory. Then, to have our state in memory be initialized from localStorage, we used Window.localStorage.getItem(name), and if there is nothing in there, then we'll initialize it to an empty string as a default. Then, to make sure that the input is showing the same value for the name as a name in memory, we specified a value prop, changing this input from an uncontrolled to a controlled input.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    function Greeting() {
      const [name, setName] = React.useState(
        window.localStorage.getItem('name') || '',
      )

      React.useEffect(() => {
        window.localStorage.setItem('name', name)
      })

      const handleChange = event => setName(event.target.value)

      return (
        <div>
          <form>
            <label htmlFor="name">Name: </label>
            <input value={name} onChange={handleChange} id="name" />
          </form>
          {name ? <strong>Hello {name}</strong> : 'Please type your name'}
        </div>
      )
    }

    ReactDOM.render(<Greeting />, document.getElementById('root'))
  </script>
</body>
```

## Use a lazy initializer with useState

### setup/14-lazy-initialization.html

Something that’s important to recognize is that every time you call the state updater function (like the setName function in our component), that will trigger a re-render of the component that manages that state (the Greeting component in our example). This is exactly what we want to have happen, but it can be a problem in some situations and there are some optimizations we can apply for useState specifically in the event that it is a problem.

In our case, we’re reading into localStorage to initialize our state value for the first render of our Greeting component. But after that first render, we don’t need to read into localStorage anymore because we’re managing that state in memory now (specifically in that name variable that React gives us each render). So reading into localStorage every render after the first one is unnecessary. So React allows us to specify a function instead of an actual value, and then it will only call that function when it needs to–on the initial render. In this lesson, I’ll show you how to do this and demonstrate how it works.

One thing that's important to know about the useState Hook is that the initial value you provide here is really important for the initial render of our component, but then it's ignored for renders of our component thereafter. That's normally not a problem, especially if you have just an empty string here, but here we're reading into localStorage every time our greeting component is re-rendered. We can add a console.log('rendered') right here to see how often that is.

We open up our console and we'll see that we already have a rendered here for our initial render of the greeting component. As we type, we get a render every time we type a character. We only need it to read into localStorage for the initialization of our state. We don't need to have it read into localStorage for every single time we re-render. This isn't really a huge deal here because reading into localStorage is pretty fast and we're not parsing anything, but if we were parsing a big JSON object, then this could be a problem.

To combat this, React.useState has a lazy initialization feature. You can provide a function as the initial value, and that function will be called to retrieve the initial value. That function will only be called when it's absolutely necessary to retrieve the initial value. If we turn this into an arrow function, which simply returns that initial value, then we save this, we'll notice that we're still getting our renders, but this function is not getting called, except on the initial value retrieval.

We can prove this by making this a multiline arrow function, returning that value and console.log('hello') in here. Now we get that hello, and then we get that rendered, and that's an important note, is that this function is called synchronously, and it's expected to be synchronous. As we type hello, you'll see that we do not get that console.log('hello'). We save ourselves the expense of reading into local storage on every render.

In review, the problem that we're solving here is that reading into localStorage is not necessary, except for the initial render of our component. We turn our initial value argument here into a function so that React will call it only when it's necessary to get that initial value, which is only on the first render.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">

    function Greeting() {
      const [name, setName] = React.useState(() => {
        console.log('hello')
        return window.localStorage.getItem('name') || ''
      })

      console.log('rendered')

      React.useEffect(() => {
        window.localStorage.setItem('name', name)
      })

      const handleChange = event => setName(event.target.value)

      return (
        <div>
          <form>
            <label htmlFor="name">Name: </label>
            <input value={name} onChange={handleChange} id="name" />
          </form>
          {name ? <strong>Hello {name}</strong> : 'Please type your name'}
        </div>
      )
    }

    ReactDOM.render(<Greeting />, document.getElementById('root'))
  </script>
</body>
```

## Manage the useEffect dependency array

### setup/15-effect-deps.html

Something that’s really important to know about React’s useEffect hook is that it eagerly attempts to synchronize the “state of the world” with the state of your application. That means that your effect callback will run every time your component is rendered. This normally won’t lead to bugs (in fact, it does a great job at preventing bugs that plagued React apps before useEffect was available), but it can definitely be sub-optimal (and in some cases can result in an infinite loop).

In this lesson we’ll observe that our effect callback is getting called more than it needs to be, and you’ll learn how to add a dependency array so it is updated only when the state it relies on changes. And in real applications, you’ll want to make sure you have and follow the rules from the ESLint plugin: eslint-plugin-react-hooks (many tools like Create React App have this installed and configured by default).

We've added a little bit here to simulate another optimization that we want to make. Here now we have a count state, and that's just being rendered into this button. Every time we click on the button, it re-renders our app component, which triggers a re-render of our greeting component. Every time our greeting component re-renders, this useEffect is going to be called. If we console.log('greeting useEffect'), we'll save that. Open up our DevTools. We see we get the greeting useEffect for the initial render. Every time I click this, we'll get another greeting useEffect.

The effect that we're running is updating localStorage to set the name to the name value. This side effect doesn't need to be run because the name value hasn't changed. We only need to synchronize the localStorage value with the name value that we have in memory for the state of this component.

React useEffect accepts a second argument as an optimization to combat this problem. That second argument is a dependency array where you pass all the dependencies for your side effect. This is where you pass anything that you want to make sure you synchronize the state of the world with the state of our application. In our case, the only thing that we're trying to synchronize here is the state of localStorage, which is the state of the world, with the state of our application, which is the name. For our dependency array, we're going to provide the name.

If we save that, then we'll notice that we get that greeting useEffect called initially, and that's because useEffect is always going to be called on the initial mount. Hereafter, when we click on this button, we're not going to get the greeting useEffect. Then when we update the name value, we're going to get greeting useEffect called because the name has changed, and the state of the world is now out of sync with the state of our application. React is going to call our useEffect callback.

It's very important that you keep this dependency array accurate according to the dependencies that your callback function relies on. For example, we rely on name. That's why it's important that we keep this dependency list in here. If you don't keep this list accurate, then you could be missing out on synchronizing the state of the world with state changes that happen in your app, and your users could lose saved work.

For example, if I were to remove the name from this array and save that, then we'll get that greeting useEffect called. As I type in here, we'll notice that the state of my application is being kept updated, but I'm not getting any console.logs. If I refresh, I'm going to be back to where I was before. I, as the user of this application, have lost work, because my code was not properly synchronizing the state of my application with the state of the world outside my application.

In an effort to help you avoid making mistakes here, the React team has created an ESLint plugin called eslint-plugin-react-hooks which you can use to not only ensure that the dependency array is kept up-to-date, but keep it up-to-date automatically for you using ESLint's fix feature. The rule that will help you with this is the exhaustive-deps rule, and I strongly advise that you use this tool and follow that rule.

In review, the problem that we were solving here is our effect callback was being called more than it needed to be. I want to make a special note here, that just because it was being called more than it needed to be didn't mean we had a bug in our application, so this is just an optimization to make our application run a little faster. A dependency array may not be necessary in all cases, but in our case, we could simply add this dependency array with the one dependency that our effect callback relied on. This callback is only called when necessary.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">

    function Greeting() {
      const [name, setName] = React.useState(
        () => window.localStorage.getItem('name') || '',
      )

      React.useEffect(() => {
        console.log('greeting useEffect')
        window.localStorage.setItem('name', name)
      }, [name])

      const handleChange = event => setName(event.target.value)

      return (
        <div>
          <form>
            <label htmlFor="name">Name: </label>
            <input value={name} onChange={handleChange} id="name" />
          </form>
          {name ? <strong>Hello {name}</strong> : 'Please type your name'}
        </div>
      )
    }

    function App() {
      const [count, setCount] = React.useState(0)
      return (
        <>
          <button onClick={() => setCount(c => c + 1)}>{count}</button>
          <Greeting />
        </>
      )
    }

    ReactDOM.render(<App />, document.getElementById('root'))
  </script>
</body>
```

## Create reusable custom hooks

### setup/16-custom-hooks.html

One of the things we love about programming is the ability to take code, place it in a function, and reuse it in other places in the software. Let’s imagine a scenario where we want to share our localStorage code with other components so other components could synchronize state with localStorage (or we could even do it with different variables in the same component). Take a step back from React specifically and considering how code reuse works in JavaScript in general, we can simply make a function, put our relevant code in that function, and then call it from the original location. That process works exactly the same with React hooks code, so let’s do that!

In the process, we’ll learn a few of the conventions for doing this and we’ll learn about some additional challenges that come with generalizing our code. As always, follow AHA programming practices!

The logic that we have here for storing some state into localStorage and keeping it synchronized could be useful in other areas of our application. Thankfully, React Hooks are pretty Vanilla JavaScript, and sharing that logic is just as straightforward as sharing any other logic in JavaScript. What we're going to do is make a function. We'll call that useLocalStorageState(), and then we'll move these lines of code into that function, and we'll replace them with a call to that function.

```javascript
function Greeting() {
  const [name, setName] = React.useState(
    () => window.localStorage.getItem('name') || '',
  )

  React.useEffect(() => {
    window.localStorage.setItem('name', name)
  }, [name])

  const handleChange = event => setName(event.target.value)

  return (
    <div>
      <form>
        <label htmlFor="name">Name: </label>
        <input value={name} onChange={handleChange} id="name" />
      </form>
      {name ? <strong>Hello {name}</strong> : 'Please type your name'}
    </div>
  )
}

ReactDOM.render(<Greeting />, document.getElementById('root'))
```

We need to generalize the code that's in our function. Instead of a name, it might make more sense to call this state and setState. Instead of getting the item with the string name, it might make more sense for the user of this function to provide us a key for localStorage, so we'll accept a parameter called key. Instead of this as a default value, it might make sense for people to provide us their own default value. We'll accept that as another parameter. We can default that to an empty string just in case they don't want to provide it.

Then we'll replace that with the default value. We'll replace the string name with a parameter that we accept called key. Then let's make sure we update these two references to that old state value as well. Then when we call useLocalStorageState, we're going to need to get access to that stateUpdater function and to the state value itself. Let's return state and setState. We can make our custom Hook have a similar API to useState so it's familiar to people who are used to the useState Hook.

Then we can come down here. We can get our name and our setName from useLocalStorageState. We'll specify our key as name. Then we're done. That's a pretty straight-up refactor from the code that we had before into a custom function. If we type in here Chuck and then refresh, we'll see that Chuck is still in there. One thing I want to call out here is that we prefaced our function with the word use. That's a convention and not required. We could change this to whateverWeWant. Save that. Things will work just as well. We can hit refresh. There we have it.

The reason that we follow this convention is because the eslint-plugin-react-hooks is able to enforce some of the same recommendations and rules on our custom Hooks as it is on the built-in Hooks because it acts under the assumption that functions that begin with use are custom Hooks.

In review, what we did here is we took some code that was in our function component. We moved it into its own function and then called it from our function component. This was no different from any other regular JavaScript refactor, which makes it easy to share logic across components and *even make open source libraries that expose custom Hooks like this*. We also learned the importance of using the use prefix on our custom Hooks so that we follow the community convention and the ESLint plugin can help us avoid mistakes.

> This was no different from any other regular JavaScript refactor, which makes it easy to share logic across components and *even make open source libraries that expose custom Hooks like this*.

Incidentally, one such mistake is happening right now. In this index.html file, I can't have ESLint running to show me the mistakes that I'm making. I made a mistake right here in this dependency array. I wonder if you can figure out what it is. I'm missing one of the dependencies for my callback. Before, we had this key hardcoded as name. It couldn't ever change. My dependency array didn't need to include that. Now, I'm accepting a key as a parameter from the users of the LocalStorageState custom Hook. They could potentially change that value. If they do, then I need to make sure to respond to that change so that I update local storage and not lose any of the user's work.

It's important that in your applications you use and follow that ESLint rule so you can avoid bugs like this. With this in mind, we could make this useLocalStorageState Hook a lot more robust by removing the item at the old key if that key has changed. I'm going to leave that as a fun exercise for you to do later.

```javascript
function useLocalStorageState(key, defaultValue = '') {
  const [state, setState] = React.useState(
    () => window.localStorage.getItem(key) || defaultValue,
  )

  React.useEffect(() => {
    window.localStorage.setItem(key, state)
  }, [key, state])

  return [state, setState]
}

function Greeting() {
  const [name, setName] = useLocalStorageState('name')

  const handleChange = event => setName(event.target.value)

  return (
    <div>
      <form>
        <label htmlFor="name">Name: </label>
        <input value={name} onChange={handleChange} id="name" />
      </form>
      {name ? <strong>Hello {name}</strong> : 'Please type your name'}
    </div>
  )
}

ReactDOM.render(<Greeting />, document.getElementById('root'))
```

## Manipulate the DOM with React refs

### setup/17-dom-refs.html

React is really good at creating and updating DOM elements, but sometimes you need to work with them yourself. A common use case for this is when you’re using a third party library that wasn’t built for or with React specifically. To do this, we need to have some value that’s associated with our component (like state) to store a reference to the DOM element, but doesn’t trigger re-renders when it’s updated (unlike state). React has something specifically for this and it’s called a ref.

You create a ref object with the useRef hook and that object’s current property is the current value of the ref. It can be anything, but if you pass that ref object to a component as a prop called ref, then React will set the current property to the DOM element it creates so you can reference it and manipulate it in your useEffect hook. In this lesson we’ll get to see how that works with a cool library called vanilla-tilt.

Accessing DOM Elements - In general, we want to let React handle all DOM manipulation. But there are some instances where useRef can be used without causing issues. In React, we can add a ref attribute to an element to access it directly in the DOM.

useRef() only returns one item. It returns an Object called current. When we initialize useRef we set the initial value: useRef(0). It's like doing this: const count = {current: 0}. We can access the count by using count.current.

```javascript
// Example:
// Use useRef to focus the input:
import { useRef } from "react";
import ReactDOM from "react-dom";

function App() {
  const inputElement = useRef();

  const focusInput = () => {
    inputElement.current.focus();
  };

  return (
    <>
      <input type="text" ref={inputElement} />
      <button onClick={focusInput}>Focus Input</button>
    </>
  );
}

ReactDOM.render(<App />, document.getElementById('root'));
```

We have a function component called Tilt. Thanks to use some handy class names and some handier CSS, we have it styled in this fancy-looking way but we can make it do something fancy by using a library that I've included called vanilla-tilt. Vanilla-tilt takes a DOM node and makes it react to when the user mouses over that DOM node. The DOM node we want to give it is the DOM node that's created for this element, the tilt root. Remember this is a React element, not a DOM node and React takes that React element and renders it to the DOM.

```javascript
function Tilt({children}) {

  return (
    <div className="tilt-root">
      <div className="tilt-child">{children}</div>
    </div>
  )
}
```

So we need React to give us the DOM node that it creates for this particular React element, so we can wire up vanilla-tilt to it. To do this, we're going to use a ref prop and we need to pass a ref which is an object that has a mutable current property. Let's go ahead and use the React.useRef hook. From that we'll get our tiltRef and then we can copy that, paste it here to our ref. Then the tiltRef is an object that has a current property. That current property is the current value for this ref object.

In our case, because we're passing this ref to a div with a ref prop, that current property will be the DOM node that React creates for this div. If we console.log tiltRef.current, and we save that then we should be seeing the DOM node. We actually see undefined. The reason we see that is because at the time that this function runs, React has not created the DOM node for this div, so the tiltRef.current is currently undefined. In fact, you can initialize that current value by passing an argument to their useRef hook.

```javascript
function Tilt({children}) {
  const tiltRef=React.useRef()
  console.log(tiltRef.current) // output = undefined
  return (
    <div ref={tiltRef} className="tilt-root">
      <div className="tilt-child">{children}</div>
    </div>
  )
}
```

Here, how do we get the DOM node so we can initialize vanilla-tilt on it? We need to have some code that runs after React has updated the DOM and set our tiltRef.current property. Interacting with the DOM is a side effect. The logical place for this would be in a React.useEffect hook.

If we move that console.log in here and we save that, then we get a refresh and now, we are getting the DOM node. From here, we can get our tiltNode from tiltRef.current and then let's go ahead and make some vanillaTiltOptions here.

```javascript
function Tilt({children}) {

  const tiltRef=React.useRef('here')
  React.useEffect(() => {
    console.log(tiltRef.current)
    // console output
    <div class="tilt-root">
      <div class="tilt-child">
        <div class="totally-centered">
          vanilla-tilt.js
        </div>
      </div>
    </div>
  })
      
  return (
    <div ref={tiltRef} className="tilt-root">
      <div className="tilt-child">{children}</div>
    </div>
  )
}
```

We can specify how we want vanilla-tilt to treat this DOM node. We'll say max 25, speed 400, glare true, and max glare 0.5. With that now, we can say VanillaTilt.init() on that tiltNode and with the vanillaTiltOptions. If we save that, we get a refresh. This code runs after React has rendered to the DOM and updated the tiltRef.current property so that we can get access to the tiltNode and initialize vanilla-tilt.

```javascript
function Tilt({children}) {

  const tiltRef=React.useRef('here')
  React.useEffect(() => {
    const tiltNode = tiltRef.current
    const vanillaTiltOptions = {
      max: 25,
      speed: 400,
      glare: true,
      'max-glare': 0.5
    }
    VanillaTilt.init(tiltNode, vanillaTiltOptions)
  })
      
  return (
    <div ref={tiltRef} className="tilt-root">
      <div className="tilt-child">{children}</div>
    </div>
  )
}
```

Now, if we hover, we get that really cool effect. If we unclick the show tilt checkbox, that will unmount the tilt component from the page removing the DOM node from the page. However, there's still a bunch of event handlers on that DOM node and several references to that DOM node from within the vanilla tilt library. That means that the DOM node itself may not exist on the page but it does still exist in memory because there're references to it in vanilla-tilt. Unfortunately, this could lead to a memory leak. If we keep on mounting and unmounting this over and over and over again, then we're going to have a bunch of DOM node sitting around in memory that really aren't needed by the user anymore.

To combat this problem, we can return a function which will be called for every update of our tilt component. In this function, we can say tiltNode.vanillaTilt which is a property that vanilla-tilt is adding to our DOM node .destroy(). This will remove all references of our DOM node from vanilla-tilt and remove all event handlers so that we can avoid memory leaks with our tilt component. What you can't see is that that DOM node has actually been garbage collected properly. We don't need to worry about memory leaks anymore.

```javascript
function Tilt({children}) {

  const tiltRef=React.useRef('here')
  React.useEffect(() => {
    const tiltNode = tiltRef.current
    const vanillaTiltOptions = {
      max: 25,
      speed: 400,
      glare: true,
      'max-glare': 0.5
    }
    VanillaTilt.init(tiltNode, vanillaTiltOptions)
    return () => {
      tiltNode.vanillaTilt.destroy()
    }
  })
      
  return (
    <div ref={tiltRef} className="tilt-root">
      <div className="tilt-child">{children}</div>
    </div>
  )
}
```

 Another thing we should do here is recognize that useEffect is going to be called on every re-render of our tilt component. That's not going to lead to any bugs but it is sub-optimal, because what that means is that we'll call destroy with vanilla-tilt and then we'll call init with vanilla-tilt between every render of our component. We don't need to do that because none of the things in this function can change with re-renders of our tilt component. We're going to add a dependency array here with all the dependencies of our function and because none of the variables in our useEffect callback can change, we don't need to list any dependencies here.

 ```javascript
function Tilt({children}) {

  const tiltRef=React.useRef('here')
  React.useEffect(() => {
    const tiltNode = tiltRef.current
    const vanillaTiltOptions = {
      max: 25,
      speed: 400,
      glare: true,
      'max-glare': 0.5
    }
    VanillaTilt.init(tiltNode, vanillaTiltOptions)
    return () => {
      tiltNode.vanillaTilt.destroy()
    }
  }, [])
      
  return (
    <div ref={tiltRef} className="tilt-root">
      <div className="tilt-child">{children}</div>
    </div>
  )
}
```

 What this is effectively saying is I want to run all the code in the useEffect when the component is initially mounted to the page and then I want to run the return function which will be called for every update of our tilt component, when the component is unmounted from the page. That's another useful optimization we can make for this case.

 In review, the thing that we wanted to do is make this DOM node do some fancy stuff and we included vanilla-tilt on the page so that we could do that. We also included some CSS from the vanilla-tilt author to make our DOM nodes look really fancy. To get access to the DOM nodes so we can initialize vanilla-tilt on it, we're using this ref prop on the div and we pass the thing that we did back from a React useRef call. That ref has a current property that we can use to access the current value of this object.

 The reason that useRef is an object that has a current property is so that we can mutate the current property to be whatever we want without triggering a re-render of our component. We can use refs for more than just DOM nodes like we're using here. We can use it for any value that we want to keep track of and mutate over time without triggering a re-render of our component.

 After a component has been mounted, our useEffect callback is going to be called. We get the tilt node from our tilt ref current property. We create some vanilla-tilt options and pass those to the initialization for our tilt node with vanilla-tilt. Then we return a cleanup function so that we can remove all references of our DOM node in vanilla-tilt and remove all the event listeners that vanilla-tilt put on our DOM node.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script src="https://unpkg.com/vanilla-tilt@1.7.0/dist/vanilla-tilt.min.js"></script>
  <style>
    /*
    Taken from the vanilla-tilt.js demo site:
    https://micku7zu.github.io/vanilla-tilt.js/index.html
    */
    .tilt-root {
      height: 150px;
      background-color: red;
      width: 200px;
      background-image: -webkit-linear-gradient(
        315deg,
        #ff00ba 0%,
        #fae713 100%
      );
      background-image: linear-gradient(135deg, #ff00ba 0%, #fae713 100%);
      transform-style: preserve-3d;
      will-change: transform;
      transform: perspective(1000px) rotateX(0deg) rotateY(0deg)
        scale3d(1, 1, 1);
    }
    .tilt-child {
      position: absolute;
      width: 50%;
      height: 50%;
      top: 50%;
      left: 50%;
      transform: translateZ(30px) translateX(-50%) translateY(-50%);
      box-shadow: 0 0 50px 0 rgba(51, 51, 51, 0.3);
      background-color: white;
    }
    .totally-centered {
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
    }
  </style>
  <script type="text/babel">
    function Tilt({children}) {
      const tiltRef = React.useRef()

      React.useEffect(() => {
        const tiltNode = tiltRef.current
        const vanillaTiltOptions = {
          max: 25,
          speed: 400,
          glare: true,
          'max-glare': 0.5,
        }
        VanillaTilt.init(tiltNode, vanillaTiltOptions)
        return () => {
          tiltNode.vanillaTilt.destroy()
        }
      }, [])

      return (
        <div ref={tiltRef} className="tilt-root">
          <div className="tilt-child">{children}</div>
        </div>
      )
    }

    function App() {
      const [showTilt, setShowTilt] = React.useState(true)
      return (
        <div>
          <label>
            <input
              type="checkbox"
              checked={showTilt}
              onChange={e => setShowTilt(e.target.checked)}
            />{' '}
            show tilt
          </label>
          {showTilt ? (
            <Tilt>
              <div className="totally-centered">vanilla-tilt.js</div>
            </Tilt>
          ) : null}
        </div>
      )
    }

    ReactDOM.render(<App />, document.getElementById('root'))
  </script>
</body>
```

## Understand the React Hook Flow

### setup/18-hook-flow.html

Understanding the order in which React hooks are called can be really helpful in using React hooks effectively. The React Hook Flow Diagram can be really helpful in understanding this, and in this lesson we’ll explore the lifecycle of a function component with hooks with colorful console log statements so we know when one phase starts and when it ends.

I recommend you watch this one slowly and watch it as many times as you need to. Also definitely play around with the code yourself until you feel relatively comfortable with this. Understanding all of this is not critical to your success with using React, and most of the time you won’t need to think about this at all, but understanding it can help you at times.

Sometimes it could be useful to understand the order in which your code is going to be run when you're using React Hooks. I've made this little app that has a checkbox for showing a child, and inside of this box this will be rendered when that checkbox is checked. When you click on this button, it's going to increment the count.

The way that this works is we have a child component here that's maintaining a countState, and then that has a whole bunch of useEffects here, which are simply logging to the console when the callback is called and logging to the console in a cleanup function that it provides. Then we create our React element for rendering to the page, and then we log to the console that our render is finished and then we return that React element we created. We do the same thing for our App component, except here we're maintaining a showChild Boolean state. We have all those useEffects, and then we render a few React elements here for rendering this UI.

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
  <script type="text/babel">
    // https://github.com/donavon/hook-flow

    function Child() {
      console.log('%c    Child: render start', 'color: MediumSpringGreen')

      const [count, setCount] = React.useState(() => {
        console.log('%c    Child: useState callback', 'color: tomato')
        return 0
      })

      React.useEffect(() => {
        console.log('%c    Child: useEffect no deps', 'color: LightCoral')
        return () => {
          console.log(
            '%c    Child: useEffect no deps cleanup',
            'color: LightCoral',
          )
        }
      })

      React.useEffect(() => {
        console.log(
          '%c    Child: useEffect empty deps',
          'color: MediumTurquoise',
        )
        return () => {
          console.log(
            '%c    Child: useEffect empty deps cleanup',
            'color: MediumTurquoise',
          )
        }
      }, [])

      React.useEffect(() => {
        console.log('%c    Child: useEffect with dep', 'color: HotPink')
        return () => {
          console.log(
            '%c    Child: useEffect with dep cleanup',
            'color: HotPink',
          )
        }
      }, [count])

      const element = (
        <button onClick={() => setCount(previousCount => previousCount + 1)}>
          {count}
        </button>
      )

      console.log('%c    Child: render end', 'color: MediumSpringGreen')

      return element
    }

    function App() {
      console.log('%cApp: render start', 'color: MediumSpringGreen')

      const [showChild, setShowChild] = React.useState(() => {
        console.log('%cApp: useState callback', 'color: tomato')
        return false
      })

      React.useEffect(() => {
        console.log('%cApp: useEffect no deps', 'color: LightCoral')
        return () => {
          console.log('%cApp: useEffect no deps cleanup', 'color: LightCoral')
        }
      })

      React.useEffect(() => {
        console.log('%cApp: useEffect empty deps', 'color: MediumTurquoise')
        return () => {
          console.log(
            '%cApp: useEffect empty deps cleanup',
            'color: MediumTurquoise',
          )
        }
      }, [])

      React.useEffect(() => {
        console.log('%cApp: useEffect with dep', 'color: HotPink')
        return () => {
          console.log('%cApp: useEffect with dep cleanup', 'color: HotPink')
        }
      }, [showChild])

      const element = (
        <>
          <label>
            <input
              type="checkbox"
              checked={showChild}
              onChange={e => setShowChild(e.target.checked)}
            />{' '}
            show child
          </label>
          <div
            style={{
              padding: 10,
              margin: 10,
              height: 30,
              width: 30,
              border: 'solid',
            }}
          >
            {showChild ? <Child /> : null}
          </div>
        </>
      )

      console.log('%cApp: render end', 'color: MediumSpringGreen')

      return element
    }

    ReactDOM.render(<App />, document.getElementById('root'))
  </script>
</body>
```

Let's go ahead and take a look at what happens when we initially load this page. I'm going to refresh, I'll open up our DevTools, and I'll scroll down here to the app, so we can follow along in the code with what we're seeing in the console. The first thing that we see is this app render start. That's the first thing that happens when we call ReactDom.render our app. It calls our app Function Component. The next thing that happens is we call react.useState and immediately React is going to call this function to retrieve the initial state for our show child state. That's why we're getting this app useState callback called.

```javascript
function App() {
  console.log('%cApp: render start', 'color: MediumSpringGreen')
  // console output - App: render start
}

const [showChild, setShowChild] = React.useState(() => {
  console.log('%cApp: useState callback', 'color: tomato')
  return false
  // console output - App: useState callback
})
```

Then, we call all these React useEffects, but you'll notice that the logs in those are not the next thing that appear in our console. Instead, we actually create this element and then we get a log to the console for app render end. Once that happens, React actually is updating the DOM. *Then, asynchronously later, it's going to call our useEffect callbacks, one at a time in the order in which they were called. useEffect is called after React finishes rendering.*

```javascript
const element = ()
console.log('%cApp: render end', 'color: MediumSpringGreen')
return element
// console output - App: render end

const [showChild, setShowChild] = React.useState(() => {
  console.log('%cApp: useState callback', 'color: tomato')
  return false
  // console output - App: useState callback
})
```

We come up here to the top, mostly, app useEffect to no deps is the first one that appears. We don't get our cleanup because there's no cleanup necessary yet, because right now, we're just mounting the component, and we haven't had any updates yet. Next, we get our useEffects empty deps, right here. We have an empty list of dependencies there and then useEffect with dependency - [showChild]. That's our show child's state. That's the next thing that gets called here.

```javascript
React.useEffect(() => {
  console.log('%cApp: useEffect no deps', 'color: LightCoral')
  // console output - App: useEffect no deps
}

React.useEffect(() => {
  console.log('%cApp: useEffect empty deps', 'color: MediumTurquoise')
  // console output - App: useEffect empty deps
}

React.useEffect(() => {
  console.log('%cApp: useEffect with dep', 'color: HotPink')
  // console output - App: useEffect with dep - [showChild]
}
```

Now, let's take a look at what happens when we click on show child. Remember that *App: useEffect with dep,* is the last console log that we saw when we initially mounted the component. If I click show child, then we're going to get an app render start. When we click show child, that triggers the onChange to set show child to the checked value of our check box input.

The setShowChild is going to trigger a re-render of our app, which is why we get our app render start. Come up here to the top again. We'll say app render start, and we'll go through all of the code just like we had at the previous render, except this time you'll notice we don't have an app useState callback, we go straight from app render start to app render end.  This is because React has already retrieved the initial state value for our show child state, and it doesn't need to retrieve that value again. *Any time you use a function callback for useState, that function is only going to be called when this component is initially rendered for the rest of the lifetime of that component.* We go through all those useEffect cause again, we create our element, and then we lock to the console that the app render has finished.

```javascript
<input
  type="checkbox"
  checked={showChild}
  onChange={e => setShowChild(e.target.checked)}
/>

function App() {
  console.log('%cApp: render start', 'color: MediumSpringGreen')
  // console output - App: render start
}

const element = ()
console.log('%cApp: render end', 'color: MediumSpringGreen')
return element
// console output - App: render end
```

Then React calls our child to start rendering of that child. *One thing that I want to stress here is that we're creating our element which includes creating the child right here.* You'll notice that we get to this - *console.log('%cApp: render end', 'color: MediumSpringGreen')* line of code before we start rendering the child. *The important thing to remember here is that just because you create a React element, doesn't mean that React element's function is going to get called, because you're not calling the function, React is.*

```javascript
const element = (
  <>
    <div
      style={{
      padding: 10,
      margin: 10,
      height: 30,
      width: 30,
      border: 'solid',
      }}
    >
      {showChild ? <Child /> : null}
    </div>
  </>
)

function Child() {
  console.log('%c    Child: render start', 'color: MediumSpringGreen')
  // console output - Child: render start
})

      function Child() {
      console.log('%c    Child: render start', 'color: MediumSpringGreen')

      const [count, setCount] = React.useState(() => {
        console.log('%c    Child: useState callback', 'color: tomato')
        return 0
      })

function App() {
  console.log('%cApp: render start', 'color: MediumSpringGreen')
  // console output - App: render start
}

const element = ()
console.log('%cApp: render end', 'color: MediumSpringGreen')
return element
// console output - App: render end

React.useEffect(() => {
  console.log('%cApp: useEffect with dep', 'color: HotPink')
  // console output - App: useEffect with dep - [showChild]
}

  
  Child: useState callback
  Child: render end
  Child: useEffect no deps
  Child: useEffect empty deps
  Child: useEffect with dep
App: useEffect no deps cleanup
App: useEffect with dep cleanup
App: useEffect no deps
App: useEffect with dep
```
