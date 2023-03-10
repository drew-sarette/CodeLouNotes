# React
React is a JavaScript library used to build complex and interactive user interfaces using components.  It is lightweight and minimalistic, leaving many choices up to the developer.

Benefits of using React:
- Better organized code, due to reusing components.
- Components can watch for changes on the server and reload themselves, without reloading the whole page. 

React relies on JSX and Babel. JSX allows you to write HTML inside of your javascript, and adds it to the dom for you.  Babel is a transpiler, that takes modern JS and rewrites it to be compatible with most browsers.

To practice using react without any setup, go to [codesandbox](codesandbox.io) 

# JSX 
Importing react and react-dom gives you the basic features of react. The react import itself enables you to use JSX. JSX offers several benefits:
- expressions can be embedded in html using {}
- can be used in loops, if statements, etc...
- embedded content in {} is automatically escaped by react-dom, preventing injection attacks

Here is an example of what a simple react app using JSX might look like:
```
import React from "react";
import ReactDOM from "react-dom";

const name = "Drew";
ReactDOM.render(
  <div>
    <h1>JSX practice</h1>
    <ul>
      <li>lists have bullet points</li>
      <li>unless they are ordered</li>
      <li>Lists are great!</li>
    </ul>
    <p>{name} is the best thing since sliced bread</p>
  </div>, 
  document.getElementById("root"))
```
Note that the ReactDOM.render function takes three paramaters
1. what to render (JSX),
2. where to put it (inside the root element in this case)
3. an optional callback for when the render is complete.

## Adding attributes to elements in JSX
Remember that JSX is closer to JavaScript than HTML, so when specifying an attribute, use camelCase. For example ```<h1 className="classy-class">```

Use " when specifying a hardcoded attribute value, but use only {} when supplying a variable value:
```
<h1 className="classy-class">
<h1 className={lowClassClass}>
```
Don't try to use both {} and ""

## Loading a JSX script
The browser will notice if there are out of place characters such as <> in a javascript file, and throw errors. Make sure to specify JSX in the type attribute of the script tag to prevent that
```<script src="../src/index.js" type="text/JSX"></script>```

## Inline Styles in JSX
To give an element inline styling in JSX, you must pass in an object. The end result will have {{}}
ReactDOM.render(
  <h1 style={{color: red}}>JSX practice</h1>, 
  document.getElementById("root"))

# Components 
A react component is created using a function in a Heading.jsx file. 
```
import React from "react" // First need to import

function Heading() { //convention is Pascal case
  return <h1>Custom heading</h1>;
}

export default Heading;
```

then in the main file, named App.jsx, you can import the component
```
import React from "react" // First need to import
import Heading from "./Heading" // extensions are optional
// import all your components here

function App() {
  return <>
    // list your components here, using self-closing tags when they dont have children
    <Heading /> //convention is leave space before closing
  </>
  export default App;
}
```

Then the simplified index.js file looks like this:
```
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";

ReactDOM.render(<App />, document.getElementById("root"));
```
You should create a components folder and possibly subfolders to organize your components, and updat the paths in the imports accordingly.

