# Classes
A class is a blueprint for creating new objects with the same set of properties and methods.

A constructor function is included in the class, but it is only called once, on the creation of the object. 

class Rectangle {
    constructor (width, height) {
        this.width = width;
        this.height = height;
    }
    getArea () {
        return this.width * this.height;
    }
}
let elRectanle = new Rectangle(8, 5);
console.log(elRectangle.width); // => 8
console.log(elRectancle.getArea()); // => 40

The constructor function typicallys sets object properties using user input.

In this example, getArea() is a method of the class, which can be called on any given rectangle to calculate area

## Getters and Setters
Getters and setters are methods that behave like properties. For example 
```
class Square {
    constructor (side) {
        this.side = side;
    }
    get area () {
        return Math.pow(this.side, 2);
    }
    set area(area) {
        this.side = Math.sqrt(area);
    }
}
let square1 = new Square(4);
console.log(square1.area) // => 16
square1.area = 36;
console.log(square1.side); // => 6
conosle.log(square1.area); // => 36
```

## Static methods
A static method exists independent of any instances of the class, and is usually a type of utility that is related to the class, but not a method of any particular instance.

class Square {
    constructor (side) {
        this.side = side;
    }
    get area () {
        return Math.pow(this.side, 2);
    }
    set area(area) {
        this.side = Math.sqrt(area);
    }
    static isSideWholeNumber (square) {
        if (square.side % 1 === 0) {
            return true;
        }
        else {
            return false;
        }
    }
}

## Inheritance
If a class "extends" another class, it inherits its parent classes properties and methods, and typically adds more. 

The super keyword calls the parent class's constructor function, and is used in the child classes constructor function. That way, the child class does not have to repeat the parent's logic.

## Polymorphism
Polymorphism is simply redeclaring a method of a parent class within a child class. It is common to  use 
```
childMethod() {
    super.parentMethod();
    // more specific added functionality
}
```
to make the child method include and expand on the parent's logic.

## Singletons 
A singleton is an instance of a class that can only have one instance. If the constructor is called multiple times, it will return the same object.  This can be implemented many ways in JS. Here is an example using a settings object:
```
class Settings {
    constructor() {
        if (Settings.instance instanceof Settings) { 
            return Settings.instance; // Use previous settings instance if it has already been called
        }

        this.settingsObject = {
            background: 'mauve',
            version: Math.floor(Math.random() * 3000)
        }

        Object.freeze(this.settingsObject); // prevent the settingsObject from being changed
        Object.freeze(this); // prevent the Settings instance from being changed
        Settings.instance = this; // store the first instance on the class. 
    }

    get(key) {
        return this.settingsObject[key];
    }
}
```

## Binding to html
This class creates a binding to an HTML element ( ul or ol )that is passed into the constructor. The instance then maintains a list of items that can be modified by the add, clear, and update methods.  The static method, which does not refer to ```this``` is used as a utility to keep all the fiddly bits of dom manipulation contained in the class.

```
export class ListBinding {
  constructor(element) {
    this.listItems = [];
    this.element = element;
  }

  static makeLi(item) {
    const li = document.createElement("li");
    li.textContent = item;
    return li;
  }

  add(item) {
    this.listItems.push(item);
    this.update();
  }

  clear() {
    this.listItems = [];
    this.update();
  }

  update() {
    this.element.innerHTML = null;
    for (const item of this.listItems) {
      this.element.appendChild(ListBinding.makeLi(item));
    }
  }
}
```

