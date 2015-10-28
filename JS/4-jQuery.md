
#Principles of jQuery

As the name suggests, jQuery is focused on queries. A query uses CSS selectors to get a set of elements in the document. We can then perform operations on all the selected elements at once.


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


