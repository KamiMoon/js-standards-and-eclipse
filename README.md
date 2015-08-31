# js-standards-and-eclipse

Just having a W3Schools understanding of JavaScript is not enough.

"JavaScript is the only language people feel like they don't need to learn to use."- Douglas Crockford

I would recommend anything written by Douglas Crockford (http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742), but to get people up to speed here is a quick list of the most important and hardest things for most developers to grasp when dealing with JavaScript. JSHint will automatically detect most of these issues as well.

Also a good link: http://jstherightway.org/

1. Falsey Values
  * JavaScript is dynamically typed and these will evaluate as false while everything else is true:
    * false (boolean)
    * 0 (zero)
    * "" (empty string)
    * null (assigned by programmer)
    * undefined (automatically assigned by JavaScript)
    * NaN (Not a Number, a result of some bad math or operation)
  * All variables are assigned to undefined by default. If a variable is declared like this:
```javascript
var myVar;
```
  * At this point JavaScript doesn't know if myVar is a number, an Object, an Array, or a Function. It could be anything and be used as anything since it is dynamically typed. It is undefined at this point.
  * Unlike Java, testing if myVar is null won't be useful unless you know myVar can be set to null at some point in the program
  * For more information on the difference between null and undefined see: http://stackoverflow.com/questions/5076944/what-is-the-difference-between-null-and-undefined-in-javascript
```javascript
if(myVar){
  //myVar is not false, 0, empty string, null, undefined, or NaN
  //in Java this would be the equivalent of testing if a string was not null and not empty
}
```
* This will be enough in most cases to determine if a variable is useable. Note that this may not be a good idea if myVar can be 0 and that is a valid value.

2. Comparisons
  * Given falsey values and the dynamicly typed nature of JavaScript it is almost always a better idea to use === and !== rather than == and !=
  * The === operator will compare that types are equivalent. The == operator will do type coercion, which can lead to logical errors.
  * For more information see: http://stackoverflow.com/questions/359494/does-it-matter-which-equals-operator-vs-i-use-in-javascript-comparisons
  * JSHint automatically detects this and will give you a warning

3. Hoisting
  * All variables that are used in a function are automatically hoisted to the top of the function and assigned to undefined within the function. This is a hidden feature of the language and you need to be aware of this. It is a good practice to explicitly var (define) your variables at the top of the function and assign them a value (otherwise they are undefined). You do not have to do this for everything, but just be aware that this can be a source of errors.
```javascript
(function() {
  var foo = 1;
  var bar = 2;
  var baz = 3;
 
  alert(foo + " " + bar + " " + baz);
})();
```
  * Result is "1 2 3"
```javascript
(function() {
  //var bar; hidden and hoisted up as undefined
  //var baz; hidden and hoisted up as undefined
 
  var foo = 1;
  alert(foo + " " + bar + " " + baz);
  var bar = 2;
  var baz = 3;
})();
```
  * Result is "1 undefined undefined"
  * JSHint can be configured to enforce that all variables in a function are explicitly defined at the top of the function if you want. You should at least be aware of this feature.
  * See http://www.sitepoint.com/back-to-basics-javascript-hoisting/

4. Function Scope
  * JavaScript has function scope rather than block scope like Java.
  * For example here is a for loop:
```javascript
var myFunction = function(){
  //var i; note this is hoisted to the top of the function and is undefined
 
  for ( var i = 0; i < 5; i++) {
    //doStuff
  }
  //i is still in scope and will be incremented
 
  for (; i < 5; i++) {
    //won't execute because i is already incremented
  }
  //i is still in scope and will be incremented
}
```
  * Instead of block scope we have function scope. A function inside of another function has acess to the variables of the outer function
```javascript
var myParent = function(){
  var myNumber = 5;
 
  //in JavaScript functions can be assigned to variables and a function can have a variable that is a function
  var myChild = function(){
    //myNumber is still in scope here
  };
 
}
```
  * This is a powerful feature of the language and allows for closures. For more information on closures see: http://javascriptissexy.com/understand-javascript-closures-with-ease/

5. Global scope
  * If you do not declare your variable using var it will seep out of function scope into the global scope
```javascript
var function1 = function(){
  //seeps out into global scope!
  i = 5;
}
var function2 = function(){
  //clobbering the global variable!
  i = 4;
}
```
  * JSHint will detect this. Always declare your variables.

6. Object and Array literals
  * Use {} rather than new Object() and [] rather than new Array()
  * http://yuiblog.com/blog/2006/11/13/javascript-we-hardly-new-ya/
  * Pretty much the only time you will be using new is for using a constructor function
  * This is primarily a style thing for writting modern JavaScript.

7 . The usage of this depends on the context. It is dynamicly assigned.

```javascript
var myObj = {
  age: 5,
  doStuff: function(){
    //store a reference to ourself
    var that = this;
 
    console.log("----------------------------------------");
    console.log("Inside my own function: " + this.age); //5
 
    //timeout callback
    setTimeout(function(){
      //this refers to a context defined at a later time within the timeout
      console.log("Inside a timeout callback using 'this' " + this.age);  //undefined
      console.log("Inside a timeout callback using 'that' " + that.age);  //5
    });
 
    //ajax callback
    $.get("www.google.com", function( data ) {
      //this refers to the ajax request
      console.log("Inside an ajax callback using 'this' " + this.age);  //undefined
      console.log("Inside an ajax callback using 'that' " + that.age);  //5
    });
 
    //click callback
    $("#myButton").on("click", function(e){
      //this refers to click event and what you clicked on
      console.log("Inside an click callback using 'this' " + this.age);  //undefined
      console.log("Inside an click callback using 'that' " + that.age);  //5
    });
  }
};
 
myObj.doStuff();
```
  * You can save a reference to the context you want in a variable.  For consistency this can be called "that."
  * More information on this http://javascriptissexy.com/understand-javascripts-this-with-clarity-and-master-it/

8. Function are first class.
  * Not really a source of errors, but it is key to understanding JavaScript.
  * Unlike Java, function are first-class objects. They can be stored in variables, passed as arguments to functions, created within functions, and returned from functions. This allows for functional programming and is used heavily in JavaScript as callbacks. http://javascriptissexy.com/tag/higher-order-functions/

9. setTimeout can be used to fix display issues when timing is an issue
  * http://stackoverflow.com/questions/779379/why-is-settimeoutfn-0-sometimes-useful
  * setTimeout with 0 often just means "do this when it is done rendering"
  * For examples this can be used with the jQuery UI drag and drop plugin to synchronize having one action occur after something is dropped and done rendering.

10. JavaScript can simulate "private" variables
  * http://javascript.crockford.com/private.html
 
11. JavaScript can simulate "classical" inheritance
  * Class.js by John Resig (creator of jQuery) http://ejohn.org/blog/simple-javascript-inheritance/
  * http://www.crockford.com/javascript/inheritance.html

12. Use a native for loop for performance reasons. Don't use library forEach or native forEach. In Chrome native for loops are much faster than everything else.

13.  Use normal camel case for javaScript variables that are not constants
```javascript

var MY_CONSTANT = 5;
var myVariable = 5;
 
var some_variable = 5; //bad
```


# Recommended way to import a JS project into Eclipse
* Temporarily turn off build automatically, because node_modules folder is too big.
* File->New>JavaScript Project pick the option to create project from existing source.
* Under Project facets convert to JavaScript.
* In include paths add node_modules as excluded.

# Install and use JSHint with Eclipse
* Website:  http://jshint.com/about/
* Configuration Options:  http://jshint.com/docs/options/
* Eclipse plugin:  http://github.eclipsesource.com/jshint-eclipse/
* JSHint File:  https://github.com/KamiMoon/js-standards-and-eclipse/blob/master/jshint/.jshintrc
* Under project properties make sure JavaScript is selected as a project facet. This will enable JavaScript tooling for Eclipse. Eclipse comes with some minimal tooling for JavaScript. JSHint will enhance the tooling further.
* Follow the instructions to install the plugin: http://github.eclipsesource.com/jshint-eclipse/install.html
* A .jshintrc file will need to be placed in the root of your project.
* Once the plugin is installed and Eclipse is restarted you will have a JSHint option on your project properties where you can configure JSHint. Configure the includes, excludes, and tell the plugin to use the .jshintrc file.

# JavaScript Code Formatter
* Windows->Preferences->JavaScript->Code Style->Formatter. Import https://github.com/KamiMoon/js-standards-and-eclipse/blob/master/formatter/javascript-formatter.xml and apply these settings.
* Windows->Preferences->JavaScript->Code Style->Clean Up. Import https://github.com/KamiMoon/js-standards-and-eclipse/blob/master/formatter/javascript-cleanup.xml and apply these settings.
* Under Windows->Preferences->JavaScript->Editor->Save Actions perform the selectied actions on save:  Format Source code.  Additonal actions:  Convert control statement bodies to block, remove uncessary parentheses, remove trailing whitespaces on all lines

# AngularJS Plugin
* Follow instructions here and install:  https://github.com/angelozerr/angularjs-eclipse


