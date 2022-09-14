# loops
## for
the best loop. Executes the block of code a predetermined number of times.
```
for (let i = 0; i < 10; i++) {
 //statements
}
```
use let to prevent I from becoming a global variable. **DO NOT OMIT LET!!**

## while
```
while (condition) {
	statements//
}
```

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
do {
	//statement
} while (condition)

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

