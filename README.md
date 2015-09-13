# JavaScript Interview Questions

💬 What is a potential pitfall with using `typeof bar === "object"` to determine if bar is an object? How can this pitfall be avoided?
`#type` `#variable`

💡 typeof `null` is `object`
```js
(bar !== null) && (typeof bar === "object")
```

- - -

💬 What will the code below output to the console and why?
`#invoke_function` `#variable` `#scope` `#use_strict`
```js
(function(){
  var a = b = 3;
})();

console.log("a defined? " + (typeof a !== 'undefined'));
console.log("b defined? " + (typeof b !== 'undefined'));
```
💡 `b` be defined outside of the scope of the enclosing function, try `"use strict";` to reveal error.
```js
a defined? false
b defined? true
```

- - -

# Template
##### 
```js

```
> 
```js

```
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
