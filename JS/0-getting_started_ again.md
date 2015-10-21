
Data Types and Objects in Js
========================

## Data Types
	  * Boolean
	  * Null (nonexistent object)
	  * Undefined (empty variable)
	  * Number (integer and floating point)
	  * String (words in quotes)
	  * Symbol (only in ES6)

```javascript
var foo = 42;    // foo is now a Number
var foo = "bar"; // foo is now a String
var foo = true;  // foo is now a Boolean
```

#Object Oriented Programming

##Objectives

| Objectives: students will be able to . . . |
| :--- |
|  |
| summarize key features of the Object Oriented Programming paradigm |
| model real-world data and relationships with JavaScript objects |
| justify choices of which methods and attributes to include, and whether to put them on a constructor, a prototype, or a single object |

<!--| use localStorage to store persistent data in a JSON format |-->

##Programming Paradigms

<!--
![XKCD goto](https://imgs.xkcd.com/comics/goto.png)    
*Dev culture reference: 'goto considered harmful.' Google it LATER.*
-->

We've been working with **procedural programming**, putting blocks of code in functions (aka procedures) that we call at various points in the code. 

```
data <--> global or local variables

behaviors <--> procedures  (functions)

```


With **object oriented programming**, we organize data and behaviors in objects.  

```
data <--> attributes  ("class" or "instance" variables)

behaviors <--> methods (functions)

```

##OOP features

###Classes and Instances

JavaScript doesn't have classes (yet). We can instead think of "object types" or "kinds of objects" that are defined by the combination of (1) a constructor function (like `Array()`) and (2) the constructor function's prototype (`Array.prototype`).

Objects created with the `new` keyword are cloned "instances" of the "object type" of the constructor.

###Composition

Object types are built up or composed of other data types, including objects. 

###Delegation

Basically, "delegating" tasks to another part of the program. In JS, think of **prototype chain** lookup.

###Inheritance 

Basically, letting objects be "a kind of" other objects. The process by which, for example, we can easily create both `Employee` and `Student` object types starting from the features of a base `Person` object type. Tomorrow!


###Encapsulation

Encapsulation is an *overloaded* term - it can mean a few different things.  In the context of OOP, it most often refers to keeping attributes or methods "private," instead of "public" and exposed. JS doesn't have actual private object variables but can simulate them by using a scoping setup known as a **closure**.

Private variables always need *getter* and *setter* methods if they're going to be accessible from outside their scope.

```
function Person (name, realAge, feelsOld){
  this.name = name; 
  this.feelsOld = feelsOld;

  var _realAge = realAge;  // this variable will be "private", not accessible
  // can also make "private" function variables if your design calls for it

  this.getAge = function(){
    if (this.feelsOld){
     return _realAge - 10
    } else {
     return _realAge;
    }
  }
}

var grandpa = new Person("Jim", 72, true);

console.log("real age: ", grandpa._realAge);  // undefined

console.log("'age': ",grandpa.getAge());  // 62 :D
```

##Constructor and Prototype Review

**Constructors**

* variables and functions are declared once for each instance
* functions have access to "private" variables declared within the constructor's scope
* when you update the constructor, previously created instances DON'T update
* data is "embedded" in each instance

**Prototypes**
 
* all instances share the same function and variable declarations
* when you update the prototype, previously created instances DO get the updates
* data is "referenced" from the prototype copy

**Instance variables and functions**

* adds variable or function directly to the instance
* overwrites constructor properties/methods by replacing them
* overwrites prototype properties/methods by being earlier on the lookup chain!

##Modeling with Constructors, Prototypes, Instances

| Place | How it Works | Attribute Example | Method Example |
| :-- | :--- | :--- | :--- |
| constructor | common, each instance gets a copy at creation | usually passed in (name), sometimes calculated | rare, can access "private" variables |
| prototype | all instances share a lookup copy | commonalities (numLegs on Dog), or shared data (numCreated) | common, same behavior across instances |
| instance | only one copy, for this instance | singularities (secretCode with a sibling) or overwriting (3-legged dog)| rare, singularities (interpretSecretCode) |

Remember, when possibly overwriting an existing prototype property or method (especially on built-in objects' prototypes), always use `||`:

`Array.prototype.sort = Array.prototype.sort || mySort;`


## Objects

>Object refers to a data structure containing data and instructions for working with the data. Objects sometimes refer to real-world things, for example a car or map object in a racing game.

Object literal notation

```javascript
var myCar = {
  make: 'Ford',
  model: 'Mustang'
  year: '1969'
}
```
You can use the bracket notation with `for...in` to iterate over all the enumerable properties of an object. To illustrate how this works, the following function displays the properties of the object when you pass the object and the object's name as arguments to the function:

```javascript
function showProps(obj, objName) {
  var result = "";
  for (var i in obj) {
    if (obj.hasOwnProperty(i)) {
        result += objName + "." + i + " = " + obj[i] + "\n";
    }
  }
  return result;
}
```

So, the function call showProps(myCar, "myCar") would return the following:

```javascript
myCar.make = Ford
myCar.model = Mustang
myCar.year = 1969
```
**Further Reading**

1 [JavaScript data types and data structures [MDN]](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)

 2 [Different ways to define an object [SO]](http://stackoverflow.com/questions/1143498/difference-between-an-object-and-a-hash)
 
 3 [Working with strings](http://learnjsdata.com/strings.html)
  ([`split`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split) )

4 [Working with objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)




#Exercise

Modeling Cars for a Dealership

For each challenge that asks you to add a variable to the Car object type, write a comment that explains why you chose to put it on the constructor, prototype, or individual car instance.

1. List important attributes and methods for a Car object type.

1. Create a constructor for the Car object type.

1. Create a "public" (normal) `location` attribute for the Car object type.  Should this be on the constructor or the prototype?

1. Create a `drive` method for the Car object that takes in a new location and changes the car's location to that place. Should this be on the constructor or the prototype?

1. Create a `numWheels` variable that says how many wheels cars should have. Should this be on the constructor or the prototype?

1. Almost all of your cars are black. Create a `color` variable that stores the color of a car.  Should this be on the constructor or the prototype?

1. Create an instance of a car, and change its `color`.

1. Create a "private" `_priceMarkup` variable for the Car object type that stores the markup above a car's actual price (don't want customers to see this!). For example, `_priceMarkup = 0.5` would mean the final price of the car is 1.5 times its actual price. Should this be on the constructor or the prototype?

1. Create a getter method and a setter for the `_priceMarkup` variable.  Should these methods be on the constructor or the prototype?

1. Create a `getFinalPrice` method that returns the calculated cost of the car (based on the `price` and `_priceMarkup`). Should this be on the constructor or the prototype?

1. Create an `carCount` variable that counts how many cars the dealership has entered into inventory.  Should this be on the constructor or the prototype?

1. Stretch: Use `carCount` to assign an `inventoryID` to each car when it's created. A car's `inventoryID` should be unique to that car. Should this be on the constructor or the prototype? 


##Solution

```javascript
//OOP Modeling Challenges (Car Dealership)

// constructor for the Car object type.
var Car = function(make, model, year, location, actualPrice, priceMarkup){
	this.make = make;
	this.model = model;
	this.year = year;

	// location attribute is on Car constructor because 
	// we DON'T want all cars to share a location - 
	// they're probably in different places!
	this.location = location;

	// color could go either way, but we'll put it in constructor
	// because color is more tied to each car (constructor)
	// than to being a car or car-ness (prototype)
	this.color = "black";

	// 'private' variables HAVE to be in the constructor...
	var _priceMarkup = priceMarkup;
	var _actualPrice = actualPrice;
	// ...and so do the getters and setters for them
	this.getPriceMarkup = function(){
		return _priceMarkup;
	}
	this.setPriceMarkup = function(newMarkup){
		_priceMarkup = newMarkup;
	}

	this.getFinalPrice = function(){
		return _actualPrice + _actualPrice*_priceMarkup;
	}

	// COUNT OPTION 1
	// the carCount CAN'T be stored in the constructor,
	// because it needs to change every time a new car is created
	// but we need to update it in the constructor in order to keep track
	Car.prototype.carCount = Car.prototype.carCount + 1;

	// COUNT OPTION 2 (PREFERRED)
	// we could also add a carCount property directly to the Car constructor
	// since it's just a function, and JS functions are all just objects
	// this is a more common way to track all cars than than option 1
	Car.carCount = (Car.carCount || 0) + 1;


	// each car needs its own inventory id, and they'll all be different,
	// so inventoryID belongs in the constructor.
	// the expression below looks up the current carCount (some number)
	// and stores it as the new car's inventory id.
	this.inventoryID = Car.prototype.carCount;   // OPTION 1
	// or 
	this.inventoryID = Car.carCount; // OPTION 2 (PREFERRED)
}

// COUNT OPTION 1
// Again, the carCount CAN'T be stored in the constructor
Car.prototype.carCount = 0;

// the drive behavior is the same for all cars, 
// and it doesn't access 'private' attributes,
// so we keep code DRY by adding to prototype
Car.prototype.drive = function(newLocation){
	this.location = newLocation;
}

// numWheels could go either way
// but almost all cars have 4 wheels, 
// so we'll look it up from the prototype
Car.prototype.numWheels = 4;


// creating an instance
blueCar = new Car("Ford", "Focus", 2005, "Lot A", 6000, 0.25);

// changing its color
blueCar.color = "blue";
```