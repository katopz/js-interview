## [MDN-JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

📝 [Expressions and operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators)
- - -
####Logical operators####
```js
var a5 = "Cat" && "Dog";    // t && t returns Dog
var a7 = "Cat" && false;    // t && f returns false
var o5 = "Cat" || "Dog";    // t || t returns Cat
var o6 = false || "Cat";    // f || t returns Cat
var n3 = !"Cat"; // !t returns false
```
📝 https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Details_of_the_Object_Model
- - -
####Creating the hierarchy####
```js
function Employee() {
  this.name = "";
  this.dept = "general";
}
function Manager() {
  Employee.call(this);
  this.reports = [];
}
function Manager() {
  Employee.call(this);
  this.reports = [];
}
Manager.prototype = Object.create(Employee.prototype);

function WorkerBee() {
  Employee.call(this);
  this.projects = [];
}
WorkerBee.prototype = Object.create(Employee.prototype);
```
####Object properties####
```js
function Employee (name, dept) {
  this.name = name || "";
  this.dept = dept || "general";
}
function WorkerBee (projs) {
 this.projects = projs || [];
}
WorkerBee.prototype = new Employee;
function Engineer (mach) {
   this.dept = "engineering";
   this.machine = mach || "";
}
Engineer.prototype = new WorkerBee;
```
