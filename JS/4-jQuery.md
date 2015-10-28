
#Principles of jQuery

As the name suggests, jQuery is focused on queries. A query uses CSS selectors to get a set of elements in the document. We can then perform operations on all the selected elements at once.

Recall that we can call the $() method on a single element in order to get a selection of one object. We can also select a single element using document.getElementbyId.

```javascript
var jqElem = $("#egg");
var domElem = document.getElementById("egg");
```

Both jqElem and domElem refer to a single element, but they don’t work in the same way. This is because these two objects are different kinds of objects. domElem is a raw DOM element object, whereas jqElem is a jQuery object. You can see this by looking at the available methods: jqElem only has methods available to jQuery objects, and domElem only has methods available to DOM elements. A jQuery object behaves like a wrapper around the underlying DOM objects. It provides you with new methods, and it executes the methods by performing actions on the underlying DOM object.


##The $ variable

When you include the jQuery script, it exports a single object into the global namespace. The object is sensibly named jQuery. For convenience, jQuery also aliases the variable $ to the same object. Because the jQuery variable is so frequently used, the $ variable is more commonly used, as it is shorter and easier to type.

$ is a function object, which means that it can be called as a function, but it also has a number of properties (mostly methods) that can perform other useful things.

$ is a heavily overloaded function. It takes a single argument, and always returns a jQuery collection. Depending on the type of the argument, it can do four different things:

 -If the argument is a CSS selector, it returns a jQuery collection of   DOM elements that match the selector.

 -If the argument is a HTML string, it creates a new DOM element from the HTML string, and returns it as a jQuery collection.

 -If the argument is a DOM element, it returns the DOM element as a jQuery collection.

 -If the argument is absent, it returns an empty jQuery collection.

 -If the argument is a jQuery collection, it returns the jQuery collection unchanged. Therefore calling $ on the output of $ is a no-op.

##Selection

Earlier on, we showed that we could select elements in the DOM using functions such as document.getElementById(). jQuery makes this much simpler by giving us an easier selector syntax. Suppose we had a <div> element with its id attribute set to “hello”. The following example shows how to select it using the DOM and using jQuery.

```javascript
var domMan = document.getElementById("hello");
var jqMan = $("#hello");
```

Here, $ is a query function. We pass it a selector string that tells jQuery which elements we want to find.

Notice that we used the # symbol to indicate that the string is an id. This looks like a lot like CSS selectors. In fact, the $ function can take any CSS selector. For instance, if we wished to select all elements of class my_class, we would use the selector string “.my_class”. Here are other common selectors.

All Selector (”*”)
Selects all elements.

Class Selector (“.class”)
Selects all elements with the given class.

Element Selector (“element”)
Selects all elements with the given tag name.

ID Selector (“#id”)
Selects a single element with the given id attribute.

Multiple Selector (“selector1, selector2, selectorN”)
Selects the combined results of all the specified selectors.

Descendant Selector (“ancestor descendant”)
Selects all elements that are descendants of a given ancestor.

##Manipulating Elements

jQuery objects are somewhat different from raw DOM objects. jQuery are raw DOM objects wrapped with a layer that provides us with new methods to work with those objects. These methods are usually much easier to use than the native DOM methods.

The attr method allows us to get and set HTML attributes. When called with an attribute name, the attr method gets the current value of that attribute.

When called with an attribute name and a new value, the attr method sets that attribute to the given value. When called with a map of attribute names and new values, the attr method sets each attribute to the corresponding new value.

The css method allows us to get and set CSS styles. Its usage is identical to the usage of attr. When called with a CSS property name, the css method gets the current value of that CSS property. It does so by inspecting the style attribute on the element. Note that it is unable to obtain the style of the element as defined in the CSS stylesheet.

When called with a CSS property name and a new value, the css method sets that style to the given value. When called with a map of CSS properties and new values, the css method sets each CSS property to the corresponding new value. These properties are set by modifying the style attribute on the element. The CSS stylesheets will remain unchanged.

Often, we want to change many styles on an element at once. For instance, if we were building a custom toggle button, we might want to have a set of styles for selected buttons, and a different set of styles for an unselected button. Rather than using the css method to set up all of the styles, it is easier to define the styles as a class style in a CSS stylesheet, and then apply the appropriate classes to the elements.

The addClass and removeClass methods enable us to do this. Both methods take a single argument, which should be string of classes to be added or removed. Multiple classes should be separated by spaces.

We often want to control if elements on a page are visible or invisible. For instance, if we were building a tooltip help widget, we could create HTML elements corresponding to each . The easiest way to do this is to set the CSS property display to none when the element is to be hidden, and to the original value, either block or inline, when the element is to be displayed. This is such a common idiom that jQuery provides helper methods to do this.

The hide and show methods hide or show an element respectively. They work by modifying the display property inline CSS in the manner described above.

Finally, the val method allows us to get or set the values of form elements.
