# Canvas Best Practice

This best practice guide is provided to help you build applications using 
[Canvas for TM1](https://canvasfortm1.com) that are easy to maintain and 
advantage of all of the Canvas features.

There are some keys principles of this document:
 * Consistency **IS** quality!
 * Readability is more important than reducing key strokes.
 * All names (variables, class names, etc) should describe it's usage.
 * Comment anything that is obvious.

## Table of Contents

 * [General Rules](#general-rules)
 * [HTML](#html)
 * [Styles (CSS)](#styles)
 * [Javascript](#javascript)
 * [Logic in HTML or Controllers?](#logic-in-html-or-controllers)

## <a name="general">General Rules</a>

  * Having consistent names and case makes your code easier to follow.
  * Always use the Page Creator in the /admin console to create new pages.
  * It will create a HTML page and JavaScript controller.
  * Use inline code for simple operations.
  * Create $scope functions for more complicated code so it can be easily debugged or for reused in the page.
  * Avoid the use of $root scope to pass parameters between pages.
  * Use state parameters to pass simple values from one page to another.
  * Update URL query parameters each time a selection is made in the page. This is important for PDF creation.
  * Use Bootstrap as much as possible, it will give the look and feel consistency and allow you to switch between themes.
  * Do not use JQuery, i.e. `$("class")...`, use Angular 1 directives instead.


## HTML

  * All html elements, attributes and id's should be **lower-case**
  * Use hyphen to separate words in a value: `id="myElement"` becomes `id="my-element"`.
  * Use 2 spaces as indentation (the default in VS Code).
  * Always indent child blocks inside a parent element.
  * Use empty lines to separate logical code blocks.
  * For elements with many attributes place one on each line (indented) instead of a single line.
  * Always use double-quotes for values for element attributes.
  * The one exception to the above rule is for `tm1-elements`. For this attribute it is better to 
  use single quotes so elements can be qualified with a double quote.

```html

  <!-- BAD -->
  <DIV ID="myELEMENT" >
  </DIV>

  <!-- BETTER, use lower-case and words with a hyphen -->
  <div id="my-element" >
  </div>

```

```html

  <!-- BAD -->
  <div>
  <ul>
  <li></li>
  </ul>
  </div>

  <!-- BETTER, indent your elements -->
  <div>
    <ul>
      <li></li>
    </ul>
  </div>

```

```html

  <!-- BAD -->
  <tm1-ui-dbr tm1-instance="Instance Name" tm1-cube="Cube Name" tm1-elements='Comma separated element list' tm1-comment-cube="Cube Name" tm1-comment-elements='Comma separated element list' tm1-picklist-radio="none" tm1-multi-line="1" tm1-read-only="false" tm1-comment-read-only="false">
  </tm1-ui-dbr>

  <!-- BETTER, use a single attribute per line -->
  <tm1-ui-dbr
     tm1-instance="Instance Name"
     tm1-cube="Cube Name"
     tm1-elements='Comma separated element list'
     tm1-comment-cube="Cube Name"
     tm1-comment-elements='Comma separated element list'
     tm1-picklist-radio="none"
     tm1-multi-line="1"
     tm1-read-only="false"
     tm1-comment-read-only="false"
     >
  </tm1-ui-dbr>

```

### Styles

  * Don't use `<table>` elements to layout your page. 
  * Use Bootstrap `class="col-md-4"` classes instead, this will make your page responsive to different browser sizes.
    * SEE: [Bootstrap Grid System](http://getbootstrap.com/css/#grid)
  * Style all of your visual elements: tables, buttons, input, select, labels, etc with Bootstrap classes.
  * Limit the use of the style attribute on elements.
  * If you repeat a particular style on two or more elements make it a CSS class instead.
  * Before creating your own styles try to use a Bootstrap one instead. This will allow you to change themes easily.
    * SEE: [Bootstrap CSS helper classes](http://getbootstrap.com/css/#helper-classes)
  * Place page specific styles in a `<style>` element at the top of the page.
  * If you use a CSS class on more than one page place it in the `\css\style.css`
  * CSS class names should be **lower-case** and hyphenated between words: `warning-message`

```html

  <!-- BAD, don't use tables for page layouts -->
  <table style="width: 100%;">
    <tr>
      <td>
        Left Column
      </td>
      <td>
        Right Column
      </td>
    </tr>
  </table>

  <!-- BETTER, use Bootstrap grid system instead -->
  <div class="row">
    <div class="col-md-6">
      Left Column
    </div>
    <div class="col-md-6">
      Right Column
    </div>
  </div>

```

```html

  <!-- BAD, remember to add the Bootstrap classes  -->
  <table></table>
  <button></button>
  <input></input>
  <select></select>

  <!-- BETTER, add the relevant Bootstrap classes -->
  <table class="table table-striped"></table>
  <button class="btn btn-primary"></button>
  <input class="form-control"></input>
  <select class="form-control"></select>

```

```html

  <!-- BAD, don't repeat styles -->
  <table class="table table-striped" >
    <tr>
      <td style="text-align: right;"></td>
      <td style="text-align: right;"></td>
    </tr>
  </table>

  <!-- BETTER, use either a Bootstrap class or a custom one -->
  <table class="table table-striped" >
    <tr>
      <td class="text-right"></td>
      <td class="text-right"></td>
    </tr>
  </table>

```

```html 

  <!-- Use the style element for custom styles -->
  <style>

    .custom-style {
      text-align: right;
      font-weight: bold;
    }

  </style>

```

```css

  /* Add classes for multiple pages in css/style.css */
  .custom-style {
    text-align: right;
    font-weight: bold;
  }

```

```css

  /* BAD, CSS classes should be lower case */
  .CUSTOMSTYLE {
    text-align: right;
    font-weight: bold;
  }

  /* BAD, separate words with a hyphen */
  .customstyle {
    text-align: right;
    font-weight: bold;
  }

  /* BETTER, lower-case and hyphen as a separator */
  .custom-style {
    text-align: right;
    font-weight: bold;
  }

```

## JavaScript
These JavaScript rules apply to both code in your controllers as well as inline code. 
Inline code is any JavaScript inside Angular directives such as: `ng-if`, `ng-show`, `ng-click`, etc. Example:
```html

  <!-- The code inside ng-click is just regular JavaScript -->
  <!-- The semi-colons are required with writing multiple commands -->
  <button class="btn btn-primary" ng-click="page.instance = 'dev'; page.cube = 'General Ledger';">Click Me!</button>

```

```javascript

  // The above code is equivalent to:
  $scope.page.instance='dev'; 
  $scope.page.cube = 'General Ledger';


```

* Always indent your blocks of code, i.e. if, for, etc.
* Use two spaces as indentation (the default in VS Code).
* Use empty lines to separate logical code blocks.
* Use whitespace and multiple lines to increase readability.
* Always use curly braces for all code blocks.
* All variables should use **camelCase**.
* Don't use prefixes on your variable names to indicate scope or the data type.
* Declare $scope variables in your controller
* Don't use ng-init to declare variables
* All $scope level variables should be part of an object
* Code should be in the following order: 
  1. $scope level variables
  1. Any functions
  1. Any initialisation code, i.e. requests to the server.
  

```javascript

  // BAD
  if( condition ){
  // No indentation
  for(var i = 0; i < 10; i++){
  // Do something
  }
  }

  // BETTER
  if( condition ){
    // Indentation makes is easier to read! 
    for(var i = 0; i < 10; i++){
      // Do something
    } 
  }

```

```javascript

  // BAD, no empty lines
  $scope.page = {
    instance: "dev"
  }
  $scope.getCubes = function(){
    $http.get("api/cubes/" + $scope.page.instance).then(function(success, error) {
      $scope.cubes = success.data.value
    });
  };
  $scope.dimensionNames = function(cube){
    var dims = [];
    _.each(cube.Dimensions, function(dim){
      dims.push(dim.Name);
    });
    return dims.join(", ");
  }

  // BETTER, a line between blocks makes it easier to read
  $scope.page = {
    instance: "dev"
  }

  $scope.getCubes = function(){
    $http.get("api/cubes/" + $scope.page.instance).then(function(success, error) {
      $scope.cubes = success.data.value
    });
  };

  $scope.dimensionNames = function(cube){
    var dims = [];
    _.each(cube.Dimensions, function(dim){
      dims.push(dim.Name);
    });
    return dims.join(", ");
  }


```

```javascript

  // BAD, always use braces and use whitespace
  if( condition ) $scope.instance = "prod";
  
  // BETTER, braces are always used and blocks should be over multiple lines
  if( condition ){
    $scope.instance = "prod"; 
  }

```

```javascript

app.controller('SampleCtrl', ['$scope', '$rootScope', '$interval', '$timeout', '$state', '$stateParams', '$http', '$location', function($scope, $rootScope, $interval, $timeout, $state, $stateParams, $http, $location) {
	
  // Declare $scope variables first
  $scope.page = {
    region: "Europe",
    department: "Corporate",
    version: "Budget"
  };

  // Declare any functions
  $scope.loadData = function(){
    // Add load logic
  };
	
  // Call any functions
  $scope.loadData();

});


```

## Logic in HTML or Controllers

One of the first questions you are going to ask when developing your first Canvas applications is when to use inline
JavaScript or add page logic to the controller. Canvas was built to minimise the amount of code that needs to be written.
It does most of the heavy-lifting for you, what you need to decide is whether you and fellow developers can easily 
maintain and follow the code.

In this section we will outline the pro's and con's of both methods. It is likely you will use both depending on the
complexity of logic if it needs to be reused.


### Simple rules for when to use inline JavaScript:

  * If your logic is simple, one or two commands only. This will be the case for most pieces of logic.
  * If the code isn't required in multiple locations on the page.

### Simple rules for when to use $scope Functions:

  * If the logic is complex or requires conditional statements or loops.
  * If the piece of logic needs to be reused.
  * If you are having problems in your page and need to debug your logic.
  * If you need access JavaScript libraries and functions.



### Inline HTML Logic

Inline logic is added directly to the attributes (AngularJS directives) on your HTML elements such as `ng-click`,
`ng-if` and `ng-class`. The code is just regular JavaScript that has direct access to the variables in $scope, i.e.
you do not have to prefix the variables with `$scope.`. See the example below:  

```html

  <!-- The code inside ng-click is just regular JavaScript -->
  <button class="btn btn-primary" ng-click="page.instance = 'dev'">Click Me!</button>

```

You can create more complicated logic by using regular JavaScript syntax, you are however restricted to a single line. 
Use semi-colons to separate multiple lines of code.

```html

  <!-- The code inside ng-click is just regular JavaScript -->
<button class="btn btn-primary" ng-click="if( condition ) { page.instance = 'dev'; } else { page.instance = 'prod'; }">Click Me!</button>

```


The above method is the easiest method to add logic to your page and should be used as the default method. Below 
is a summary of the advantages and disadvantages.

| Advantages | Disadvantages |
| ---------- | ------------- |
| Code is inline so it is easy to see the logic without switching to a JavaScript file | Code is placed on one line making multiple statements hard to read |
| Variables that don't exist are automatically created including the hierarchy | Variables are automatically created making it easy for a typo in a variable name to be missed |
| No need to prefix variables with $scope | Most errors in your logic fail silently making it difficult to find issues |
| You don't have to know a lot about JavaScript | You can't debug the code in your browser developer tools |
| | No direct access to JavaScript libraries such as Math |


### Controller Logic

You can also use the Angular (v1) controller for your logic. This is the best practice when developing regular Angular (v1) applications 
as it enables the separation of the model (data), view (HTML) and controller (logic). This is called the MVC pattern and is widely used 
it all types of modern applications. 

Canvas applications are a little different because the directives are designed to do much of the heavy lifting for you, i.e. you don't 
need to create queries and request data from the server using API's. This means that you controller will be limited to more advanced 
scenarios such as querying the API's directly or adding complicated logic.

The controller is a JavaScript file that has the same name as your HTML file, for example `/html/home.html` has a corresponding file 
called `/js/controllers/home.js`. Below are some examples of placing logic in controller: 

```html

  <!-- Initialise the value of a scope variable -->
  <!-- The 'page' object gets create automatically and the 'instance' property added to it
  <div ng-init="page.instance = 'dev'"></div>

```

Becomes:


```javascript

  // Initialise the value of a scope variable
  // Create the 'page' object with an 'instance' property
  // Only create the 'page' object once
  $scope.page = {
    instance: "dev",
    secondProperty: "something"
  };

  // The 'page' object was created above so we can now use the dot (.) notation to create a property
  $scope.page.thirdProperty = "something else";

  // You could also initial the 'page' variable as an empty logic
  $scope.page = {};
  $scope.page.instance = "dev";
  $scope.page.secondProperty = "something";

```

```html 

  <!-- Set the 'department' property on the 'page' object to 'Administration'  -->
  <button ng-click="page.department = 'Administration'" >Administration</button>
  
```

Becomes

```javascript

  // Create a function in the controller
  // This can be used multiple times on your page
  $scope.setDepartment = function(department){
    $scope.page.department = department;
    // Add extra logic here
  };

```

```html

  <!-- Use the setDepartment function on ng-click  -->
  <button ng-click="setDepartment('Administration')" >Administration</button>

```

 
