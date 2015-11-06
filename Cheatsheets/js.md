
#Input 


#### Grabbing input from the user in the browser

```
var color = prompt(“What is your favorite color?”)
```
Conditionals
==========

####if / else
```
if (condition) {
  //do something
} else if ( other_condition ) {
  //do something else
} else {
  //do something else
}
```

#### While loop
```
while ( condition ) {
  //do something
}
```

#### For loops

```js
// prints 0 through 9
for(var i=0; i<10; i++) {
  console.log(i);
}
```

Strings
======

#### String concatenation
```
var first = "Doogie";
var last = "Howser";
var full = first + " " + last;
```

#### charAt
```
var word = "heya";

//this will be the letter h
var letterh = word.charAt(0);

//this will be the letter y
var lettery = word.charAt(2);
```

#### Random

```
//number between 1 and 10
var random = Math.floor(Math.random()*10) + 1;
```


Arrays
=====

```js
//Make a new empty array
var a = [];

//Make a new array with 3 elements
var b = [5,20,1];

//Sets the first element of b to 5
b[0] = 5;

//Adds a new element to an array
b.push(20);

//merge the contents of two arrays
a.concat(b);
```

Functions
========

**Creating a function**

```
var myfunc = function(param1, param2) {
  //do something with param1 and param2
  return something; //optional
}
```

**Calling a function**

```
var a = //something;
var b = //something;
var return_value = myfunc(a, b);
```

#### Function Scope

```
var a = 5;
var sum = function(a,b) {
  // here a is a parameter
  return a+b;
};

console.log(3, 4); // 7

// outside the function, a is 5 again
console.log(a); // 5
```

```
var a = 5;
var multipleOfN = function(x, y) {
  // here we define a new variable using var
  var a = x * y;
  return a;
};

console.log(multipleOfN(3,7)); // 21

// Outside of the function, a is 5 again
console.log(a); // 5
```

```
var a = 5;
var multiplyA = function(n) {
  // Here we are not using var,
  // so we are changing the outside a variable

  a = a * n;
  return a;
};

console.log(multiplyA(3)); // 15
console.log(a); // 15
```
#### Timers

**Call a function 2 seconds from now**
```
var handle = setTimeout(myfunc, 2000);
//we can also remove that Timeout
clearTimeout(handle);
```

**Call a function every 2 seconds**
```
var handle = setInterval(myfunc, 2000);
//we can remove that Interval
clearInterval(handle);
```

Objects
======

**Creating objects**
```javascript
var obj = {};
var obj2 = { name: "doogie", age: 14};
```

**Accessing values**
```javascript
var obj = {name: "crawford"};
var name = obj["name"];
var also_name = obj.name
```

**Changing and creating values**
```javascript
var obj = {name: "amy"};
obj["name"] = "roger";
obj.name = "laura";
```

#### Looping through Objects
```javascript
var obj = {name: "amy", age: 99};
var keys = Object.keys(obj);
for(var i=0; i< keys.length; i++) {
  var key = keys[i];
  var value = obj[key];
  console.log(value);
}
```

#### this
```javascript
var f = function() {
  console.log(this.name)
}

var obj = {
  name: "sean",
  printName: f
}

var obj2 = {
  name: "david",
  heresMyName: f
}

//will print sean
obj.printName();

//will print david
obj2.heresMyName();
```

## constructors
```javascript
var F = function() {
  this.name = "sean"
}
var f = new F();
console.log("my name is " + f.name);
```

Selecting and modifying DOM elements
========================

#### selecting an element
```js
var css_selector = "li#mouse"
var element = document.querySelector(css_selector);
```

#### selecting multiple elements
```js
var css_selector = "li.mammal"
var elements = document.querySelectorAll(css_selector);
//elements can now be looped through using a for loop
```

#### grabbing the text of a textbox
```js
var textbox = document.querySelector("input#mytextbox");
var thetext = textbox.value;
```

#### grabbing whether a checkbox is checked
```js
var checkbox = document.querySelector("input#mycheckbox");
var ischecked = checkbox.checked;
//ischecked is now either true or false
```

#### changing an attribute of an element
```js
var element = document.querySelector("#someid");
var attribute = "width";
var newvalue = "100";
element.setAttribute(attribute, newvalue);
```

#EventListeners
```js
//select an element, such as a button
var element = document.querySelector("#someid");
var eventname = "click";
var someFunc = function() {
  //do something
}
element.addEventListener(eventname, someFunc);
```

## Keyup/Keydown

**Reference**
  - [Every keyboard keycode](ttp://www.cambiaresearch.com/articles/15/javascript-char-codes-key-codes)
  
The difference between `keyup` and `keydown` is when the
event is fired.
  - `keydown` will be fired the moment you press down
on a keyboard key.
  - `keyup` will be fired when you release the keyboard
key that you were pressing.

```js
var textInput = document.querySelector('#myinput');
//I am only adding this keylistener to a inputbox so that
//it only fires when a user presses a key AND the textbox
//is currently selected. This event will not fire if the
//textbox is not selected (i.e. they are not typing into it).
textInput.addEventListener("keyup", function(event) {
  //every letter and key on your keyboard has a keycode
  //associated with it. The enter key happens to have
  //the code 13.

  var keycode = event.keyCode;
  if (keycode === 13) {
    alert("you just pressed the enter key!");
  }
});
```


## Radio buttons and dragging

#### radio buttons
Make sure that they all have the same ```name```
```html
<input type="radio" name="hamster">First
<input type="radio" name="hamster">Second
<input type="radio" name="hamster">Third
```

#### dragging

In your html:
```html
<li draggable="true" id="justsomeid">
```

# DOM manipulation

#### createElement
```js
document.createElement("elementType")
```

#### insertBefore
```js
parentElement.insertBefore(newElement, referenceElement)
```

#### appendChild
```js
parentElement.appendChild(elementToAppend)
```

#### removeChild
```js
parentElement.removeChild(elementToRemove)
```

In your yavascript, listen for the `dragstart` event. Also, set the `draggable` attribute on your list item element to `"true"`

## forEach
```js
var array = [1,2,3];
array.forEach(function(elem) {
  // do something for each element
});
```


Node
====

## Reading in Input
```js
var cb = function(data) {
  var strData = data.toString().trim();
  console.log("you typed " + strData);
}
process.stdin.on("data", cb);
```

## Exiting your node program
```js
process.exit();
```

## npm

#### global install


*you can run it no matter what directory you're in*
```
npm install -g [package-name]
```

#### local install

*this is for node/javascript code and not executables*
```
npm install [package-name]
```
#### package.json

*this will create a bare bones package.json for your node "app" or package*
```
npm init
```

#### installing dependencies to your package.json
*do this to install any third-party package that your code depends on*
```
npm install --save [package-name]
```

#### gitignore

just add this to a .gitignore file in the directory of any node app
```
node_modules
.DS_Store
```

## wscat

listening on port 3000:
```
wscat -l 3000
```

connecting to a remote server at port 3000
```
wscat -c ws://seanwest.princesspeach.nyc:3000
```

## Websockets server
```js
var WebSocketServer = require("ws").Server;
var server = new WebSocketServer({port: 3000});
server.on("connection", function(ws) {
  console.log("Client connected!");
});
```

