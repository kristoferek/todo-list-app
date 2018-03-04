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

The managing part of program (Contrloller) is responsible for:
1.  listening to user actions from View,
2.  calling Model to perform requested operations,
3.  calling View to display results from Model  


## Program specification
You can find detailed description of all functions in [file javascript.md](./javascript.md). It was generated automatically from JavaScript files using 'documentations' script.

### **HTML** file
- **index.htm** is the only HTML file in project. It is the application entry point.

### CSS files
-  **index.css** - defines all application CSS styles
-  ***base.css*** - defines common styles

### **JavaScript** files
All the actions and user interactions are managed by JavaScript files.

#### MVC model
-  **app.js** creates an instance of program by initiating Model, View and Controller
-  **controller.js** initiates all user action listeners, delivers methods that connects View interactions with Model operations
-  **model.js** is responsible for data management
-  **view.js** is responsible for displaying data

#### Additional files
-  ***storage.js*** delivers sample data storage solution
-  ***template.js*** delivers template function to display list items, change button states, escape characters
-  ***helper.js*** deliver helper functions for DOM elements querying, wrapping, delegating events  

## Testing results
I performed two staged  based testing: ***manual*** testing and ***automatic Jasmine*** based testing

1. During **manual testing** I found two bugs:
  -  misspelling function declaration "addItem"
  -  risky random ID generating for list elements without checking past occurrence

2. During **automatic Jasmine testing** I found a list of ready tests. I've written new test learning from existing ones. I've added or modified tests for:
  -  should show entries on start-up
  -  should show active entries
  -  should show completed entries
  -  should show the content block when todos exists
  -  should highlight "All" filter by default
  -  should toggle all todos to completed
  -  should update the view
  -  should add a new todo to the model
  -  should remove an entry from the model

During writing additional test for stayling of checkbox state I found bug. There was  wrong ID declaration in `<label>` selector preventing proper element styling  

## Bug fixing
I corrected following:
-  in ***controller.js***

    found `Controller.prototype.adddItem`

    replaced with `Controller.prototype.addItem`
-  in ***index.html***

    found `<input class="toggle-all" type="checkbox">`

    replaced with `<input class="toggle-all" id="toggle-all" type="checkbox">`
- in ***strore.js***

    found

        for (var i = 0; i < 6; i++) {
          newId += charset.charAt(Math.floor(Math.random() * charset.length));
        }
    replaced with
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

My impression is that page loads fast, uses small amount of memory and displays content immediately. It is based only on html, css and javascript sources and doesn't require any media files, like images or video as well as fonts or heavy and complicated css files.

#### Loading
*(The worst achieved result)*

- Transfered: **17.KB**
- Transfer time: **625ms**
- DOM loads: **507ms**
- Page loads in: **652ms**
- JS memory heap: **9.2 - 17.2MB**

The majority of loading time is done by JS scripting - over 50%, while rendering and painting take less then 10%.

Memory required by application to start is lower then 20MB which is more then suitable for majorty of devices (even older ones).

Loading testing results are available on below listed snapshots:

[Overview](./img/loading.jpg) :: [Performance](./img/loading_performance.jpg) :: [Memory](./img/loading_memory.jpg) :: [Scripting](./img/loading_scripting.jpg)

#### Operating

1. Operation of **typying in, adding and deleting two list elements**
    - scripting: **16ms**
    - rendering: **70.4ms**
    - memory usage: **+(<2)%**

    [Performance](./img/switch_performance.jpg) :: [Memory](./img/switch_memory.jpg)
2. Operation of continuosly **switching three basic views** between All, Active, Completed
    - scripting: **12.2ms**
    - rendering: **32.7ms**
    - memory usage: **-(<1)%**

3. Operation of **marking one task completed**
    - scripting: **2.7ms**
    - rendering: **27.6ms**
    - memory usage: **-(<1)%**
    [Performance](./img/marking_performance.jpg) :: [Memory](./img/memory_memory.jpg)

4. Operation of **Clearing three completed tasks**
    - scripting: **7.2ms**
    - rendering: **11.3ms**
    - memory usage: **-(<1)%**
    [Performance](./img/clearing_performance.jpg) :: [Memory](./img/clearing_memory.jpg)

Operating fully loaded application requires minimum recources. While using app Dev tools shows low memory usage short scripting and rendering times.

#### Conclusions
App performs very efficient. There is a space for further developments with regards of keeping app small and quick. In my opinion it would be optimal to use dedicated CSS and vanilla JavaScript styling with normalization for different platforms and browsers.

To-do-app can be developed as well as sole application as a very efficient module to be combined in a larger project. One of the key chalanges is to chose appropiate storage solution that will allow to keep simplicity, speed and low recources demand.

## Competitor comparison
- Comparison with competitor's audit results
