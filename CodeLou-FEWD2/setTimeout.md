# setTimeout()
setTimeout() is not part of the ES6 specification, but is available in all browsers and Node.js. It takes at least two arguments,
1. The function to be called after the time is up, and
2. The time interval to wait, in ms
3. All arguments to pass to the function in order.

for example: 
```
setTimeout(confirm, 2000, "Did you get a chance to read that memo?")

```
Note that the function confirm is mentioned, not invoked. Hence it is sans (). With (), it will be called immediately and without any arguments. Similarly, if you try to give it () and arguments, it will be called immediately with those args.


# Timer Identifier and clearTimeout()
The setTimeout function actually returns a "timer identifier" that can be used to cancel the timer. In a browser, that identifier could be a simple number, or a variety of other objects. In Node, it is an object with some additional methods. See the [HTML Living Standard](https://html.spec.whatwg.org/multipage/timers-and-user-prompts.html#timers) for more details.

The clearTimeout function can be called to cancel the setTimeout callback:
```
const timerId = setTimeout(confirm, 2000, "read that memo yet?"); //timer is started, id saved to timerId

clearTimeout(timerId); //timer cancelled
console.log(timerId); //id is still there 
```
Note: it is best to clearTimeout every single setTimeout, since setTimeout saves the function *and* its lexical environment until clearTimeout is called. 

# Nested setTimeout
setTimeout can be nested to create a repeating timed event:
```
function printNumbers(from, to) {
  setTimeout(function nextNumber(){
    if (from <= to){
      console.log(from);
      from++;
      setTimeout(nextNumber, 1000);
    }
  }, 1000)
}
printNumbers(1, 5);
```