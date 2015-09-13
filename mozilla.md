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
####Property inheritance revisited####
💡 Maker every inherit name "Unknow"
```js
function Employee () {
  this.dept = "general";
}
Employee.prototype.name = "";

function WorkerBee () {
  this.projects = [];
}
WorkerBee.prototype = new Employee;

var amy = new WorkerBee;

Employee.prototype.name = "Unknown";
```
**Determining instance relationships**
```js
var f = new Foo();
var isTrue = (f instanceof Foo);
```
- - - 
📝 [Introduction to Object-Oriented JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript)
- - - 
####Terminology####
**Namespace**
* A container which lets developers bundle all functionality under a unique, application-specific name.

**Class**
* Defines the object's characteristics. A class is a template definition of an object's properties and methods.

**Object**
* An instance of a class.

**Property**
* An object characteristic, such as color.

**Method**
* An object capability, such as walk. It is a subroutine or function associated with a class.

**Constructor**
* A method called at the moment an object is instantiated. It usually has the same name as the class containing it.

**Inheritance**
* A class can inherit characteristics from another class.

**Encapsulation**
* A method of bundling the data and methods that use the data.

**Abstraction**
* The conjunction of an object's complex inheritance, methods, and properties must adequately reflect a reality model.

**Polymorphism**
* Poly means "many" and morphism means "forms". Different classes might define the same method or property.
