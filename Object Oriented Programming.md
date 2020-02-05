# Object Oriented Programming

Before this Read: [Is JavaScript a true OOP?](https://medium.com/@andrea.chiarelli/is-javascript-a-true-oop-language-c87c5b48bdf0)



Object-oriented programming is a methodology used in many different programming languages that is based around data structures (called objects) that contain related data fields (properties) and methods (functions). It is important to note that simply using objects to organise a bunch of unrelated methods/properties is not object-oriented programming.

There are three main object-oriented concepts that are important to understand when you are programming: encapsulation, composition/inheritance, and polymorphism. We will go into further detail on these three concepts below.

### Encapsulation

Imagine you are building a tiny exploration game. The user playing the game has an avatar, and the avatar has various actions that the user can command the avatar to perform. Think about how you might begin coding the actions for the avatar. We are going to have to not only provide a way to perform actions in the code through methods (functions), but we also have to keep track of the avatar's state (where it is located, whether it is in motion, waiting for a command, maybe it has picked something up and has it in an inventory, etc). It is very useful to abstract a lot of internal logic of the avatar away from the rest of the program, so if the program wants the avatar to move it simply calls the `move()` method, or something similar. This concept of abstracting logic away from the program is called encapsulation.

If we make the avatar a class, we can expose only the information we need to to the outside program while maintaining a private internal state. Consider the following pseudo-code as a rough example of what that class might look like. The implementation of the functions is purposely left out.

```js
class Avatar {
    // Private properties
    energy;
    inventory;

    // Public methods
    move();
    speak();
    sleep();

    // Private methods
    determineState();
}
```

The above code shows a few private properties for the Avatar class. In a lot of cases you encapsulate properties in an object, and you only allow interaction with the object through methods. The public methods are exposed to the outside program, and thus to the user of the program. So the private methods/properties encapsulate the "state" of the avatar, while the public methods expose what the avatar can do, and each public method will modify the internal "state" of the avatar.

So why is encapsulation important? The point of encapsulation is to hide the implementation details from the rest of a program. This allows you to create an interface for the program to use, and allows you to modify what happens internally without changing the interface. As a software project grows in size it is incredibly important to have these kinds of abstractions, allowing you to change pieces of code knowing you won't affect the program as a whole.

### Composition/Inheritance

An object may contain other objects as properties, also known as instance variables. In the Avatar class above, maybe the "inventory" property is actually an instance of an Inventory class that looks like the following:

```js
class Inventory {
    // Private properties
    size;
    maxSize;
    items;

    // Public methods
    add();
    remove();
    size();
    sort();
    show();
}
```

Object composition is seen in this example, where Avatar has an instance of Inventory as a property. Using composition, we might create a large class that has multiple classes encapsulated as properties.

A parallel concept to composition is inheritance. Inheritance allows classes to be arranged in a heirarchy representing "is-a-type-of" relationships. In our example above, perhaps the Avatar class inherits from a Being class:

```js
class Being {
    // Public properties
    name;

    // Protected properties
    age;

    // Public methods
    move();
    speak();
    sleep();
}

class Avatar extends Being {
    // Private properties
    energy;
    inventory;

    // Public methods
    throw();
    fight();

    // Private methods
    determineState();
}
```

In this example Avatar **extends** Being, therefore an Avatar instance "is-a-type-of" Being. When a class inherits from (or extends) another class, it also inherits the functionality of that class. So in this case Avatar inherits the "name" and "age" properties as well as the "move", "speak", and "sleep" methods. Notice the comment `// Protected properties`. This is a special term for objects, indicating that those properties are exposed to children (objects that inherit) of the class. So while the external program would not have direct access to "name" and "age", the Avatar class can access those properties directly.

JavaScript does support inheritance, but not all programming languages do. In languages that do not support inheritance, you would accomplish what we did above by composing Avatar with its own "Being" property.

### Polymorphism

Do not be afraid of this "big word." Polymorphism is actually fairly easy to understand once you grasp the concept of inheritance. Polymorphism provides a way to define the exact same usage of a class or a parent class. In our example above, Avatar extends Being and as such inherits the `move()` and `sleep()` methods (among other things). Imagine now we are writing a function that involves calling the `move()` and `sleep()` method:

```js
function goToBed(being) {
    console.log(`${being.name} is tired`);
    being.move('bed');
    being.sleep();
}
```

Using polymorphism we could write a function that takes in anything that "is-a-type-of" Being, knowing that the interface for Being has the `name` property as well as the `move()` and `sleep()` methods. So if you pass an Avatar into the function it will still work. In fact, if you pass anything that inherits "is-a-type-of" Being it will work. This means that if you are evolving your game and all of a sudden you have different classes that extend Avatar (maybe a Mage, Ranger, Warrior, etc) and are thus a type-of Avatar, they will also be a type-of Being. So since they are a type-of Being they too can use your `goToBed()` function.



## Classes

Classes are a construct provided in many different languages including JavaScript. The syntax differs between the languages, but the concept is the same. You actually have already been using classes thus far in the course, though you haven't yet created one on your own. When you have used `document.querySelector` or anything in jQuery you are actually using classes. There are many classes built into JavaScript, and creating one is relatively simple. Consider the following code:

```js
class Circle {
    constructor(radius) {
        this.radius = radius;
    }
}
```

This is the most basic form of a class. Classes have a "constructor" function, which is called on when the class is instantiated. To instantiate the Circle class you would do the following:

```js
const myCircle = new Circle(5);
```

Now the `myCircle` variable will be a Circle with radius 5. Classes have `method` and `properties`. Methods are functions, properties are also known as "instance variables."

### The Constructor

The `constructor` method is a special method for creating and initializing an object created with a `class`. The constructor is used to take in Initialization arguments, and sometimes it must make a call to the super class using the `super` keyword. For example:

```js
class Shape {
    constructor(width, height) {
        this.width = width;
        this.height = height;
    }
}

class Circle extends Shape {
    constructor(radius) {
        super(2 * radius, 2 * radius);
    }
}
```

In the code above, Circle extends Shape, meaning Shape is the "super class" of Circle. The Circle constructor takes in a radius, but the Shape constructor takes in a width and height. So to compensate, the Circle class makes a `super` call and passes in the correct width/height (2 * radius). In the end, the Circle class will have a `this.width` and `this.height` equal to `2 * radius`.

### Methods and Properties

Methods (also known as "Prototype methods") are functions in a class. They have special access to the "this" and "super" keywords. consider the following code:

```js
class Shape {
    // Getter property
    get area() {
        return this.calculateArea();
    }

    constructor(width, height) {
        this.width = width;
        this.height = height;
    }

    resize(width, height) {
        this.width = width;
        this.height = height;
    }

    calculateArea() {
        return this.width * this.height;
    }
}

class Circle extends Shape {
    constructor(radius) {
        super(radius, radius);
    }

    resize(radius) {
        super.resize(radius, radius);
    }

    calculateArea() {
        const radius = this.width / 2;

        return Math.PI * radius * radius;
    }
}
```

In the code above there are two methods: `resize` and `calculateArea`. There are also three properties: `width`, `height`, and a "getter" property called area. The `get` syntax binds an object property to a function that will be called when the property is looked up. So if you write the following code you will log the area of the circle:

```js
const myCircle = new Circle(5);

console.log(myCircle.area);
```

The code above will end up looking up the `area`, thus calling the `area` getter function which in turn calls `this.calculateArea()`. It is important to note that the Circle class doesn't have the `area` property, but it does inherit it from Shape. So when `area` is looked up and `this.calculateArea()` is called, it will actually end up calling the `calculateArea()` method on the Circle class because the `claculateArea()` method on the Shape class is overridden.

The other method defined, `resize` is also overridden in the Circle class. The reason for this is that the width and height of a circle are equal, allowing the circle to take in only the radius, and then adjusting its size accordingly. In this case it uses the `super` keyword to call the `resize()` method on the Shape class. It is necessary in this case to use the `super` keyword because the Circle overrides the `resize()` method, so `super` indicates that the Circle wants to call the super class directly.

Similar to the `get` syntax there is a `set` syntax that allows a function to be called when an object's property is set. `get` and `set` are particularly useful when you want to know when a value is being accessed or changed.

### Static Methods

The `static` keyword defines a method on a class. Static methods are called without instantiating a class, and are not available on an instance of a class. Consider the following code:

```js
class Circle extends Shape {
    static diameter(circle) {
        return circle.width * 2;
    }

    constructor(radius) {
        super(2 * radius, 2 * radius);
    }

    resize(radius) {
        super.resize(2 * radius, 2 * radius);
    }

    calculateArea() {
        const radius = this.width / 2;

        return Math.PI * radius * radius;
    }
}
```

In the code above there is a `static diameter` method. This method can only be called on the Circle class itself, not on instances. So it would be called like this:

```js
const myCircle = new Circle(5);

console.log(Circle.diameter(myCircle));
```

Static methods do not have access to the instance `this` or `super` keyword.



## Inheritance

Inheritance is also known as "sub-classing". It is a construct available in JavaScript through the "extends" keyword. Inheritance is not available in all object-oriented programming languages, but most OOP languages do include it.

### extends

The `extends` keyword is used in class declarations to create a class that is a "child" of another class. Consider the following code:

```js
class Human {
    constructor(name) {
        this.name = name;
    }

    move() {
        console.log(this.name + ' moves.');
    }
}

class Baby extends Human {
    constructor(name) {
        super(name);
    }

    move() {
        console.log(this.name + ' crawls.');
    }
}

const baby = new Baby('Daisy');
baby.move(); // Daisy crawls.
```

In this example Baby extends Human, inheriting Human's properties and methods. Baby can override those methods as it sees fit. So in this case the `move()` method is overridden to be more specific, indicating that a baby "crawls." The `super` keyword is used to call to the parent class, and it can be used inside of methods as well as the `constructor`. The `this` keyword is available in every method, and it can access properties and methods defined by the class as well as those defined by parent classes.

You can have many levels of inheritance. In fact the DOM is a prime example of deep inheritance. Consider the following code:

```js
const myDiv = document.createElement('div');
```

Most people say `myDiv` is now an element, and that is correct because `myDiv` "is-a-type-of" Element. However `myDiv` is actually an HTMLDivElement that extends an HTMLElement, which extends Element, which extends Node, which extends EventTarget. So the hierarchy looks like this: `EventTarget > Node > Element > HTMLElement > HTMLDivElement`.







