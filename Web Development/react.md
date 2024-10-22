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
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <div>
    <h1>JSX practice</h1>
    <ul>
      <li>lists have bullet points</li>
      <li>unless they are ordered</li>
      <li>Lists are great!</li>
    </ul>
    <p>{name} is the best thing since sliced bread</p>
  </div>
);
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
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<h1 style={{color: red}}>JSX practice</h1>);

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

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```
You should create a components folder and possibly subfolders to organize your components, and updat the paths in the imports accordingly.

# Import and Export in React
Note that when exporting or importing components, you need to use export default, and leave out the {};

This is because if a module exports only one value (like a component) it is best to use a default export. Curly braces are used only with named exports and imports.

# Properties (props) 
Props are used in react to pass information into the components. While attributes are added in the component file, such as the className use above, props are given when the component is instantiated: 
```
import React from "react";
import Card from "./Card";
import contacts from "../contacts";

function App() {
  return (
    <div>
      <h1 className="heading">My Contacts</h1>
      {contacts.map((c) => (
        <Card
          key={c.id}
          name={c.name}
          email={c.email}
          phone={c.phone}
          imgURL={c.imgURL}
        />
      ))}
    </div>
  );
}

export default App;

```
This code creates a Card component for each contact in a contacts array. It passes the specific info for each contact as a prop, which is then accessible in the component like this:
```
import React from "react";

function Card(props) {
  return (
    <div className="card">
      <div className="top">
        <h2 className="name">{props.name}</h2>
        <img
          className="circle-img"
          src={ props.imgURL }
          alt="avatar_img"
        />
      </div>
      <div className="bottom">
        <p className="info">{ props.phone }</p>
        <p className="info">{ props.email }</p>
      </div>
    </div>
  );
}

export default Card;
```

The app component works because React knows to render each component generated by a map function between {} automatically.

In React, you need to supply a key prop for a component whenever you render a list of items using the map() method or any other loop to help React identify which items have been added, removed, or modified. The key prop should be a unique value that remains consistent across renders for each item in the list.

# Rendering using Map()
```
import React from "react";
import Header from "./Header";
import Footer from "./Footer";
import Note from "./Note";
import notes from "../notes";

function App() {
  return (
    <div>
      <Header />
      {notes.map(n => <Note key={n.key} title={n.title} content={n.content} />)}
      <Footer />
    </div>
  );
}

export default App;
```
This function outputs an array of Note components, each with unique props taken from the notes.js file.  Whenever this method is used, react requires each note to have a unique "key" prop, that identifies it in the array.

# Conditional rendering

T

# Destructuring
Arrays can be destructured using 
```
const example = [ "one", 2, "three" ];

[ a, b, c ] = example;
console.log(a, b, c) // => "one", 2, "three";
```

rest syntax can be used to split an array into a variable plus the other elements as a new array:
```
[x, ...rest] = example;
console.log(x, rest); //=> "one", [2, "three"]
```

objects can be destructured using
```
const myObj = { name: "Drew",  epithet: "The Yellow Dart" };

const { name, nickname = "Drewsky", epithet: moniker };
console.log(name, nickname, moniker);
// => "Drew", "Drewsky", "The Yellow Dart"
```
When destructuring objects, properties can be renamed using a semicolon. If a property is not in an object, it will return undefined. If a default value is supplied, it will use that. 

destructuring can be used to get variables from nested objects and arrays:
```
const book = {
  title: "How to Avoid Huge Ships",
  pages: 492,
  chapters: [
    "Introduction",
    "Barges",
    "Aircraft Carriers",
    "Pesky Pirates"
  ]
  author: {
    first: "Anatoly",
    last: "Bresznowsky",
    children: [
      "Anna",
      "Marco",
      "Pyotr"
    ]
  }
}
const { pubdate = "1972", title, chapters: [ firstChapter, ...rest ], author: { children: [firstborn] } } = book

console.log(firstChapter, firstborn) //=> "Introduction", "Anna"
```



# hooks and state
Hooks must be used inside of a functional component.