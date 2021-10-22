# Complete Intro React Notes
Link: https://jscomplete.com/learn/complete-intro-react

## What is React?
**React is a JavaScript "library" for Building User Interfaces.
** It's not a framework. It's a non-complete solution and you'll
often use React with other libraries with React to achieve your
solution. React doesn't assume anything about the other parts
of the solution.

## What are "frameworks" (and "libraries")?
Frameworks serve a great purpose of making smart design
decisions for you to focus on writing applicaiton logic.
This is great for young teams and startups, but may conflict
for experienced developers with larger codebases it can be a
deal breaker.

Frameworks are inflexible and usually want you to code a
certain way, large and are full of features, bloated and
carry baggage you won't need. This is changing but frameworks
are still not ideal. Some are modular, but don't follow the
pure Unix philosophy, that is:
> Write programs that do one thing and do it well.
> Write programs to work together.
> — Doug McIlroy

React follows this philosophy. It's small that focused on
a single goal, and does it extremely well.

## On building UIs with React
User Interfaces are simply controls for the users to interact
with the program without affecting their source code.
React is for building these interfaces.
Any device understanding JavaScript can utilize React to build
the interface. This usually entails using React to describe
Web UIs.

React is really like **describing** what we want it to do.
Without React, we'd end up using native Web APIs and JS:
not easy. This makes React "declarative"; we describe, and
React takes care of the "how". In a similar way that HTML
handles static data declaratively, so does React represent
dynamic data.

React also introduced the idea of the virtual DOM (Document
Object Model), which treats HTML (and XML) docs as tree
structures to enable changing the document's structure,
style, and content. **React is the language of UI "outcomes"**
today, and devs can just simply describe interfaces in terms
of a final state (like a function). React takes care of
updating those UIs in the DOM based on functions,
**i.e. React is the outcome based UI language**.

# React: The Language
The basic premise of this section is an example involving
making a to-do list app. Without React, you have to worry
about all these DOM operations to create, insert, delete,
& update these DOM nodes, and when they need to happen and
how to perform these operations efficiently. React does this
work: all you have to do is place the "todo" array in the
"state" of your app and command React to display that state
in the UI, then do the data operations on that array.
It's easy to work and understand with.

## React's Tree Reconciliation
React serves as an agent to work with the browser's API,
(the DOM API) i.e. the DOM tree. This is good because
manual work on the DOM tree is a nightmare, as every single
action taken on the browser is done on a single thread,
even banal events like scrolling.
React manages this instead of you doing so manually by
managing a virtual representation of the tree and cacheing/
batching operations whenever possible, reducing the active
operations taking place when it performs these DOM operations.
React also compares two different version of these trees
of elements and only updates the new operations (sub trees)
based on the differences of the two, making a new tree in
the process.

This is the **Tree Reconciliation Algorithm** that makes
React efficient to work with regarding the DOM tree.

Additional points:
- React gives devs a friendly "virtual browser" to work with
- React is **"Just JavaScript"**, ie learn the small amount
of React and the limit is how much JS you know
- **React Native** allows you to build easy mobile apps
- React is tested live by Facebook and has little bugs
upstream

# Your First React Example
- Seeing the practical benefit of tree reconciliation process
by working on a simple example
- Example is generating and updating a tree of HTML elements
twice, using Web API, then using React API
- No components or JSX in this example
- The update is done through a JS internal timer, which isn't
done in React, but for demonstration purposes.

#### Method #1: Using Web DOM API directly
	document.getElementById('mountNode').innerHTML = `
	  <div>
	    Hello HTML
	  </div>
	`;

#### Method #2: Using React API
	ReactDOM.render(
	  React.createElement(
	    'div',
	    null,
	    'Hello React',
	  ),
	  document.getElementById('mountNode2'),
	);

- `ReactDOM.render` & `React.createElement` method are core API
methods in a React application, React apps can't exist without
using these two

### ReactDOM.render
- The **entry point** into a browser's DOM
- Has two arguments:
	1. WHAT React element to render to the browser
	2. WHERE to render the React element in the browser.
	- Has to be a valid DOM node that exists in plain HTML.
	- Example uses a special `mountNode2` element which
exists in playground display area (the first `mountNode` is used
for native [HTML] version).

So what's exactly a React element? A VIRTUAL element describing
a DOM element. (It's what the `React.createElement` API method
returns.)

### React.createElement
- In React we represent DOM elements with **objects** using calls
to the `React.createElement` method as opposed to using Strings
- These objects in React are known as "React elements"
- The `React.createElement` function has many arguments:
	1. The HTML "tag" for the DOM to represent, which is `div` in example
	2. Any attributes (like `id`, `href`, etc) we want the element to have
	3. Content of the DOM element, like the "Hello React" string.
	4. (Optional third arguement, &) any subsequent arguments form
the **children** list. (An element can 0 or more children).
- (!) React.createElement can also be used to create elements from
React components
- React elements are created in memory, to show them in the DOM,
we use `ReactDOM.render` method
- Executing the 2 methods show "Hello HTML" & "Hello React"

#### Nesting React elements
- We have two nodes:
	- one controlled directly by DOM
	- one controlled by React API (which *uses* the DOM API)

- Major diff between the two:
	1. The HTML verion uses a String to rep. the DOM tree
	2. The React version uses pure JS calls, & reps the DOM tree w/ an object

- In React, *every* HTML element is rep'd by a React element
- Adding more elements to the UI:
	- HTML ver. you inject new element tag direct inside template
	- React ver. you add more arguments after the third,
in example, we can add another `React.createElement` as argument that renders
another `input` element.

- **What does React do so well vs vanilla HTML format?** The answer: **updating**


### Updating React elements
- The example is to make the time string **tick** every second
- Repeating JS functions with `setInterval` Web API is easy:
	- Put all the DOM manips for both ver. into a function
	- name it `render`
	- then use it in a `setInterval` call (argument) to repeat every second

- **Mind blow**:
	- You can't type in the text box of the native HTML version
		- This is because the whole DOM tree is taken by every tick
	- You *can* type it in the React version
		- This is because React is only changing the content of the `pre` element
	- Chromium dev tools can be useful to highlight these types of updates
	- This is a demonstration of React's **diffing** algorithm in action
		- Only changes what needs to be updated due to React's virtual repping
		- Removes having to **think** about updating UIs and focus on data states


## React is about components











## Expressions in JSX
- You can include a JS expression using a pair of curly brackes anywhere in JSX
- **Only expressions** can be included in the curly brackets, i.e. **anything that
returns a value**
- BTW, you should know what a **ternary operator** is, it's an expression
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)
- Keep the logic in the curly brackets in a function:
	- Put code in function
	- make it return something
	- put it in curly brackets

- JS variables are also expressions

- JS object literals are also expressions

- Using the `style` attribute is special, use object as value & object defines styles as it we're setting them throught the JS DOM API
- React translates...........
- Using CSS class names may be better in production.


## JSX is not a template language

## Create components using classes
- React supports creating components using JS syntax, too
- 

## Functions vs classes
- React hooks relase introduced a new API in 2019 to make a function component stateful (and give it many other features)
- i.e. this is functions (new) vs classes (advanced &|| old)
- [list reasons why API is superior]
	- You don't have to work with class "instances" and implicit state (i.e. less "suprise" in code)
	- ...
	- ...
- Focus on using the new API as a newcomer

### Components vs Elements
- "components" and "element" are interchanged in tutorials
- Compoments are templates
- Elements are what get returned from components

## Benefits of components
- "component" as a term is used in many fr..
- components can be reused relatively easily

## What exactly are hooks?
- class ends here 	GET TO HERE IN THE NOTES
