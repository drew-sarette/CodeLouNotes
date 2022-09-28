# loops
## for
the best loop. Executes the block of code a predetermined number of times.
```
for (let i = 0; i < 10; i++) {
 //statements
}
```
use let to prevent i from becoming a global variable. **DO NOT OMIT LET!!**

## while
```
while (condition) {
	statements//
}
```
The condition is checked before statements are executed.

## for ... in
loops over the keys in an object or the indexes in an array

```
const platypus = {
	name: "perry",
	hat: "fedora",
	type: "mammal",
	limbs: 5
}

for (let key in platypus) {
	console.log(key, platypus[key]);
}

//name perry
//hat fedora
//type mammal
//limbs 5
```

## for ... of
loops over the values in an iterable object. Less used than for...in

```
let inventory = ["knife","rabbit's foot", "piece of string", "lint"];

for (let prop of inventory) {
	console.log(prop);
}

//"knife"
//"rabbit's foot"
//"piece of string"
//"lint"
```
## do ... while
```
do {
	//statement
} while (condition)
```
The statements are executed at least once before the condition is checked.

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

# Switch Statements
More efficient and readable than complicated if-else structures.

    let x = "bippity"
    switch (expression) {
	    case 0: 
		    //statements
		    break;
		 case 1: {
			  let x = "boppity"
			  //statements
			  break;
			  }
		 case 2:
			case 3:
				//statements
				break;
			default: 
				//statements
    }
For a case to run, the expression must match exactly.  If example is 4, case "four" or "4" will not happen. Cases 2 and 3 trigger the same statements.  By itself, a case does not create a block scope. To do that, use {}. If no case expression = true, the default will run.

# Break and Continue
Break terminates the innermost enclosing loop, and continue terminates the current iteration of the loop an starts the next one.
Break and continue can be used with labels to specify which loop to break or continue


For example here, "continue checkj" continues the checkj while loop:
```
let i = 0;
let j = 10;
checkiandj: while (i < 4) {
  console.log(i);
  i += 1;
  checkj: while (j > 4) {
    console.log(j);
    j -= 1;
    if ((j % 2) === 0) {
      continue checkj;
    }
    console.log(j, ' is odd.');
  }
  console.log('i = ', i);
  console.log('j = ', j);
}
```

# Destructuring
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