The window object provides some built in objects to work with APIs;
    - XMLHttpRequest
    - fetch
    - Axios
    - jQuery

## XMLHttpRequest
```
const request = new XMLHttpRequest();
request.open("GET", "https://jsonplaceholder.typicode.com/users");
request.send();
request.onload = ()=>{
    if (request.status === 200) {
        console.log(JSON.parse(request.response));
} else {
    console.log(`error ${request.status}`);
}
```
XMLHttpRequest was deprecated in ES6.  A new request object is created, then the open, send and onload methods are used. The response is a string, which can be parsed to JSON. 

## fetch API
fetch is a property of the window object. It returns a promise, which 
```
fetch("https://jsonplaceholder.typicode.com/users")
.then(response=>{
    return response.json();
}).then(json=>{
    console.log(json);
})
```