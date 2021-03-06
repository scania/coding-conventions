# Custom Elements Style Guide

Even though Custom Elements is a part of the W3C HTML Standard, the way we name and create custom elements is of importance. Standard HTML elements are namned using one word only. A Custom Element on the other hand side, always needs to have 2 building blocks, separated by a dash. Example of standard elements are `<h1>`, `<input>` and `<section>` while custom elements can look in many different ways; `<polymer-header>`, `<x-input>` or for example `<custom-header>`. A Custom Element is extremly customizable, why a standard is of high importance.

When a Custom Elements library grows and includes more and more of your HTML code, any prefix chosen will become quite dominant in the code base. Assuming that you're using lot of `<polymer-custom-elements>` the prefix `<polymer->` will be all over the code. Therefore we want to use a short and discreet prefix, making the code easier to read.
  
Build your Custom Elements as close to the HTML standard as possbible. Just add a c- prefix in front of the element name, and we'll understand that this is a `<c(ustom)-element>`. Some of the most common components that you can use are `<c-header>`, `<c-navigation>` and `<c-footer>`. These are tailor made elements, available to be used in any of your application, regardless of project, framework or platform in use.

## The c- prefix

In order to make custom elements as portable as possible, we do like to make them as general as we can. A standard HTML header is namned `<header>` and when we decided to make a custom header, it's simply namned `<c-header>`. In the same manor, when we like to extend the functionality of the `<input>` element, we'd call that the `<c-input>` element.

## Brand or project based prefixes

It could be tempting to use a custom element prefix that ties the element to your project, application or company. One might not know it at the moment of development, but chances are that another group within the company, or within a sibling company, can reuse much of your work. Having used a common prefix and code standard, that will then save a lot of migration tasks and will also simplify a future, shared, maintainance.

## Variations and Attributes

Naturally, we do need some variations of a Custom Element. In standard HTML, that issue is solved  in various ways, sometimes a few different elements has been created as done with the `<ol>` and `<ul>` elements. This could technically has been solved with adding a attribute to a (currently non-existing) `<list>` element. Such an emelement then would have looked something like `<list type="ordered">` and `<list type="unordered">` respectivly. 

In other instances, standard HTML do in fact use attributes to give you control over the appearance. The Input element is an example of that, as it can take a lot of different shapes; `<input type="text">`,  `<input type="checkbox">`, `<input type="radio">` or `<input type="password">` just to mention a few.

For a Custom Element we have the same options and we can use attributes for theming:  `<c-theme name="scania">` or `<c-theme name="volkswagen">` or `<c-theme name="what-ever">`. Some times it might be a good idea to break down a complex component and make a few stand alone elements out of it; `<c-main-navigation>`, `<c-side-navigation>`, `<c-table-of-contents>` or even a  `<c-parallax-navigation>` are all examples of different kind of navigations. Hosted in one huge element might not be a good idea, but probably they would all use common code from a more general `<c-navigation>` element.

## Conclusion

While standards within other areas are available for re-use, there are no standards for Custom Elements. In the meantime, these elements can work as a great way to package and share code between teams and entities. Therefore we recomend you to spend some extra time re-searching the naming of a Custom Element before creating it, as well of what attributes are available from the HTML standard and what kind of attributes that're used by other components.





