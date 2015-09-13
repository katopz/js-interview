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
 
####Custom objects####
```js
var Person = function (firstName) {
  this.firstName = firstName;
};

Person.prototype.sayHello = function() {
  console.log("Hello, I'm " + this.firstName);
};

var person1 = new Person("Alice");
var person2 = new Person("Bob");

// call the Person sayHello method.
person1.sayHello(); // logs "Hello, I'm Alice"
person2.sayHello(); // logs "Hello, I'm Bob"

var helloFunction = person1.sayHello;
// logs "Hello, I'm undefined" (or fails
// with a TypeError in strict mode)
helloFunction();     

// logs "Hello, I'm Alice"
helloFunction.call(person1);
```
💡 Create empty `Student` by not call super for their `firstName` while construct
```js
// Define the Person constructor
var Person = function(firstName) {
  this.firstName = firstName;
};

// Add a couple of methods to Person.prototype
Person.prototype.walk = function(){
  console.log("I am walking!");
};

Person.prototype.sayHello = function(){
  console.log("Hello, I'm " + this.firstName);
};

// Define the Student constructor
function Student(firstName, subject) {
  // Call the parent constructor, making sure (using Function#call)
  // that "this" is set correctly during the call
  Person.call(this, firstName);

  // Initialize our Student-specific properties
  this.subject = subject;
};

// Create a Student.prototype object that inherits from Person.prototype.
// Note: A common error here is to use "new Person()" to create the
// Student.prototype. That's incorrect for several reasons, not least 
// that we don't have anything to give Person for the "firstName" 
// argument. The correct place to call Person is above, where we call 
// it from Student.
Student.prototype = Object.create(Person.prototype); // See note below

// Set the "constructor" property to refer to Student
Student.prototype.constructor = Student;

// Replace the "sayHello" method
Student.prototype.sayHello = function(){
  console.log("Hello, I'm " + this.firstName + ". I'm studying "
              + this.subject + ".");
};

// Add a "sayGoodBye" method
Student.prototype.sayGoodBye = function(){
  console.log("Goodbye!");
};

// Example usage:
var student1 = new Student("Janet", "Applied Physics");
student1.sayHello();   // "Hello, I'm Janet. I'm studying Applied Physics."
student1.walk();       // "I am walking!"
student1.sayGoodBye(); // "Goodbye!"

// Check that instanceof works correctly
console.log(student1 instanceof Person);  // true 
console.log(student1 instanceof Student); // true
```
💡Create `Object` without `Object.create` for old browser by [polyfill/shim](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create)
```js
function createObject(proto) {
    function ctor() { }
    ctor.prototype = proto;
    return new ctor();
}

// Usage:
Student.prototype = createObject(Person.prototype);

// Making sure that this points to the right thing regardless of how the object is instantiated can be difficult.
// However, there is a simple idiom to make this easier.
var Person = function(firstName) {
  if (this instanceof Person) {
    this.firstName = firstName;
  } else {
    return new Person(firstName);
  }
}
```
