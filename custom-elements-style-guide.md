# Custom Elements Style Guide

Even though custom elements is a part of the W3C HTML Standard, the way we name we name and create custom elements is of importance. Standard HTML elements are namned using one word only. A Custom Element name on the other hand side, always needs to have 2 building blocks, separated by a dash. So, example of standard elements are `<h1>`, `<input>`, `<div>` while custom elements can look in many different ways; `<polymer-header>`, `<x-input>` or `<custom-header>`. 

When the custom elements library grows and are handling more and more of your HTML code, any prefix chosen will become quite dominant in the code base. If using a lot of `<polymer-xxx>` elements, `<polymer->` will be all over the code. Therefore we want to use a short and discreet prefix.
  
Build your custom elements so they are as close to the HTML standard as possbible. Just add a c- prefix in front of the element name, and we'll understand that this is a `<c(ustom)-element>`. Some of the most common components that you can use are `<c-header>`, `<c-main-navigation>` and `<c-footer>`. These are custom made elements, available to be used in any of your application, regardless of framework or platform in use.

## The c- prefix

In order to make custom elements as portable as possible, we do like to make them as generall as we can. A standard HTML header is namned `<header>` and when we decided to make a custom header, it's simply namned `<c-header>`. In the same manor, when we like to extend the functionality of the `<input>` element, we'd call that the `<c-input>` elements.

## Variations and Attributes

Naturally, we do need some variations of a custom element. In standard HTML, that issue is solved by using in various ways, sometimes a few different elements are created as has been done with `<ol>` and `<ul>` elements. This could technically has been solved with adding a attribute to a `<list>` element. That would then have looked something linke `<list type="ordered">` and `<list type="unordered">` respectivly. In other instances, standard HTML do in fact use attributes to give you control over the appearance. The Input element is a great example of that as it can take a lot of different shapes; `<input type="text">`,  `<input type="checkbox">`, `<input type="radio">`, `<input type="password">` just to mention a few.



