SPELLCHECK
### Table of Contents
-  [Introduction](#introduction)
-  [Program specification](#Program-specification)
-  [Testing results](#Testing-results)
-  [Bug fixing](#Bug-fixing)
-  [Audit](#Audit)
-  [Competitor comparison](#Competitor-comparison)


## Introduction
Todo-list-app is an application that allows to manage a list of tasks. It allows adding, updating, deleting and toggling state od each task. It has minimalistic design and basic functionality.
You can see it working here:

[https://kristoferek.github.io/todo-list-app/](https://kristoferek.github.io/todo-list-app/)

App is a kind of model showing how to implement MVC approach in JavaScript. Model, Controller, View (MVC) methodology separates program logic (model) from display functionality (View) and manages them using separate entity (Controller).

The managing part of program (Contrloller) is resposible for:
1.  listening to user actions from View,
2.  calling Model to perform requested operations,
3.  calling View to diplay results from Model  


## Program specification
You can find detailed description of all functions in [this file](./javascript.md). It was generated automaticly from JavaScript files.

### **HTML** file
The **index.htm** file is the only html file in project. All the actions are managed by js files.
ENTRYPOINT

### CSS files
WHAT EACH FILE DOES
-  **index.css** - Todo-app-list styles
-  ***base.css*** - app commons

### **JavaScript** files

#### MVC model
-  **app.js** creates an instance of program by initiating Model, View and Conroller
-  **controller.js** initiates all user action listeners, delivers methods that connects View interactions with Model operations
-  **model.js** is responsible for data management
-  **view.js** is resposible for displaying data

#### Additional files
-  ***storage.js*** delivers sample data storage solution
-  ***template.js*** delivers template function to display list items, change button states, escape characters
-  ***helper.js*** deliver helper functions for DOM elements querying, wrapping, delegating events  


## Testing results
I performed two staged testing: ***manual*** testing and ***Jasmine*** testing

1. During **maual testing** I found two bugs:
  -  misspelling function declaration "addItem"
  -  generating random ID for list elements without checking past occurance

2. During **Jasmine testing** I found a list ready test. I've written new test learning from existing ones. I've added or refactored tests for:
  -  should show entries on start-up
  -  should show active entries
  -  should show completed entries
  -  should show the content block when todos exists
  -  should highlight "All" filter by default
  -  should toggle all todos to completed
  -  should update the view
  -  should add a new todo to the model
  -  should remove an entry from the model

During writing additional test for checkbox state stayling I found bug in wrong ID specification in <label> selector preventing proper element styling  

## Bug fixing
I corrected following:
-  in ***controller.js***

    replaced ```Controller.prototype.adddItem```

    with ```Controller.prototype.addItem```
-  in ***index.html***

    replaced ```<input class="toggle-all" type="checkbox">```

    with ```<input class="toggle-all" id="toggle-all" type="checkbox">```
- in ***strore.js***

    replaced

        for (var i = 0; i < 6; i++) {
          newId += charset.charAt(Math.floor(Math.random() * charset.length));
        }
    with
        var isUnique = false;

        while (!isUnique){
    			for (var i = 0; i < 6; i++) {
    				newId += charset.charAt(Math.floor(Math.random() * charset.length));
    			}
    			isUnique = true;
    			for (var i = 0; i < todos.length; i++) {
    				if (todos[i].id == newId) {
    					isUnique = false;
    				}
    			}
        }


## Audit
- Audit results section

## Competitor comparison
- Comparison with competitor's audit results
