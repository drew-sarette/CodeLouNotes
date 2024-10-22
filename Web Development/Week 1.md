# Javascript Variables
# Primitives
- string
- number 
- boolean
- bigint
- symbol
- null
- undefined

Primitives are *immutable* . They cannot be changed.  Variables can be assigned to a different primitive, but the value itself is unaffected. When a method is called on a primitive, an imaginary object is implicitly created and the method is called on that object. 

    typeof someVariable;  // Returns what datatype it is

## Number
Includes floats and ints between Number.MIN_VALUE and Number.MAX_VALUE (+ and -), NaN.

    Number.isSafeInteger(someNumber);  // true if safe
    
NaN is not equal to anything, including itself.
Sometimes you need to convert a string to a number. Use the Number() constructor

    const a = new Number('123'); // a === 123 is false
    const b = Number('123');     // b === 123 is true
    a instanceof Number;         // is true
    b instanceof Number;         // is false
    typeof a // "object"
    typeof b // "number"

## Bigint
use for unsafe numbers. Add an "n" to the end of the number at assignment:

    const inchesToMoon = 9182739327764813745698245387686n
## String
Strings can be created with "" '' or  \`\`
Inside of `` , a string can include  ${variable or expression here}, which will be evaluated as code.
If quotations are inside a string, alternating levels of "" and '' must be used. 
## Boolean
Simply true or false
## Null
A variable is intentionally assigned null to show it is empty
## Undefined
Undefined is returned when a variable is unintentionally left empty.
- when a variable is created but not initialized, it is undefined.
- the value of a non-existing key in an object is undefined.
## Symbol
# Declaration
- const cannot be reassigned or redeclared
- let can be reassigned but not redeclared
- var can be reassigned and redeclared

Prefer the most restrictive option. If the variable does not *need* to be reassigned, use const. Never use var. Var is too flexible and can behave unexpectedly.
# Scope
Scope is the current context of execution where values can be seen and referenced. JS has global, module, function, and block scope.
## Global
variables declared outside of a function or block of code, can be used by any script or function on the page.  if a variable is assigned without being declared 

    sloppy = 2;
    
it becomes a global variable automatically. Do not use global scope unintentionally, as it can overwrite window variables and be overwritten by window object.
## Function
variables declared in a function cannot be accessed outside that function, including function arguments (at least inside the function).
## Block
code cannot "see" into {}. code inside of {} can access outside variables, however.  Var breaks this rule, and is not scoped by {}.

# Operators
## math
\+ - * / are the usual. \** is an exponent. % is remainder after division.
## increment
a++  returns a, then adds 1 to a. ++m adds 1 to m, then returns m. Can also use decrement operator (--)

    a = 2;
    b = a++; // b = 2, a = 3
    m = 7;
    n = ++m; // m = 8, n = 8

## assignment
A shorthand for x = x + f() is x += f(). Use with other operators, 
## comparison
- = is for assignment
- == is not to be used. It does not care about data types.
- === is "strictly equal to". Only same value and type will be equal.
- 
# Objects
you can const an object, but still change its properties. EG

    const violin = {
	    maker: Guadagnini,
	    owner: me,
	    year: 1780,
	    paidFor: false
	  }
Const does not affect an object like it does a variable.  
## Destructuring Assignment
Valuable way to get info from an object an array, such as when working with a JSON from an API. Can be used to clean up unnecessary if statements, and is part of working with many libraries

       const { owner, price = 'unknown', ...rest } = violin; 
       // const the named properties from the violin object
       console.log(price); // price not found in violin, defaults to unknown
       console.log(owner); // returns me
       console.log(rest); // returns obj containing maker, paidFor, year
    
when used on arrays, the index is used rather than the key:

    const stuff = ['oil', 'vinegar', 'eggs'];
    const [ingredient1, ingredient2, ingredient3] = stuff;
    //ingredients are taken in order from stuff
    

