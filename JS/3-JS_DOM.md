
The dom and JS
===

#Document Object Model (DOM)

The DOM is how JavaScript code can interact with elements on a HTML web page.As specified by the DOM API, each HTML element is represented by an object, hence the term “Object Model”. Each object has various properties and methods that corresponds to the appearence or behavior of the corresponding HTML element. The object also has parents, children and siblings as specified by the DOM tree.

Each node has a type, corresponding to what kind of HTML element it represents. Each node has different properties and methods available, depending on its type. There is a type hierarchy for DOM nodes, as shown below. The base type of all dom nodes is Node, which contains methods for traversing the tree. All HTML elements would have the type Element and HTMLElement, but an image would have type HTML and so on.


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

#### Add Dynamic Changes to Events with Functions
Add a function
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