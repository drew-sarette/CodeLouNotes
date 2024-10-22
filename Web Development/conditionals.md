# Switch Statements
More efficient and readable than complicated if-else structures.
```
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
            break;
		case 3:
			//statements
			break;
		default: 
			//statements
    }
```
For a case to run, the expression must match exactly.  If example is 4, case "four" or "4" will not happen. Cases 2 and 3 trigger the same statements.  By itself, a case does not create a block scope. To do that, use {}. If no case expression = true, the default will run.