
#Principles of jQuery

As the name suggests, jQuery is focused on queries. A query uses CSS selectors to get a set of elements in the document. We can then perform operations on all the selected elements at once.


##The $ variable

When you include the jQuery script, it exports a single object into the global namespace. The object is sensibly named jQuery. For convenience, jQuery also aliases the variable $ to the same object. Because the jQuery variable is so frequently used, the $ variable is more commonly used, as it is shorter and easier to type.

$ is a function object, which means that it can be called as a function, but it also has a number of properties (mostly methods) that can perform other useful things.

$ is a heavily overloaded function. It takes a single argument, and always returns a jQuery collection. Depending on the type of the argument, it can do four different things:

*If the argument is a CSS selector, it returns a jQuery collection of *DOM elements that match the selector.
*If the argument is a HTML string, it creates a new DOM element from the HTML string, and returns it as a jQuery jQuery collection.
*If the argument is a DOM element, it returns the DOM element as a jQuery collection.
*If the argument is absent, it returns an empty jQuery collection.
*If the argument is a jQuery collection, it returns the jQuery collection unchanged. Therefore calling $ on the output of $ is a no-op.


