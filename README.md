# JavaScript Interview Questions

💬 **What is a potential pitfall with using `typeof bar === "object"` to determine if bar is an object? How can this pitfall be avoided?** 
> `#type` `#variable` `#null` `#undefined`

💡 typeof `null` is `object`
```js
(bar !== null) && (typeof bar === "object")
```

- - -

💬 **What will the code below output to the console and why?**
```js
(function(){
  var a = b = 3;
})();

console.log("a defined? " + (typeof a !== 'undefined'));
console.log("b defined? " + (typeof b !== 'undefined'));
```
> `#function_invocation` `#variable` `#scope` `#use_strict`

💡 `b` be defined outside of the scope of the enclosing function, try `"use strict";` to reveal error.
```js
a defined? false
b defined? true
```

- - -

💬 **What will the code below output to the console and why?**
```js
var myObject = {
    foo: "bar",
    func: function() {
        var self = this;
        console.log("outer func:  this.foo = " + this.foo);
        console.log("outer func:  self.foo = " + self.foo);
        (function() {
            console.log("inner func:  this.foo = " + this.foo);
            console.log("inner func:  self.foo = " + self.foo);
        }());
    }
};
myObject.func();
```
> `#closure` `#scope` `#this` `#self` `#function_invocation`

💡 'this' is inner function which foo never defined
```js
outer func:  this.foo = bar
outer func:  self.foo = bar
inner func:  this.foo = undefined
inner func:  self.foo = bar
```

- - -

💬 **What is the significance of, and reason for, wrapping the entire content of a JavaScript source file in a function block?**
> `#closure` `#scope` `#this` `#self` `#function_invocation`

💡 Avoid conflict from other modules and libraries e.g.
```js
// pass jQuery in as $
(function($) { /* $ can be use */ } )(jQuery);
```
or with ready `#noConflict`
```js
// release $ from other
$.noConflict();
// wait for document reay and accept argument as $ and use it
jQuery(document).ready(function($){/* $ can be use */});
```

💬 **What is the significance, and what are the benefits, of including 'use strict' at the beginning of a JavaScript source file?**
> `#use_strict` `#global_variable`

💡 It's best practice to be more strict instead of failed silently.
* **Makes debugging easier** : Code errors that would otherwise have been ignored or would have failed silently will now generate errors or throw exceptions, alerting you sooner to problems in your code and directing you more quickly to their source.
* **Prevents accidental globals** : Without strict mode, assigning a value to an undeclared variable automatically creates a global variable with that name. This is one of the most common errors in JavaScript. In strict mode, attempting to do so throws an error.
* **Eliminates `this` coercion** : Without strict mode, a reference to a this value of null or undefined is automatically coerced to the global. This can cause many headfakes and pull-out-your-hair kind of bugs. In strict mode, referencing a a this value of null or undefined throws an error.
* **Disallows duplicate property names or parameter values** : Strict mode throws an error when it detects a duplicate named property in an object (e.g., var object = {foo: "bar", foo: "baz"};) or a duplicate named argument for a function (e.g., function foo(val1, val2, val1){}), thereby catching what is almost certainly a bug in your code that you might otherwise have wasted lots of time tracking down.
* **Makes eval() safer** : There are some differences in the way eval() behaves in strict mode and in non-strict mode. Most significantly, in strict mode, variables and functions declared inside of an eval() statement are not created in the containing scope (they are created in the containing scope in non-strict mode, which can also be a common source of problems).
* **Throws error on invalid usage of delete** : The delete operator (used to remove properties from objects) cannot be used on non-configurable properties of the object. Non-strict code will fail silently when an attempt is made to delete a non-configurable property, whereas strict mode will throw an error in such a case.

- - -

# References
* http://bahmutov.calepin.co/functional-javascript-interview-question.html
* http://www.skilledup.com/articles/20-must-know-javascript-interview-qa
* http://www.techrepublic.com/blog/software-engineer/javascript-interview-questions-and-answers/
* https://www.interviewcake.com/javascript-interview-questions
* https://blog.udemy.com/javascript-interview-questions/
* http://www.toptal.com/javascript/interview-questions
* https://github.com/diegocard/js-questions/blob/master/questions%2FjQuery.md
* http://www.sitepoint.com/5-typical-javascript-interview-exercises/
* http://www.w3schools.com/js/js_quiz.asp
