# Functions
A function is a block of organized, reusable code that serves a single purpose.

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
A closure is the combination of a function and the lexical environment within which that function was created.

If a function returns another function, the inside function is not executed until the outside function is invoked.

That inside function then has access to its own scope + its parent's scope because of lexical scoping.

Closures are usefull for creating a family of related functions:
```

```

a closure can be used to "memoize" a function. A memoized function stores its previous values in a private cache, and only computes new values if it has not done so already:

```
const lenghtyCalc = memoizedLenghtyCalc();
// memoizedLengthyCalc returns a function, not a value. LengthyCalc is called to calculate a result. It has access to the cache in the memoized function through the closure.

function memoizedlengthyCalc(x){
    let cache = {};
    return function (x){
        if (x in cache){
            return cache[x];
        }
        let result = someFormulaHere(x);
        cache[x] = result;
        return result;
    }
}
```



# Arrow functions
 A simpler and more compact way to write functions:
- no "function" or "return" keywords
- no parentheses or brackets whatsoever
- just an argument (or multiple arguments in parentheses) followed by => and the statement to perform

