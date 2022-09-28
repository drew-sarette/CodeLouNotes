<<<<<<< HEAD
# Function
Def - a block of organized, reusable code used to perform a single related action
=======
# Functions
A function is a block of organized, reusable code that serves a single purpose.
>>>>>>> a47a16d3d87e9e66a9638f518fa29d8d81565b5d

<<<<<<< HEAD
arguments are what is passed to a function when you invoke it

parameters are what is listed in the function definition

the arguments object is accessible from inside a function. It is like an array containing all the arguments passed. It does not include forEach or other array methods

variables declared using const or let inside of a function are scoped to that function

# IIFE Immediately Invoked Function Expression
used to avoid poluting global variables.
```
(function() {
    console.log(`hello`);
})(); // the closing () invokes the function.
```
# Closures
Q: is there a practical reason we should know about closures?
a closure is the combination of a function and the lexical environment within which that function was created.

if a function returns another function, the inside function is not executed until the outside function is invoked.

that inside function then has access to its own scope + its parent's scope because of lexical scoping.

# Arrow functions
 A simpler and more compact way to write functions:
- no "function" or "return" keywords
- no parentheses or brackets whatsoever
- just an argument (or multiple arguments in parentheses) followed by => and the statement to perform

=======
A function is *declared* using the function keyword, (), and the statements to be executed are put into {}

```
function newFunc (params) {
    //statements
}

const otherFunc = function (params) {
    //statements
}
```
The *parameters* are variables passed into a function. They are called *arguments* when the function is called and they are being passed in.

The arguments object is an array-like object accessible inside functions that contains the values of the arguments passed to the function.

```
console.log(arguments[2]);
//logs the value of the third argument passed into the function
```

## Scope
Variables declared with const or let have function scope. They are not accessible outside the function. However, functions can access variables in parent functions.

## Immediately Invoked Function Expression (IIFE)
A function that is run as soon as it is defined. Entire function is enclosed in (), and then invoked with another set of () and a ; right after. They are anonymous.
```
(function () {
  // …
})();
```
Typically used for initialization, because it avoids polluting the global namespace.  If the 

## Closures
Allow access to variables that were in function scope earlier from outside the function. Can be used with an IIFE
```
let greeting = (function() {
    let message = 'hello';
    let getMessage = function() {
        return message;
    };
    return {
        getMessage: getMessage,
    };
})();
console.log(greeting.getMessage()); // hello
```
according to MDN, a closure is the combination of a function bundled together with its lexical environment. Lexical environment refers to an inner function's access to its parent functions' variables.

In this example, the function displayName() is returned from makeFunc *before it is executed*. This is possible because JS creates a closure tying displayName to its lexical environment, so that it can access name at a later time.

```
function makeFunc() {
  const name = 'Mozilla';
  function displayName() {
    console.log(name);
  }
  return displayName;
}

const myFunc = makeFunc();
myFunc();
```
The benefit of using the IIFE version is that it cuts out the extra function that had to be made in the second example.

A common use of closures is an event in a web browser. 
```
function makeSizer(size) {
  return function () {
    document.body.style.fontSize = `${size}px`;
  };
}

const size12 = makeSizer(12);
const size14 = makeSizer(14);
const size16 = makeSizer(16);
```
is an easy way to create three different custom functions.

Q: What is a callback?
Q: What is the benefit of returning an object containing a function vs just a function?

## Arrow Functions
Simpler way to write a function expression. Not a perfect substitute for a standard function. Different treatment of 'this' keyword. In a standard function, this refers to the function object.  In an arrow function, this refers to the window object. Dont use this in arrow functions!

```
let greeting = function() {
    return 'hello';
}

let greeting = () => {
    return 'hello';
}

// for no params, it looks like this:
let greeting = () => 'hello';

//for one param, it looks like this
let greeting = name => 'hello ' + name; 
```

## call, apply, and bind

The this variable always refers to an object.
- If a method is called on an object, 'this' refers to that object
- If a regular function call is made, 'this' refers to the global object. In a browser, that is the window object.

call, bind, and apply are used to explicitly set the value of 'this'

For example, if you have two objects, and want to use a method from one object on another, you can use call.
```
const john = {
  name: 'john',
  age: '74',
  job: retired;
  greeting: function(style) {
    swirtch(style){
      case 'formal':
      console.log(`Good day to you, my name is ${this.name} and I am ${this.age} years old. I am ${this.job}`)
      break;
      case 'casual':
      console.log(`Hey, I'm ${this.name} and I'm ${this.age}. I am ${this.job}`)
      break;
    }
  }
}
const mark = {
  name: 'mark',
  age: '28',
  job: funemployed;
}

john.greeting('casual');
//`Hey, I'm john and I'm 74. I am retired
//'this' refers to john object

john.greeting.call(mark, 'casual');
//Hey, I'm mark and I'm 28. I am funemployed
//'this' is set to refer to mark (first argument).
```

apply is similar, except it takes only two objects
```
john.greeting.apply(mark, ['formal']);
//Good day to you, my name is mark and I am 28 years old. I am funemployed
```
Use apply when the arguments are all closely related in an ordered sequence.

Bind returns a copy of the function, with the value of 'this' and all arguments preset.
```
const greetMark = john.greeting.bind(mark, 'casual');
greetMark();
//Hey, I'm mark and I'm 28. I am funemployed
```

## Default parameters
Set a default value for one of the parameters.  These assignments must come after any normal parameters.
```
function sayHi (name = 'world'){
  console.log('Hello' + name);
}
sayHi();
//Hello world
sayHi('Beelzebub');
//Hello Beelzebub
```

a rest parameter collects all arguments into an array, no matter the number!

```
function sayHi (greeting, ...names){
  names.forEach(name => console.log(greeting + " , " + name));
}
sayHi('hi', 'Marty', 'Pashmeena', 'Ron');
//hi Marty
//hi Pashmeena
//hi Ron
```

the spread operator is the opposite of the rest parameter. It takes a single array as argument, and spreads it into individual parameters. It can be used in conjunction with the rest parameter to handle any number of arguments.

```
let letters = 'ljdsssii';
function logLetters (char1, char2, char3, char4, ...others) {
  console.log(char1, char2, char3, char4);
  console.log(others);
}

logLetters(...letters);
//l j d s s s i i
```

>>>>>>> a47a16d3d87e9e66a9638f518fa29d8d81565b5d