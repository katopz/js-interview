What is a potential pitfall with using `typeof bar === "object"` to determine if bar is an object? How can this pitfall be avoided?
> typeof `null` is `object`
> typeof `Array` is `[object Array]`

```js
console.log((bar !== null) && (typeof bar === "object") && (toString.call(bar) !== "[object Array]"));
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
