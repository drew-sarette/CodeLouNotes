# Objects
Objects have properties and methods. Properties are key-value pairs that can contain primitives, or objects. Methods are functions that can act on that object. Objects make it easier to organize information and its logic, and move it around together.

# Creating Objects
## Object literal:
```
const me = {
    fname: "Drew",
    lname: "Sarette",
    age: 2002,
    fullName: fuction () {
        return this.fname + " " + this.lname;
    }
}
```
Note that ```this``` refers to the parent object.

## New Object()
Use the Object() constructor to create a new empty object then add properties later:
```
const person = new Object();
person.fname = "Nina";
// can keep adding properties
```
## Constructor functions
```
function Painting(artist, date, title) {
    this.painter = artist;
    this.date = date;
    this.title = title;
}

const painting1 = New Painting("Caravaggio", "unknown", "Judith Beheading Holofernes");
```
# Accessing/creating Properties
using dot notation:
```
obj.newProp = newValue;
```
using brackets:
```
obj[newProp] = newValue;
```
Brackets are useful for creating or reading a property that is a variable name. Also for properties that have non-standard names (starting with a number, including spaces, etc...)

## Destructuring
Another way of accessing object and array info.

```
const pikachu = {
	name: pikachu
	number: 025
	type: electric
	evolutions: [
		"pichu",
		"pikachu",
		"raichu"
	]

}

const [name, evolutions: versionsOfPikachu, ...rest];
console.log(name);
console.log(rest);
console log(versionsOfPikachu[1]);

// output:
// "pikachu"
// "number: 025, type: electric"
// "pikachu"
```
## for ... of
Iterates over the values of an object or array.
```
const human = {legs: 2, arms: 2, head: 1, torso: 1};

for (const bodyPart of human) {
	console.log(bodyPart);
}

// output
// "2"
// "2"
// "1"
// "1"
```

## for ... in

Avoid using for ... in, since you will rarely need to get all the keys of an object.  It is mostly used for debugging, where you might want to check if any particular key holds a particular value.

```
const human = {legs: 2, arms: 2, head: 1, torso: 1};

for (const bodyPart in human) {
	console.log(`bodyPart);
}

// output
// "legs" 
// "arms"
// "head"
// "torso"
```
Iterates over the keys of an object

## Optional Chaining
If you have a nested object, and you try to access a child of a parent who does not exist, you get an error. You can use the ```?.``` operator to only try to access nested objects if they exist. If they don't exist, undefined is returned.

```
const obj = {
  address: {
    street: 'Trincomalee Highway',
    city: 'Batticaloa',
  },
};

obj.address.zipCode;
// => undefined

obj.residence.street;
// => TypeError: Cannot read property 'street' of undefined

obj.residence?.street;
// => undefined
```
## Nullish Coalescing
Used to suppy a default value to variables only if they contain null or undefined. The nullish coalescing operator ```??``` returns the operand on the right if the left operand is null or undefined. Otherwise it returns the left-hand operand.
```
let x;
// x undefined
x = x ?? 0;
// x is 0