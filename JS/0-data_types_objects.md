
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


## Objects

>Object refers to a data structure containing data and instructions for working with the data. Objects sometimes refer to real-world things, for example a car or map object in a racing game.

```javascript
var myCar = new Object();
myCar.make = "Ford";
myCar.model = "Mustang";
myCar.year = 1969;
```

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
