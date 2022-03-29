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
