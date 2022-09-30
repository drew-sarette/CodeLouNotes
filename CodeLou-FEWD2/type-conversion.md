# Type Conversion
The global objects Boolean, Number, and String can be used to explicitly convert values.  
## Boolean
There is a set list of "falsy" values that convert to false, and all others convert to true
 Falsy values:
 - false
 - 0
 - -0
 - '', "", ``
 - null
 - undefined
 - NaN
 - document.all

 ```
 console.log(Boolean(false)); // false
 console.log(Boolean('false')); // true
 console.log(Boolean({})); // true
```
## Converting to Number
Number() is used to convert a value to a number.  Whitespace is ignored and an empty string converts to 0. For non-primitives and strings that do not represent numbers, NaN is returned.
```
Number(true);
// => 1
Number(false);
// => 0
Number(null);
// => 0
Number(undefined);
// => NaN
Number("123");
// => 123
Number();
// => 0
```

## Converting to String
String() converts any primitive value to a string. An array is converted into a comma delimited list. To change the delimiter use the join method:

```
const arr = [1, 2, null, false];
String(arr);
// => '1,2,,false'
arr.join("");
// => '12false'
```

To convert objects to strings, you can provide a ```toString``` method: (Object to Primitive Conversion)[https://javascript.info/object-toprimitive]

# Type Coercion
Depending on the context, JS will implicitly convert a value.

## Boolean Context
Values will be coerced into Booleans in these contexts:
- condition of an if statement
- first operand of ternary operator ```?```
- operand of the NOT operator ```!```
- operands of && or ||
- Note: && and || will return one of the original operands, not necessarily a Boolean

## String Context
If the addition operator is used and one operand is a string, the other will be coerced into a string as well.

## Numeric Context
- unary and binary operators +, -, *, /, %, etc... will coerce values to numbers.
- use === or !== to avoid conversion mistakes
- use Number() rather than implicit conversion to avoid unintended results
