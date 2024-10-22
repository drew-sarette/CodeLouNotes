# Throw
The throw operator generates an error, and stops the code from running. It logs and sends the following object (or primitive) to a catch block.

```
console.log("Valid statements"); //=> valid statements
throw "knife"; //=> "knife"
console.log("valid statements"); // not executed.
```
Though anything can be thrown, including strings or numbers, it is best to use an object with at least a name and a message property.

# Try/Catch
if there is a try/catch, throw will skip to the catch, and then the script will continue normally

```
try{
    throw "knife";//=> sends knife over to catch
    console.log("valid statement");// not executed
}
catch(error){
    console.log("Caught " + error);//=> "Caught knife"
}
finally {
    console.log("ouch"); //=> "ouch"
}
```
# Finally
Finally will be executed, whether there is an error or not.
The finally block will be run even if there is a value returned, an error is thrown, or some other jump out of the try/catch block occurs

# Error object.
Whenever an error occurs, JS generates an object containing the details. The object can then be passed to catch.

An error object has two main properties:
1. name: "ReferenceError" for an undefined variable, for ex.
2. message: string containing details
3. stack: not supported in all environments. String with sequence of nested calls that lead to the error.

JS has built in constructors for many errors:
```
let error = new Error(message);
// or
let error = new SyntaxError(message);
let error = new ReferenceError(message);
```