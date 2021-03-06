### Table of Contents

-   [Todo](#todo)
-   [Controller](#controller)
    -   [setView](#setview)
    -   [showAll](#showall)
    -   [showActive](#showactive)
    -   [showCompleted](#showcompleted)
    -   [addItem](#additem)
    -   [removeItem](#removeitem)
    -   [removeCompletedItems](#removecompleteditems)
    -   [toggleComplete](#togglecomplete)
    -   [toggleAll](#toggleall)
    -   [\_updateCount](#_updatecount)
    -   [\_filter](#_filter)
    -   [\_updateFilterState](#_updatefilterstate)
-   [Model](#model)
    -   [create](#create)
    -   [read](#read)
    -   [update](#update)
    -   [remove](#remove)
    -   [removeAll](#removeall)
    -   [getCount](#getcount)
-   [Store](#store)
    -   [find](#find)
    -   [findAll](#findall)
    -   [save](#save)
    -   [remove](#remove-1)
    -   [drop](#drop)
-   [Template](#template)
    -   [show](#show)
    -   [itemCounter](#itemcounter)
    -   [clearCompletedButton](#clearcompletedbutton)
-   [View](#view)

## Todo

Sets up a brand new Todo list.

**Parameters**

-   `name` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** The name of your new to do list.

## Controller

Takes a model and view and acts as the controller between them

**Parameters**

-   `model` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** The model instance
-   `view` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** The view instance

### setView

Loads and initialises the view

**Parameters**

-   `locationHash`  
-   `null` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** '' | 'active' | 'completed'

### showAll

An event to fire on load. Will get all items and display them in the
todo-list

### showActive

Renders all active tasks

### showCompleted

Renders all completed tasks

### addItem

An event to fire whenever you want to add an item. Simply pass in the event
object and it'll handle the DOM insertion and saving of the new item.

**Parameters**

-   `title`  

### removeItem

By giving it an ID it'll find the DOM element matching that ID,
remove it from the DOM and also remove it from storage.

**Parameters**

-   `id` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** The ID of the item to remove from the DOM and
    storage

### removeCompletedItems

Will remove all completed items from the DOM and storage.

### toggleComplete

Give it an ID of a model and a checkbox and it will update the item
in storage based on the checkbox's state.

**Parameters**

-   `id` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** The ID of the element to complete or uncomplete
-   `completed`  
-   `silent` **([boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean) \| [undefined](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/undefined))** Prevent re-filtering the todo items
-   `checkbox` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** The checkbox to check the state of complete
                             or not

### toggleAll

Will toggle ALL checkboxes' on/off state and completeness of models.
Just pass in the event object.

**Parameters**

-   `completed`  

### \_updateCount

Updates the pieces of the page which change depending on the remaining
number of todos.

### \_filter

Re-filters the todo items, based on the active route.

**Parameters**

-   `force` **([boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean) \| [undefined](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/undefined))** forces a re-painting of todo items.

### \_updateFilterState

Simply updates the filter nav's selected states

**Parameters**

-   `currentPage`  

## Model

Creates a new Model instance and hooks up the storage.

**Parameters**

-   `storage` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** A reference to the client side storage class

### create

Creates a new todo model

**Parameters**

-   `title` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** The title of the task
-   `callback` **[function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)?** The callback to fire after the model is created

### read

Finds and returns a model in storage. If no query is given it'll simply
return everything. If you pass in a string or number it'll look that up as
the ID of the model to find. Lastly, you can pass it an object to match
against.

**Parameters**

-   `query` **([string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) \| [number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number) \| [object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))?** A query to match models against
-   `callback` **[function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)?** The callback to fire after the model is found

**Examples**

```javascript
model.read(1, func); // Will find the model with an ID of 1
model.read('1'); // Same as above
//Below will find a model with foo equalling bar and hello equalling world.
model.read({ foo: 'bar', hello: 'world' });
```

### update

Updates a model by giving it an ID, data to update, and a callback to fire when
the update is complete.

**Parameters**

-   `id` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** The id of the model to update
-   `data` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** The properties to update and their new value
-   `callback` **[function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)** The callback to fire when the update is complete.

### remove

Removes a model from storage

**Parameters**

-   `id` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** The ID of the model to remove
-   `callback` **[function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)** The callback to fire when the removal is complete.

### removeAll

WARNING: Will remove ALL data from storage.

**Parameters**

-   `callback` **[function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)** The callback to fire when the storage is wiped.

### getCount

Returns a count of all todos

**Parameters**

-   `callback`  

## Store

Creates a new client side storage object and will create an empty
collection if no collection already exists.

**Parameters**

-   `name` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** The name of our DB we want to use
-   `callback` **[function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)** Our fake DB uses callbacks because in
    real life you probably would be making AJAX calls

### find

Finds items based on a query given as a JS object

**Parameters**

-   `query` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** The query to match against (i.e. {foo: 'bar'})
-   `callback` **[function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)** The callback to fire when the query has
    completed running

**Examples**

```javascript
db.find({foo: 'bar', hello: 'world'}, function (data) {
 // data will return any items that have foo: bar and
 // hello: world in their properties
});
```

### findAll

Will retrieve all data from the collection

**Parameters**

-   `callback` **[function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)** The callback to fire upon retrieving data

### save

Will save the given data to the DB. If no item exists it will create a new
item, otherwise it'll simply update an existing item's properties

**Parameters**

-   `updateData` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** The data to save back into the DB
-   `callback` **[function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)** The callback to fire after saving
-   `id` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** An optional param to enter an ID of an item to update

### remove

Will remove an item from the Store based on its ID

**Parameters**

-   `id` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** The ID of the item you want to remove
-   `callback` **[function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)** The callback to fire after saving

### drop

Will drop all storage and start fresh

**Parameters**

-   `callback` **[function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)** The callback to fire after dropping the data

## Template

Sets up defaults for all the Template methods such as a default template

### show

Creates an <li> HTML string and returns it for placement in your app.

NOTE: In real life you should be using a templating engine such as Mustache
or Handlebars, however, this is a vanilla JS example.

**Parameters**

-   `data` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** The object containing keys you want to find in the template to replace.

**Examples**

```javascript
view.show({
id: 1,
title: "Hello World",
completed: 0,
});
```

Returns **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** HTML String of an <li> element

### itemCounter

Displays a counter of how many to dos are left to complete

**Parameters**

-   `activeTodos` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** The number of active todos.

Returns **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** String containing the count

### clearCompletedButton

Updates the text within the "Clear completed" button

**Parameters**

-   `completedTodos` **\[type]** The number of completed todos.

Returns **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** String containing the count

## View

View that abstracts away the browser's DOM completely.
It has two simple entry points:

-   bind(eventName, handler)
    Takes a todo application event and registers the handler
-   render(command, parameterObject)
    Renders the given command with the options

**Parameters**

-   `template`  
