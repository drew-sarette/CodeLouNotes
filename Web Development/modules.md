# Modules
A module is a file that exports some code.

Benefits:
- you can import only the code you need
- it is clearer what each module is doing and how they relate

To use modules:
- modern browser
- use .js or .mjs (.mjs does not work in all browsers, .js does)
- use import and export statements
- use type="module" in your script tag

## Exports

### Named Exports
Can just use 'export' before any top level variable, function, etc...

can use 
```
export {thing1, thing2, thing3};
```
 at the end of  the file to export named items in a list.

- default
- aggregate


## Imports