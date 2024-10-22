# Arrays
Arrays are a special type of object where the keys are all numbers.  They are used to store multiple bits of similar information under one variable name, and provide convenient methods to manipulate their contents.
- JS arrays can contain different types
- Arrays can be resized at any time
- contents must be accessed using brackets and a non-negative integer.
- 

## Create an array
```
const arr = [1, "item2", False];
console.log(arr[1]) //=> "item2";

const grains = New Array("barley", "rye", "spelt", "wheat");
console.log(grains[0]); //=> "barley"

const letters = Array.from("Supercalifragilisticexpialidocious");
console.log(letters[5]); //=> "c"
```

## Modify an Array
- arr.push(newElement) adds newElement to the next available index
- arr.pop() returns the element at the last index, and leaves the array without that.
- arr.unshift() is like push but adds an item at index 0 and "shifts" all the other elements over
- arr.shift() is like pop but it gets arr[0]
- arr.splice(startIndex, deleteCount, itemToAdd, ...) modifies the contents of an array at the startIndex by deleting items or adding items. Any deleted elements are returned in an array.
- arr.slice(startIndex, stopIndex) returns the items starting at startIndex, and stopping before stopIndex as a new array. It does not change arr

# Analyze an Array
