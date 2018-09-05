In JavaScript, classes are based on JavaScript’s prototype-based inheritance mechanism. If two objects inherit properties from the same prototype object, then we say that they are instances of the same class.

```javascript
var Class = {
  aMethodInsidePrototype: function(){
    console.log(this.anObjectProperty);
  }
}

// One object from Class
var object1 = Object.create(Class);
object1.anObjectProperty = "A string for object1";
object1.aMethodInsidePrototype();

// Another object from Class
var object2 = Object.create(Class);
object2.anObjectProperty = "A string for object2";
object2.aMethodInsidePrototype();
```
Here we used `Object.create()` to create inherited objects from `Class`. But normally classes are created using constructor functions. In the above code, we need to explicitly assign individual object properties using dot operator. But constructor functions make object creation much easier by creating new objects and initializing the state of newly created objects.

## Constructor Function
A constructor is a function designed for the initialization of newly created objects. Constructors are invoked using the `new` keyword. The critical feature of constructor invocations is that the prototype property of the constructor is used as the prototype of the new object. This means that all objects created with the same constructor inherit from the same object and are therefore members of the same class.
```javascript
// Constructor function
function Person(name, age) {
  this.name = name;
  this.age = age;
}

// Create an object
var p1 = new Person("Joby", 32);
```
When using `new`, a new object is created from Constructor Function prototype and assigned to `this` before the constructor is called. This helps the constructor function to assign properties to the newly created object using `this`. Constructor invocation automatically creates a new object, invokes the constructor as a method of that object, and returns the new object.
