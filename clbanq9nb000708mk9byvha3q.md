# Object-oriented programming 
(OOP) With Javascript

## What is Object-Oriented programming (OOP)?

*   Object-oriented programming (OOP) is a programming paradigm (<mark>Style of code, “how” we write and organize code</mark>) based on the concept of objects.
    
*   We use objects to model (describe) the real-world (your phone) or abstract features (RAM, ROM). For example, we might use an object to model a person, a car, or a building.
    
*   Objects may contain data (properties) and code (methods). By using objects, we pack data and the corresponding behavior into one block.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670040280339/82052ab4-46fc-4b62-85b7-45353cd6f328.png align="left")

*   In OOP, objects are **self-contained pieces of code** that can be used to create and manage separate, related sets of functionality.
    
*   Objects are the fundamental building blocks of applications, and they interact with one another to achieve a particular goal or result.
    
*   Interactions happen through a public interface (API): methods that the code
    
    Outside of the object can access and use to communicate with the object.
    
*   OOP was developed with the goal of **organizing code**, to make it **more flexible** and **easier to maintain.**
    
    ## Classes And Instances
    
    In the real world, you often have many objects of the same kind. For example, your car is just one of many cars in the world. Using object-oriented terminology, we say that your car object is an instance (in the glossary) of the class of objects known as cars. Cars have some state (current gear, four wheels) and behavior (change gears, brakes) in common. However, each car's state is independent of and can be different from that of other cars.
    
    When building cars, manufacturers take advantage of the fact that cars share characteristics, building many cars from the same blueprint. It would be very inefficient to produce a new blueprint for every individual car manufactured.
    
    In object-oriented software, it's also possible to have many objects of the same kind that share characteristics: rectangles, employee records, video clips, and so on. Like the car manufacturers, you can take advantage of the fact that objects of the same kind are similar and you can create a blueprint for those objects. A software blueprint for objects is called a class (in the glossary)
    
    `Definition: A class is a blueprint that defines the variables and the methods common to all objects of a certain kind.`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670046755220/e4751d4b-f0a0-479a-ad64-a8903f7f56b7.png align="left")
    

## The 4 fundamental OOP principles

1.  Abstraction
    
2.  Encapsulation
    
3.  Inheritance
    
4.  Polymorphism
    
    ### Abstraction:
    
    Abstraction is a fundamental concept in object-oriented programming (OOP) that refers to the idea of focusing on the essential characteristics of an object in order to reduce complexity and increase efficiency.
    
    An example of abstraction in the real world might be a person using a smartphone. The person is not concerned with the internal workings of the phone, such as how the processor communicates with the memory and other components. Instead, they are only concerned with the essential features of the phone, such as making calls, sending texts, and using apps. By abstracting away the underlying complexity of the phone, the user is able to interact with it more easily and efficiently.
    
    `Abstraction: Ignoring or hiding details that don’t matter, allowing us to`
    
    `get an overview perspective of the thing we’re implementing, instead of`
    
    `messing with details that don’t really matter to our implementation.`
    
    ### Encapsulation :
    
    Encapsulation is another fundamental concept in OOP that refers to the idea of combining related data and functionality into a single unit, known as an object. An example of encapsulation in the real world might be a car. A car is a self-contained unit that has its own engine, transmission, and other components that work together to enable it to function. The driver does not need to know how each of these components works individually; in order to drive the car; they only need to know how to operate the car as a whole. By encapsulating the various parts of a car into a single unit, it is easier to use and maintain.
    
    Encapsulation can be achieved by declaring all the variables in the class as private and writing public methods in the class to set and get the values of the variables.
    
    **Prevents external code from accidentally manipulating internal properties/state**
    
    **Allows to change internal implementation without the risk of breaking external code.**
    
    `Encapsulation: Keeping properties and methods private inside the class, so they are not accessible from outside the class. Some methods can be exposed as a public interface (API).`
    
    ### Inheritance
    
    Inheritance is another concept in OOP that refers to the ability of one class to inherit the characteristics and behavior of another class. An example of inheritance in the real world might be the relationship between a parent and a child. A child inherits certain physical and behavioral characteristics from their parents, such as eye color, height, and the tendency to laugh at certain jokes. Additionally, a child also inherits certain societal and cultural values and norms from their parents, such as the importance of education, the value of hard work, and the importance of family. In this way, inheritance allows for the continuation and development of certain traits and behaviors from one generation to the next.
    
    `Inheritance: Making all properties and methods of a certain class available to a child class, forming a hierarchical relationship between classes. This allows us to reuse common logic and to model real-world relationships.`
    

### Polymorphism

Polymorphism is a concept in OOP that refers to the ability of an object to take on multiple forms. An example of polymorphism in the real world might be the behavior of animals. Different animals can exhibit similar behaviors, such as eating, sleeping, and reproducing, but they may do so in different ways. For instance, a lion and a tiger may both hunt for food, but the lion may do so by stalking its prey and pouncing on it; while the tiger may do so by stealthily creeping up on its prey and attacking it from behind. Despite the differences in their hunting behavior, both the lion and the tiger are exhibiting the same general behavior of obtaining food. This is an example of polymorphism, where an object (in this case, an animal) can exhibit different behavior based on the specific situation or context.

`Polymorphism: A child class can overwrite a method it inherited from a parent class.`

## OOP IN JAVASCRIPT: PROTOTYPES

In JavaScript, an object is a collection of properties, and a property is an association between a name (or key) and a value. A property's value can be a function, in which case the property is known as a method.

Here is an example of an object in JavaScript that represents a car:

```javascript
// Example 1
let car = {
make = "Ford",
model = "Mustang",
year = 1969,
color = "Red",
passengers = 4,
convertible = true,
mileage = 0,
started = false,

start: function() {
this.started = true;
},
stop: function(){
this.started = false;
},
drive: function(){
if(this.started) {
console.log("Vroom,vroom!");
this.mileage += 10;
}
else{
console.log("You need to start the engine first");
}
}
};
```

In this example, the car object has several properties, such as make, model, and year, which store data about the car. It also has several methods, such as start, stop, and drive, which contain code that manipulates the data in the object.

To access the properties and methods of an object in JavaScript, you can use the dot notation, like this:

```javascript
car.make; // returns "Ford"
car.model; // returns "Mustang"
car.start(); // start the car's engine
car.drive(); // logs "Vroom,vroom! and increment the car's mileage by 10"
```

### Let's take a look at prototypes in JS to get a better understanding of the process:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670066502662/YlDnUyDX2.png align="left")

In JavaScript, prototypal inheritance is a way for one object to inherit properties and methods from another object. This is different from classical inheritance, which is a way for one class (a blueprint for objects) to inherit from another class.

`Prototypal inheritance works by creating a link, or "prototype" between the two objects so that the child object can access the properties and methods of the parent object.`

In JavaScript, objects can have a special type of property called a **prototype**. A prototype is an object that is used as a **blueprint** for creating other objects. When you create an object, JavaScript automatically sets the prototype of the object to be the prototype of the object's constructor function.

For example, let's say you have a constructor function called Car that creates objects representing cars. The Car function has a prototype property that is an object containing properties and methods that should be available to all objects created using the Car constructor. Here is an example of how you could define the Car function and its prototype:

```javascript
// Example 2
function Car(make, model, year){
this.make = make;
this.model = model;
this.year = year;
this.mileage = 0;
this.started = false;
}

Car.prototype.start = function(){
this.started = true;
}
Car.prototype.stop = function(){
this.started = false;
}
Car.prototype.drive= = function(){
if(this.started){
console.log("Vroom,vroom!");
this.mileage += 10;
}
else {
console.log("You need to start the engine first");
}
};
```

Now, whenever you create a new Car object using the new keyword, the object will have access to the start, stop, and drive methods defined in the Car prototype. For example:

```javascript
let myCar = new Car("Ford", "Mustang", 1969);
myCar.start(); // starts the car's engine
myCar.stop(); // logs "Vroom,vroom!" and increment the car's mileage by 10
```

### There are several ways to implement prototypal inheritance in JavaScript. Here are three common methods:

1.  **Using the new keyword** and a constructor function: In JavaScript, a constructor function is a special type of function that is used to create new objects; As shown in the previous example.
    
2.  **Using the Object.create() method**: the Object.create() method can be used to create a new object that has a specified object as its prototype. This method is available in modern browsers, and can also be polyfilled (emulated) in older browsers that do not support it.
    
    ```javascript
    //Refer example 1 we are here creating object for example 1
    let myCar = Object.create(Car);
    myCar.year(2021);
    myCar.start();
    myCar.stop();
    ```
    
    In this example, the myCar object is created using the Object.create() method, which takes the 'car' object as its prototype. This means that myCar has access to the properties and methods of 'car', but can also have its own properties and methods that are unique to it.
    
    To access the properties and methods of the prototype, you can use the \_\_proto\_\_ property or the Object.getPrototypeOf() method. For example:
    
    ```javascript
    console.log(myCar.__proto__ === car) // logs true
    console.log(Object.getPropertyOf(myCar) === car); // logs true
    ```
    
    3.  The **Object.setPrototypeOf()** method can be used to set the prototype of an existing object to be a specified object. This allows you to dynamically change the prototype of an object and add or modify its inherited properties and methods.
        
        ```javascript
        // Refer Example 1
        let myCar = {
        year: 2022,
        };
        // Set the prototype of myCar to be car
        Object.setPrototypeOf(myCar, car);
        // Now myCar has access to the properties and methods of car
        myCar.start(); // starts the car's engine
        myCar.drive(); // logs "Vroom,vroom!"
        ```
        
        In this example, the myCar object is created without a prototype. Then, the Object.setPrototypeOf() method is used to set the prototype of myCar to be the car object. This allows myCar to inherit the properties and methods of car, such as the start, stop, and drive methods.
        
        `Note that this method is only available in modern browsers, and may need to be polyfilled (emulated) in older browsers that do not support it.`
        
    
    ### Prototype chain
    
    In JavaScript, the prototype chain is a mechanism that allows objects to inherit properties and methods from other objects. This is an important concept in JavaScript, as it allows for the implementation of inheritance, which is a fundamental characteristic of object-oriented programming languages.
    
    ```javascript
     Object
      |
      |
      |
      |
    Prototype
      |
      |
      |
      |
    Concrete Object
    ```
    

In this diagram, the Object at the top of the chain is the parent or prototype of the Prototype object, which in turn is the parent or prototype of the Concrete Object. The Concrete Object is an instance of the Prototype, which in turn is an instance of the Object.

When we call a method or access a property on the Concrete Object, the JavaScript engine first looks for that method or property on the Concrete Object itself. If it is not found, the engine then looks for the method or property on the Prototype object. If it is still not found, the engine continues to search up the prototype chain until it reaches the Object at the top of the chain. If the method or property is not found on the Object, then the search ends and a undefined value is returned.

This mechanism allows objects to inherit methods and properties from their parent objects, and allows for the creation of hierarchical object-oriented designs.

**Here is a simple example of how the prototype chain can be used in a real-world scenario:**

Suppose we have a Car object that represents a generic car. This Car object has properties and methods that are common to all cars, such as the make and model properties for the car's manufacturer and model name, and the startEngine method for starting the car's engine.

```javascript
const Car = {
make: 'unknown',
model: 'unknown',
startEngine: function() {
// Code for starting the engine
 }
```

Next, we can create a Ford object that represents a specific type of car - a Ford. This Ford object can inherit the properties and methods of the Car object by setting the Ford object's prototype to the Car object.

```javascript
const Ford = {
__proto__: Car
};
```

Now, when we call a method or access a property on a Ford object, the JavaScript engine will first look for that method or property on the Ford object itself. If it is not found, the engine will then look for the method or property on the Car object, which is the Ford object's prototype. If the method or property is still not found, the engine will continue to search up the prototype chain until it reaches the Object at the top of the chain.

This allows us to create Ford objects that have all the properties and methods of the Car object, as well as any additional properties and methods that we define on the Ford object itself.

```javascript
const mustang = {
make: 'Ford',
model: 'Mustang',
__proto__: Ford
};
mustang.make; // 'Ford'
mustang.make; // 'Ford'
mustang.startEngine(); // Starts the engine
```

In this example, the mustang object is an instance of the Ford object, which in turn is an instance of the Car object. This allows the mustang object to inherit the make and model properties and the startEngine method from the Car object, as well as the Ford object's own properties and methods.

### Inheritance between classes

In JavaScript, classes can inherit from other classes using the extends keyword. This allows a class to inherit the properties and methods of another class, and create a hierarchical class structure.

Here is an example of inheritance between classes in JavaScript

```javascript
class Animal {
constructor(name) {
this.name = name;
 }
eat() {
 console.log(`${this.name} is eating.`);
}
}
class Cat extends Animal {
constructor(name) {
super(name);
}
meow() {
console.log(`${this.name} says meow!`);
}
}

const garfield = new Cat('Garfield');
garfield.eat(); // Garfield is eating.
garfield.meow(); // Garfield says meow!
```

In this example, the Animal class is the parent class and the Cat class is the child class that inherits from Animal. The Cat class uses the extends keyword to specify that it is a child class of Animal, and the super() method to call the Animal class's constructor and inherit its properties.

The Cat class also has its own meow() method, which is not present in the Animal class. This allows the Cat class to inherit the name property and the eat() method from the Animal class, as well as have its own unique methods.

When we create a new Cat object, such as garfield, it inherits the properties and methods of the Animal class, as well as the Cat class's own methods. This allows us to call the eat() and meow() methods on the garfield object.

> I hope you enjoyed reading this blog post. If you would like to stay updated on my progress and engage in discussions with me on a variety of topics, you can follow me on Twitter. I regularly post updates on my work and thoughts on various topics, and I am always open to chatting with others on the platform.