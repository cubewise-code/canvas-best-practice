# Canvas Best Practice

This best practice guide is provided to help you build applications using 
[Canvas for TM1](https://canvasfortm1.com) that are easy to maintain and 
advantage of all of the Canvas features.

There are some keys principles of this document:
 * Consistency **IS** quality!
 * Readability is more important than reducing key strokes.
 * All names (variables, class names, etc) should describe it's usage.
 * Comment anything that isn't obvious.

## Table of Contents

 * [General Rules](#general-rules)
 * [HTML](#html)
 * [Styles (CSS)](#styles)
 * [Javascript](#javascript)
 * [Logic in HTML or Controllers?](#logic-in-html-or-controllers)
 * [Optimising Performance](#optimising-performance)

## General Rules

  * Having consistent names and case makes your code easier to follow.
  * Always use the Page Creator in the /admin console to create new pages.
  * It will create a HTML page and JavaScript controller.
  * Use inline code for simple operations.
  * Create $scope functions for more complicated code so it can be easily debugged or for reused in the page.
  * Avoid the use of $root scope to pass parameters between pages.
  * Use state parameters to pass simple values from one page to another.
  * Update URL query parameters each time a selection is made in the page. This is important for PDF creation.
  * Use Bootstrap as much as possible, it will give the look and feel consistency and allow you to switch between themes.
  * Do not use JQuery, i.e. `$(".class")...`, use Angular 1 directives instead. JQuery doesn't work well wih Angular applications.

##### <a href="#table-of-contents">(Back to Top)</a>

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

##### <a href="#table-of-contents">(Back to Top)</a>

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

##### <a href="#table-of-contents">(Back to Top)</a>

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
* All variables should be enclosed in an object as per Angular best practice.
* A standard set of buckets for variables are as follows:
  * `lists.*` should be used to store any lists that are used with ng-repeat, i.e. `tm1-ui-element-list`.
  * `selections.*` should be used for all selections that are made by a user in the page. Any values in 
  `selections` should be URL parameters as well. This will allow server-side PDF generation.
  * `options.*` should be used to store non-data driven variables or ones that aren't mirrored
  in the URL, i.e. show/hide an element in a page.
* When showing and hiding elements in a page you should indicate what it does via the name remembering that 
the default value for all variables is `false`, i.e. `null` is also `false`. Examples: 
  * Element that defaults to hidden: `ng-if="options.showDetail"`
  * Element that defaults to visible: `ng-if="options.hideDetail"`
* Don't use prefixes on your variable names to indicate scope or the data type.
* All $scope level variables should be part of an object
* Code should be in the following order: 
  1. $scope level variables
  1. Any functions
  1. Any initialisation code, i.e. requests to the server.


```javascript 

  // BAD
  $scope.ShowDetail = false;

  // BETTER, variables should be camelCase and part of an object
  $scope.options = {
    showDetail: false
  } 

```

```html 

  <!-- BAD -->
  <div ng-int="ShowDetail = false"></div>

  <!-- BETTER, variables should be camelCase and be part of an object -->
  <div ng-int="options.showDetail = false"></div>

```
  

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

##### <a href="#table-of-contents">(Back to Top)</a>

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
| Variables that don't exist are automatically created including the hierarchy, i.e. i.e. you can just initialise `page.instance = "dev"` and Angular will create the page object for you. | Variables are automatically created making it easy for a typo in a variable name to be missed |
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

Becomes:

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

  <!-- You can reuse the same function again -->
  <button ng-click="setDepartment('Sales')" >Sales</button>

```

| Advantages | Disadvantages |
| ---------- | ------------- |
| Code is more readable: multiple lines, comments, etc. | Code is in a separate file so you need move back and forth to find the function |
| You can reuse the logic throughout the page | JavaScript can be seen as too **techie** |
| You have full access to the built-in JavaScript libraries and can add Angular services | |
| Most errors can be seen in the JavaScript console in your browser |  |
| You can debug the code in your browser developer tools (press F12) | |

##### <a href="#table-of-contents">(Back to Top)</a>

## Optimising Performance

Performance is an important consideration in any application. Canvas is designed to be easy to use, even for people with little coding background.
Canvas obfuscates most of the difficult parts leaving you to focus on page design and functionality. This doesn't mean that you can just set and forget
the content on your page, there is a limit to the amount of content a browser can handle quickly.

Before we outline the best practices it makes sense to describe how Canvas works and therefor it's benefits and limitations. A Canvas page is built
with a collection of Angular directives that send information to the TM1 server and each other. Below is a sample of a very simple page:

 ```html

  <!-- A SUBMN directive is used to display a list of elements as a drop-down -->
  <tm1-ui-subnm
    tm1-instance="dev"
    tm1-dimension="Department"
    tm1-subset="Default"
    tm1-default-element="6"
    tm1-select-only="true"
    ng-model="page.department"> <!-- Is updated when an item is selected -->
  </tm1-ui-subnm>

  <!-- The DBR retrieves a value from a TM1 cell and displays in on the page -->
  <!-- When the page.department variable is updated in the SUBNM the DBR is refreshed -->
  <tm1-ui-dbr
    tm1-instance="dev"
    tm1-cube="General Ledger"
    tm1-elements='Actual,2011/12,Mar,Local,England,{{page.department}},Employee Benefits,Amount'
   >
  </tm1-ui-dbr>

 ``` 

The steps that turn this into a functioning page are as follows:

  1. The HTML source page is loaded from the server.
  2. The HTML is parsed by Angular so it can identify any directives in the page.
  3. The `tm1-ui-subnm` and `tm1-ui-dbr` directives are loaded and replaced with regular HTML in the page.
    * The `tm1-ui-subnm` is turned into a `<select>` element.
    * The `tm1-ui-dbr` is converted into a `<span>` element.
  4. `tm1-ui-subnm` loads the subset from TM1 using the REST API (via the Canvas server). 
  5. `tm1-ui-dbr` creates a request and adds it to the **request** queue.
  6. When requests stop being added to the **request** queue Canvas sends a batch request to the Canvas server.
  7. The Canvas server converts the requests into one or more MDX statements and issues a request to the TM1 Server.
  8. The results from the TM1 server then are set back to the browser to be displayed in the page.
  9. The `tm1-ui-dbr` places a **watch** of the `page.department` variable waiting for any changes.
  10.When a user selects an element from the `tm1-ui-subnm` list the `tm1-ui-dbr` recognises the change and repeats steps 5 - 8.
  11. Angular also places **watches** on all of the directives waiting for any changes. See [The Digest Loop and Apply](https://www.ng-book.com/p/The-Digest-Loop-and-apply/)

 
There is quite a lot going on here but it is important to understand that for every `tm1-ui-dbr` on a page there is a request
and value to be retrieved using a MDX query. For every `tm1-ui-*` directive the page also needs to convert the directive to 
HTML. Some directives such as the `tm1-ui-dbr` have complicated logic to handle comments, validation, formating, text boxes, 
rich-text, etc. 

What this means is that you need to think about the number of directives you place on a page. There is a limit to the number 
of items you can place of a page while maintaining acceptable performance. Luckily there are some easy steps you can take to
manage this number and still have the functionality you expect.


### `ng-if` vs `ng-show/hide`

Before going into specific Canvas tips we need to understand the difference between `ng-if` and `ng-hide`/`ng-show`. Although
they seem to do the same thing how they do it is very different. `ng-if` when set to `false` removes the element from page (DOM)
so it no longer exists. `ng-show` when `false` on the other hand adds `display: none` to the element so it is hidden but still 
exists. Take a look at the examples below:

```html

  <!-- ng-if set to false -->
  <div ng-if="false"></div>

  <!-- The result in the page is just a comment -->
  <!-- ngIf: false -->

  <!-- ng-if set to false -->
  <div ng-show="false"></div>

  <!-- The result has the ng-hide CSS class added which contains: display: none !important; -->
  <div ng-show="false" class="ng-hide"></div>

```

What this means for your pages is that elements hidden using `ng-hide/show` are still present in the page and therefore
are calculated and take up resources. Elements that are hidden with `ng-if="false"` no longer exist and require no calculation
or resources. When you set `ng-if="true"` the elements will be dynamically loaded and updated on the fly.


### Tips for keeping your Canvas page nice and fast

* Limit the number of DBR's on a page to less than 1,000. 
* Use a combination of paging and `ng-if` to limit the amount of content on a page.
* Dynamic parts of a page that shown on demand should toggle `ng-if`.
* Modal and dialog content should be removed with `ng-if="false"` until they are needed.
* For large requests with lots of rows consider using named MDX statements and `$tm1Ui.resultsetTransform()` instead of DBRs.

##### <a href="#table-of-contents">(Back to Top)</a>
