# Callback Functions
A callback function is a function that is passed as an argument to another function. When the caller function is executed, the callback function can then be invoked to trigger a subsequent action. 

Common uses include:
- event listeners
- handling errors
- asynchronus events
- array methods
- accessing variables in a closure

## Loading a resource
It may take some time to load a sldkfjalskdfj;aslkfjlkjresource such as a script. If you need something from the script you are loading to be available for the next task, use a callback function that is called on the onload event:
```
function loadScript(src, callback){
    let script = document.createElement("script");
    script.src = src;
    script.onload = () => callback(script);
    document.head.append(script);

}

loadScript("https://srcurlhere.com/path", script => {alert("Script was loaded"); //can use functions from the script here});
```

## Nested Callbacks (callback hell)
Suppose you wanted to load multiple scripts in order. You would have to call loadScript inside of the callback function, so that it only gets started after the onload event finishes. The inner, second loadScript would then take its own callback function, which would be executed when the second script is loaded.  This chain of nested callbacks leads to "callback hell"

```
loadScript(script1.js, () => {alert("Script 1 loaded");
    loadScript(script2.js, () => alert("Script 2 loaded"))
});
```
