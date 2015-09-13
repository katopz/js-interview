# JavaScript Interview Questions

💬 What is a potential pitfall with using `typeof bar === "object"` to determine if bar is an object? How can this pitfall be avoided? 
> `#type` `#variable` `#null` `#undefined`

💡 typeof `null` is `object`
```js
(bar !== null) && (typeof bar === "object")
```

- - -
- - -

💬 What will the code below output to the console and why?
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
- - -

💬 What will the code below output to the console and why?
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
- - -

💬 What is the significance of, and reason for, wrapping the entire content of a JavaScript source file in a function block?
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

- - -
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
