# Debugging Locators

Locators can and should be recorded using a recorder. While they may not be perfect, at least the recorder generates a working locator. Yes, if the locators change, they will stop working, but at the time of recording, the locator is guaranteed to be correct.

If the recorded locator is of the name or id type, there is no need to debug or optimize it. However, more attention should be paid to CSS and XPath locators.

## Basic Principles of CSS and XPath

<body><form><input type="text" name="test"></form></body>

XPath: //input[@name="test"]
CSS: input[name="test"]

If you need to locate an element, you can specify its tag name (i.e., the name of the element) and the value of one or more of its attributes. For instance, if you need to locate a text field <input> that resides within a form on a page, you can write //input (XPath). However, since there may be many <input> fields on the page, you should add additional conditions to identify this specific element among others. These additional conditions are enclosed in square brackets.

## Finding Nested Elements

If the element you need to locate does not have any suitable attributes to uniquely identify it, but it resides within a parent element (e.g., a form) that has distinguishable attributes, you can find it in two steps:

Locate the parent element, which is easier to identify.
Search for the nested element within it. This process involves a series of sequential steps.

<body><form><input name="test"><input type="text"></form></body>

XPath: //form[@name="test"]//input
CSS: input[name="test"] input

If you want to search directly within a specific parent element and not at arbitrary depths, you should use a single slash (/) in XPath or the > symbol in CSS:

XPath: //form[@name="test"]/input
CSS: input[name="test"] > input
Special Features of CSS
CSS is specifically optimized for web applications, and it provides shorthand notations for certain scenarios.

##  Identifiers
If an element has an ID and you need to search for it by that ID, CSS offers a shorthand notation:

<body><form id="test"><input type="text"></form></body>
CSS: form#test input

## Classes
If an element has a class and you need to search for it by that class, CSS also offers a shorthand notation. Classes are commonly used alongside IDs to style elements.

<body><form class="test"><input type="text"></form></body>
CSS: form.test input
What CSS Cannot Do
| Searching by Element Text
If you need to locate a link with specific text, this can be done using XPath:

XPath: //a[.="Link Text"]
| Parent Element
To find a form, you can first locate an <input> field inside it and then move one level up in the hierarchy:

XPath: //input[@id="test2"]/..
| Subqueries
Instead of traversing up the tree, you can write a query with an additional condition: "Find a form that contains an input with the ID test2":

XPath: //form[./input[@id="test2"]]
