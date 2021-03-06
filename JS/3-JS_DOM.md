
The dom and JS
===

#Document Object Model (DOM)

The DOM is how JavaScript code can interact with elements on a HTML web page.As specified by the DOM API, each HTML element is represented by an object, hence the term “Object Model”. Each object has various properties and methods that corresponds to the appearence or behavior of the corresponding HTML element. The object also has parents, children and siblings as specified by the DOM tree.

Each node has a type, corresponding to what kind of HTML element it represents. Each node has different properties and methods available, depending on its type. There is a type hierarchy for DOM nodes, as shown below. The base type of all dom nodes is Node, which contains methods for traversing the tree. All HTML elements would have the type Element and HTMLElement, but an image would have type HTML and so on.

# The Document Object

The document object represents the HTML document itself. It is at the root of the DOM tree that we previously discussed. It also provides us with a number of methods for searching for other nodes in the document.

####Traversing the DOM Tree

Once you have an element, there are a number of elements that let you get elements from elsewhere in the tree.

element.parentNode
Returns the parent node of the given element.

element.childNodes
Returns a collection of child nodes of the given element.

element.firstChild
Returns the node’s first child in the tree, or null if the node is 
childless.

element.lastChild
Returns the node’s last child in the tree, or null if the node is childless.

element.nextSibling
Returns the node immediately following the specified one in its parent’s childNodes list, or null if the specified node is the last node in that list.

element.previousSibling
Returns the node immediately preceding the specified one in its parent’s childNodes list, null if the specified node is the first in that list.


#### Select Elements

Get the first matching DOM element by selector
```
var h1Element = document.querySelector("h1")
var myId = document.querySelector("#myId")
```

Get all matching DOM elements by selector
```
var primaryButtons = document.querySelectorAll(".btn-primary")
```

--------------------------------------------------------

Get DOM element by id
```
var el = document.getElementById("myId");
```

Get DOM elements by class
```
var arr = document.getElementsByClassName("myclass");
```

Get DOM elements by HTML tag
```
var el = document.getElementsByTagName("h1");
```

#Event-based Programming

The programs discussed so far are sequential. When they are loaded, they perform a series of instructions. This is analogous to having a main function in C++ or Java: when the program is run, the main function is run until it is completed, then the program quits.

However, JavaScript is often used for programming client-side interfaces. We want a client-side interface to perform actions in response to user actions. Enter event-based programming.

Event-based programming (also known as event-driven programming) is a programming paradigm in which we write programs that respond to events. An event can be anything interesting that happens to the program. For instance, a page load, keyboard button press, or mouse click can all be events. When these events occur, the program will run a given function. This function is known as a the event listener or event handler.


#### Add Dynamic Changes to Events with Functions
The best way to register an event listener is to use the addEventListener method. The receiver of the method is the target of the event. The first parameter should be the name of the event, and the second parameter should be callback function that is fired upon receiving the event. The third event specifies whether the listener has a property called “capture”, which causes the listener to fire before the normal event bubbling chain. (In theory, the third parameter should be optional and default to false. In practice, many browsers consider a missing third parameter to be an error, so you should always include it and set it to false.)

```javascript
var helloWorldFn = function() { console.log("hello world!")};

document.getElementById("hello_world_btn").addEventListener("click", helloWorldFn, false)
```

In this example, the element with the ID “hello_world_btn” is the event target. The name of hte event is “click”. helloWorldFn is the event listener.

```
el.addEventListener("click", function() {
  alert("you clicked a button");
});

// Other Event Listeners
// "mouseenter"
// "mouseleave"
// "submit"
```

Change or add a style attribute value
```JS
var arr = document.getElementsByClassName('text-good');
// console.log(arr)

for(i = 0; i < arr.length; i++) {
    console.log(i)
    console.log(arr[i]);
    arr[i].style.color = "green"
    // arr[i].style.display= "none" // hide the element
}
```

Change text
```
el.innerText = "New Text!"
```

Add class
```
el.classList.add("danger")
```

Prevent Default Behavior
```
var button = document.querySelector("a#san-francisco_cta");
button.onclick = function(event){
    event.preventDefault(); // SUPER IMPORTANT PART
    alert("Hahah! Now you get me instead")
};
```

### Docs & Resources

* [Document Object Model docs (Mozilla)](https://developer.mozilla.org/en-US/docs/Web/API/document)
* [Document Object Model docs (W3Schools)](http://www.w3schools.com/jsref/dom_obj_document.asp)
* [List of DOM Events](https://developer.mozilla.org/en-US/docs/Web/Events)

#### Further Reading

  * [Getting started with selectors [MDN]](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_started/Selectors)
  * [Selectors with multiple classes and ids [CSS Tricks]](https://css-tricks.com/multiple-class-id-selectors/)