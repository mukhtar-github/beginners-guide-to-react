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
