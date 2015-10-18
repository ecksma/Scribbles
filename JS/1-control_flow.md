

Control Flow in Js
========================
#### Basic Boolean Operators

| English | "and" | "or" | "not" or "bang" | "double bang" |
| ------------- |:-------------|:-------------|:-------------| :------- |
| Javascript | `&&` | &#124;&#124; | `!` | `!!` | |  
| e.g. | `a && b` | a  &#124;&#124; b | `!b` | `!!b` |
| English | A and B | A or B | not B | not NOT B |

#### Boolean Comparison Operators

| strict equality | loose equality | not strictly equal | not loosely equal | greater than | less than | greater than or equal to | less than or equal to |
| ------------- |:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|
| `===` | `==` | `!==` | `!=` | `>` | `<` | `>=` | `<=` |

#### `if/else`

```
if (badWeather) {
  takeTheBus();
}

if (!badWeather) {
  walkToWork();
}
```

```
if (badWeather) {
  takeTheBus();
} else {
  walkToWork();
}
```

#### `else if`

```
if ( hasCar ) {
	// drive it!
} else if ( hasBike ) {
	// ride it!
} else if ( hasTransitPass ) {
	// take the bus!
} else {
	// better start walking!
}
```

#### `switch`

```
switch (row){	
	case 1: 	
		price = 0.25;
	case 2: 
		price = 0.50;
	case 3:
		price = 0.75;
	case 4: 
		price = 1.00;
	default:  // the rest of the products (rows 5-7) 
		price = 1.25
}	
// ^ vending machine with prices organized by row!		
```

#### `while/for` loops

```
var m = ["Bill", "Nicki", "Kelly"]
for (i = 0; i < m.length; i++) {
  console.log(m[i] + " is a nice person")
}

```

```
while (timeBeforeWork > 180000) { // Remember JS counts time in milliseconds
  hitSnooze()
}
```
