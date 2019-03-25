# Custom Elements Style Guide

Even though custom elements is a part of the W3C HTML Standard, the way we name we name and create custom elements is of importance. Standard HTML elements are namned using one word only. A Custom Element name on the other hand side, always needs to have 2 building blocks, separated by a dash. So, example of standard elements are `<h1>`, `<input>`, `<div>` while custom elements can look in many different ways; `<polymer-header>`, `<x-input>` or `<custom-header>`. 

When the custom elements library grows and are handling more and more of your HTML code, any prefix chosen will become quite dominant in the code base. If using a lot of <polmer-xxx> elements, your code base will look quite much POLYMER!!!
  
Build your custom elements so they are as close to the HTML standard as possbible. Just add a c- prefix in front of the element name, and we'll understand that this is a `<c(ustom)-element>`. Some of the most used components you can use are `<c-header>`, `<c-main-navigation>` and `<c-footer>`. These are custom made elements, availble to be used in any of your application, regardless of framework or platform in use.

## The c- prefix

In order to make custom elements as portable as possible, we do like to make them as generall as we can. A HTML standard header is namned `<header>` and when we decided to make a custom header, it's simply namned `<c-header>`. In the same manor, when we like to extend the functionality or the `<input>` element, we'd call that the `<c-input>` elements.

## Attributes
