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

