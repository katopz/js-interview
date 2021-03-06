# JavaScript Interview Questions

📝 [25 Essential JavaScript Interview Questions](http://www.toptal.com/javascript/interview-questions)

- - -

💬 **What is a potential pitfall with using `typeof bar === "object"` to determine if bar is an object? How can this pitfall be avoided?** 
> `#scope` `#type` `#variable` `#null` `#undefined`

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
* **Eliminates `this` coercion** : Without strict mode, a reference to a this value of null or undefined is automatically coerced to the global. This can cause many headfakes and pull-out-your-hair kind of bugs. In strict mode, referencing a `this` value of null or undefined throws an error.
* **Disallows duplicate property names or parameter values** : Strict mode throws an error when it detects a duplicate named property in an object (e.g., `var object = {foo: "bar", foo: "baz"};`) or a duplicate named argument for a function (e.g., `function foo(val1, val2, val1){}`), thereby catching what is almost certainly a bug in your code that you might otherwise have wasted lots of time tracking down.
* **Makes eval() safer** : There are some differences in the way `eval()` behaves in strict mode and in non-strict mode. Most significantly, in strict mode, variables and functions declared inside of an eval() statement are not created in the containing scope (they are created in the containing scope in non-strict mode, which can also be a common source of problems).
* **Throws error on invalid usage of delete** : The `delete` operator (used to remove properties from objects) cannot be used on non-configurable properties of the object. Non-strict code will fail silently when an attempt is made to delete a non-configurable property, whereas strict mode will throw an error in such a case.

- - -

💬 **Consider the two functions below. Will they both return the same thing? Why or why not?**
```js
function foo1()
{
  return {
      bar: "hello"
  };
}

function foo2()
{
  return
  {
      bar: "hello"
  };
}

console.log("foo1 : " + foo1());
console.log("foo2 : " + foo2());
```
> `#pitfall`
💡 It'll see as `return;` because `;` are optional.
```js
foo1 :[object Object]
foo2 : undefined
```
- - -

💬 **What is `NaN`? What is its type? How can you reliably test if a value is equal to `NaN`?**

> `#pitfall` `#Number` `#NaN`

💡 Stand for `Not a Number` but beware `typeof NaN === "number"` is `true`
```js
// 
isNaN(NaN);       // true
isNaN(undefined); // true
isNaN({});        // true

isNaN(true);      // false
isNaN(null);      // false
isNaN(37);        // false

// strings
isNaN("37");      // false: "37" is converted to the number 37 which is not NaN
isNaN("37.37");   // false: "37.37" is converted to the number 37.37 which is not NaN
isNaN("");        // false: the empty string is converted to 0 which is not NaN
isNaN(" ");       // false: a string with spaces is converted to 0 which is not NaN

// dates
isNaN(new Date());                // false
isNaN(new Date().toString());     // true

// This is a false positive and the reason why isNaN is not entirely reliable
isNaN("blabla")   // true: "blabla" is converted to a number. 

// extra point for ES6
Number.isNaN(NaN);
```
📎 [isNaN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/isNaN#Confusing_special-case_behavior)

- - -

💬 **What will the code below output? Explain your answer.**

```js
console.log(0.1 + 0.2);
console.log(0.1 + 0.2 == 0.3);
```

> `#pitfall` `#Number`

💡 Stand for `Not a Number` but beware `typeof NaN === "number"` is `true`
```js
0.30000000000000004
false
```

- - -

💬 **Discuss possible ways to write a function isInteger(x) that determines if x is an integer.**
> `#pitfall` `#Number` `#Integer`

💡 ES6 not provide `Number.isInteger()` 
```js
function isInteger(x) { return Math.round(x) === x; }
```

- - -

💬 **In what order will the numbers 1-4 be logged to the console when the code below is executed? Why?**
```js
(function() {
    console.log(1); 
    setTimeout(function(){console.log(2)}, 1000); 
    setTimeout(function(){console.log(3)}, 0); 
    console.log(4);
})();
```
> `#pitfall` `#async`

💡 Async will do thing after inline code.
```js
1
4
3
2
```

- - -

💬 **Write a simple function (less than 80 characters) that returns a boolean indicating whether or not a string is a [palindrome](http://www.palindromelist.net/).**

> `#algorithm`

💡 Check word == reversed_word
```js
function isPalindrome(str) {
    // trim non word and make it lower case
    str = str.replace(/\W/g, '').toLowerCase();
    // compare with reversed text
    return (str == str.split('').reverse().join(''));
}
console.log(isPalindrome("level"));                   // logs 'true'
console.log(isPalindrome("levels"));                  // logs 'false'
console.log(isPalindrome("A car, a man, a maraca"));  // logs 'true'
```

- - -

💬 **Write a `sum` method which will work properly when invoked using either syntax below.**
```js
console.log(sum(2,3));   // Outputs 5
console.log(sum(2)(3));  // Outputs 5
```
> `#algorithm` `#arguments` `#functional`

💡 Use functional programming
```js
function sum(x) {
  if (arguments.length == 2) {
    return arguments[0] + arguments[1];
  } else {
    return function(y) { return x + y; };
  }
}
```
or
```js
function sum(x, y) {
  if (y !== undefined) {
    return x + y;
  } else {
    return function(y) { return x + y; };
  }
}
```

- - -

💬 **Consider the following code snippet:**
```js
for (var i = 0; i < 5; i++) {
  var btn = document.createElement('button');
  btn.appendChild(document.createTextNode('Button ' + i));
  btn.addEventListener('click', function(){ console.log(i); });
  document.body.appendChild(btn);
}
```
(a) What gets logged to the console when the user clicks on “Button 4” and why?
(b) Provide one or more alternate implementations that will work as expected.

> `#closure` `#scope`

💡 `i` is `5` forever, need input i to closure function.
```js
...
(function (i) {
  btn.addEventListener('click', function() { console.log(i); });
})(i);
...
```
- - -

💬 **What will the code below output to the console and why?**
```js
var arr1 = "john".split('');
var arr2 = arr1.reverse();
var arr3 = "jones".split('');
arr2.push(arr3);
console.log("array 1: length=" + arr1.length + " last=" + arr1.slice(-1));
console.log("array 2: length=" + arr2.length + " last=" + arr2.slice(-1));
```
> `#array` `#referrence`

💡 Here's what happen. `silce(-1)` will pick 1 item backward which is `arr3`
```js
var arr1 = "john".split('');    // arr1 = ["j","o","h","n"]
var arr2 = arr1.reverse();      // arr2 = arr1 = ["n","h","o","j"]
var arr3 = "jones".split('');   // arr3 = ["j","o","n","e","s"]
arr2.push(arr3);                // arr2 = arr1 = ["n","h","o","j",[,"j","o","n","e","s"]]
```
output
```js
array 1: length=5 last=j,o,n,e,s
array 2: length=5 last=j,o,n,e,s
```
- - -

💬 **What will the code below output to the console and why ?**
```js
console.log(1 +  "2" + "2");
console.log(1 +  +"2" + "2");
console.log(1 +  -"1" + "2");
console.log(+"1" +  "1" + "2");
console.log( "A" - "B" + "2");
console.log( "A" - "B" + 2);
```
> `#String` `#Number``#operation`

💡 Rules : `1 +  "2" = "12"` and `-"1" = -1` also last one will judge type
```js
122
32
02
112
NaN2
NaN
```
- - -

💬 **The following recursive code will cause a stack overflow if the array list is too large. How can you fix this and still retain the recursive pattern?**

```js
var list = readHugeList();

var nextListItem = function() {
    var item = list.pop();

    if (item) {
        // process the list item...
        nextListItem();
    }
};
```
> `#recursive` `#async`

💡 Delay funcation call by `setTimeout`
```js
var list = readHugeList();

var nextListItem = function() {
    var item = list.pop();

    if (item) {
        // process the list item...
        setTimeout( nextListItem, 0);
    }
};
```

- - -

💬 **What is a “closure” in JavaScript? Provide an example.**
> `#recursive` `#async`

💡 A closure is an inner function that has access to the variables in the outer (enclosing) function’s scope chain.
```js
var x = 1;
(function(y) {
    var i = "i";
    console.log("i:" + i);
    console.log("x:" + x);
    console.log("y:" + y);
    (function(z) {
        var j = "j";
        console.log("i:" + i);
        console.log("j:" + j);
        console.log("x:" + x);
        console.log("y:" + y);
        console.log("z:" + z);
    })(3);
})(2);

```

- - -

💬 **What will be the output of the following code:**

```js
for (var i = 0; i < 5; i++) {
  setTimeout(function() { console.log(i); }, i * 1000 );
}
```
**Explain your answer. How could the use of closures help here?**

> `#closure` `#async`

💡 Only `5` is print, Need closure to cover `setTimeout`
```js
for (var i = 0; i < 5; i++) {
  (function(i){
    setTimeout(function() { console.log(i); }, i * 1000 );
  })(i);
}
```

- - -

💬 **What would the following lines of code output to the console?**
```js
console.log("0 || 1 = "+(0 || 1));
console.log("1 || 2 = "+(1 || 2));
console.log("0 && 1 = "+(0 && 1));
console.log("1 && 2 = "+(1 && 2));
```
> `#logic`

💡 Left to right process
```js
0 || 1 = 1  // 1 is true
1 || 2 = 1  // 1 is true
0 && 1 = 0  // 0 is false
1 && 2 = 2  // 1 is true then skip and check 2 which return 2
```

- - -

💬 **What will be the output when the following code is executed? Explain.**
```js
console.log(false == '0')
console.log(false === '0')
```
> `#equal`

💡 `==` is compare `value`, `===` is compare both `key` and `value`
```js
true
false
```

- - -

💬 **What is the output out of the following code? Explain your answer.**
```js
var a={},
    b={key:'b'},
    c={key:'c'};

a[b]=123;
a[c]=456;

console.log(a[b]);
```
> `#object`

💡 `b` and `c` get convert to `[object Object]`
```js
a[b]=123; // a["[object Object]"]=123;
a[c]=456; // a["[object Object]"]=456;
```
so output is
```js
456
```

- - -

💬 **What will the following code output to the console, Explain your answer.**
```js
console.log((function f(n){return ((n > 1) ? n * f(n-1) : n)})(10));
```
> `#closure`

💡 The code will output the value of 10 factorial (i.e., 10!, or 3,628,800).
```js
f(1): returns n, which is 1
f(2): returns 2 * f(1), which is 2
f(3): returns 3 * f(2), which is 6
f(4): returns 4 * f(3), which is 24
f(5): returns 5 * f(4), which is 120
f(6): returns 6 * f(5), which is 720
f(7): returns 7 * f(6), which is 5040
f(8): returns 8 * f(7), which is 40320
f(9): returns 9 * f(8), which is 362880
f(10): returns 10 * f(9), which is 3628800
```

- - -

💬 **Consider the code snippet below. What will the console output be and why?**
```js
(function(x) {
    return (function(y) {
        console.log(x);
    })(2)
})(1);
```
> `#closure`

💡 Inner function still has access to the outer function’s variables.
```
1
```

- - -

💬 **What will the following code output to the console and why:**
```js
var hero = {
    _name: 'John Doe',
    getSecretIdentity: function (){
        return this._name;
    }
};

var stoleSecretIdentity = hero.getSecretIdentity;

console.log(stoleSecretIdentity());
console.log(hero.getSecretIdentity());
```
**What is the issue with this code and how can it be fixed.**

> `#closure` `#function` `#call` `#bind`

💡 Stole `function` will miss their scope.
output
```js
undefined
John Doe
```
Use `bind` to fix.
```js
...
var stoleSecretIdentity = hero.getSecretIdentity.bind(hero);
...
```
Or temporary fix by `call` or `apply` each function with scope.
```js
...
console.log(stoleSecretIdentity.call(hero));
console.log(stoleSecretIdentity.apply(hero));
...
```
- - -

💬 **Create a function that, given a DOM Element on the page, will visit the element itself and all of its descendents (not just its immediate children). For each element visited, the function should pass that element to a provided callback function.**

The arguments to the function should be:

* a DOM element
* a callback function (that takes a DOM element as its argument)

> `#DOM` `#callback` `#traverse`

💡 Let's do it!
```js
function Traverse(p_element, p_callback) {
   p_callback(p_element);
   var list = p_element.children;
   for (var i = 0; i < list.length; i++) {
       Traverse(list[i],p_callback);  // recursive call
   }
}
```
- - -

📝 [5 Typical JavaScript Interview Exercises](http://www.sitepoint.com/5-typical-javascript-interview-exercises/)

- - -

💬 **Define a repeatify function on the String object. The function accepts an integer that specifies how many times the string has to be repeated. The function returns the string repeated the number of times specified. For example:**
```js
console.log('hello'.repeatify(3)); // Should print hellohellohello.
```
> `#method` `#inherit` `#prototype`

💡 Define `repeatify` from `String.prototype`
```js
String.prototype.repeatify = String.prototype.repeatify || function(times) {
   var str = '';

   for (var i = 0; i < times; i++) {
      str += this;
   }

   return str;
};
```

- - -

💬 **What’s the result of executing this code and why.**
```js
function test() {
   console.log(a);
   console.log(foo());
   
   var a = 1;
   function foo() {
      return 2;
   }
}
test();
```
> `#scope`

💡 `undefined` and `2` because what actually happen is
```js
function test() {
   var a;             // undefined
   function foo() {
      return 2;
   }

   console.log(a);
   console.log(foo());
   
   a = 1;
}

test();
```
- - -

📝 [https://blog.udemy.com/javascript-interview-questions/](JavaScript Interview Questions: A Not-So-Brief Overview To Help You Prepare)

- - -

💬 **What is JavaScript?**
> `#overview`

💡 JavaScript is a prototype-based, interpreted scripting language used in client-side web development to add interactivity to browser-based pages.

- - -

💬 **How do you add JavaScript to a web page?**
> `#overview`

💡 In `<head></head>` and `<body></body>`
```html
<head><script type="text/javascript" src="foo.js"></script>/head>
<body><script type="text/javascript">alert(foo);</script></body>
```
- - -

💬 **How do you add comments in JavaScript?**
> `#overview`

💡 There are two ways to add comments in JavaScript, as line comments and block comments.
```js
// one line
/* 
multi line
multi line
*/
```
- - -

💬 **Explain the difference between a local and a global variable, and how to declare each one.**
> `#overview` `#variable`

💡 Global variable can acces every where, Local variable can be use on in their scope
```js
// local
var _local = "foo";
global = "bar";
```

- - -

💬 **What are the different JavaScript data types?**
> `#type`

💡 undefined, null, String, Number, Boolean, Symbol (new in ECMAScript 6), Object (Not primitive)
📝 [7 data types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)
- - -

💬 **What is the difference between a value that is undefined and a value that is null?**
> `#undefined` `#null`

💡 A variable is undefined when it’s been declared without an assigned value.
```js
var foo
```
- - -

💬 **Explain the `this` keyword in JavaScript.**
> `#overview` `#this`

💡`this` used to reference the object in which the function is operating.

- - -

💬 **What is the HTML DOM?**
> `#overview`

💡 Once a web page loads, your browser generates something called a DOM, or Document Object Model, of the page. The DOM acts as as programming interface for HTML, which defines HTML properties, events, and methods. It also refers to HTML elements as objects.

![image](https://cloud.githubusercontent.com/assets/97060/9836599/e7b78410-5a49-11e5-8bee-fe58f4fac6a7.png)

📎 [DOM](http://www.w3schools.com/js/js_htmldom.asp)

- - -

📝 [JavaScript interview questions and answers](http://www.techrepublic.com/blog/software-engineer/javascript-interview-questions-and-answers/)

- - -

💬 **What is event bubbling?**
> `#overview` `#event`

💡 Event bubbling describes the behavior of events in child and parent nodes in the Document Object Model (DOM)

- - -

📝 [20 Must Know JavaScript Interview Q&As](http://www.skilledup.com/articles/20-must-know-javascript-interview-qa)

- - -

💬 **What is the  difference between `window.onload` and the jQuery `$(document).ready()` method?
> `#overview` `#event`

💡 
* The `window.onload method` occurs after all the page elements have loaded(HTML, CSS, images), which can result in a delay.
* The `$(document).ready()` method begins to run code as soon as the Document Object Model (DOM) is loaded, which should be faster and less prone to loading errors across different browsers.

- - -

📝 [Functional JavaScript interview question](http://bahmutov.calepin.co/functional-javascript-interview-question.html)

- - -
💬 **Fix this**
```js
['1', '2', '3'].map(parseFloat);
  //=> [1, 2, 3]
['1', '2', '3'].map(parseInt);
  //=> [ 1, NaN, NaN ]
```
> `#functional`

💡 It's failed because [parseInt](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt] function (takes string and radix)) , need to cover function.
```js
['1', '2', '3'].map(function (str) {
  return parseInt(str);
});
```

- - -

📝 [JavaScript Technical Interview Questions](https://www.interviewcake.com/javascript-interview-questions)

- - -
💬 **If we execute this Javascript, what will the browser's console show?**
```js
var text = 'outside';
function logIt(){
    console.log(text);
    var text = 'inside';
};
logIt();
```
> `#scope`

💡 It's `undefined` because what actually happen is
```js
var text = 'outside';
function logIt(){
    var text;           // undefined
    console.log(text);
    text = 'inside';
};
logIt();
```


- - -
# References
* http://bahmutov.calepin.co/functional-javascript-interview-question.html
* http://www.skilledup.com/articles/20-must-know-javascript-interview-qa
* https://www.interviewcake.com/javascript-interview-questions
* https://blog.udemy.com/javascript-interview-questions/
* http://www.toptal.com/javascript/interview-questions
* https://github.com/diegocard/js-questions/blob/master/questions%2FjQuery.md
* http://www.sitepoint.com/5-typical-javascript-interview-exercises/
* http://www.w3schools.com/js/js_quiz.asp
