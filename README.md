## Design pattern with JavaScript

### Introduction
 <i>Design patterns are solutions to recurring problems guidelines on how to tackle certain problems.</i>
 
 Wikipedia describes them as

<blockquote>
In software engineering, a software design pattern is a general reusable solution to a commonly occurring problem within a given context in software design. It is not a finished design that can be transformed directly into source or machine code. It is a description or template for how to solve a problem that can be used in many different situations.
 </blockquote>
 
### Types of design patterns
- Creational
- Structural
- Behavioral

### Creational Design Patterns
&emsp; Creational patterns are focused towards how to instantiate an object or group of related objects.

<b>Wikipedia says</b> <br/>

<blockquote>
<p dir="auto">In software engineering, a software design pattern is a general reusable solution to a commonly occurring problem within a given context in software design. It is not a finished design that can be transformed directly into source or machine code. It is a description or template for how to solve a problem that can be used in many different situations.</p>
</blockquote>

### Simple Factory

Real world example

<blockquote>
<p dir="auto">Consider, you are building a house and you need doors. It would be a mess if every time you need a door, you put on your carpenter clothes and start making a door in your house. Instead you get it made from a factory.</p>
</blockquote>

In plain words

<blockquote>
<p dir="auto"> Simple factory simply generates an instance for client without exposing any instantiation logic to the client </p>
 </blockquote>
 
 #### Programmatic Example
 
First of all we have a door interface and the implementation

``` javascript
/*
Door

getWidth()
getHeight()

*/

class WoodenDoor {
  constructor(width, height){
    this.width = width
    this.height = height
  }

  getWidth(){
    return this.width
  }

  getHeight(){
    return this.height
  }
}
```

Then we have our door factory that makes the door and returns it

```javascript
const DoorFactory = {
  makeDoor : (width, height) => new WoodenDoor(width, height)
}
```

And then it can be used as

```javascript
const door = DoorFactory.makeDoor(100, 200)
console.log('Width:', door.getWidth())
console.log('Height:', door.getHeight())
```

#### When to Use?

When creating an object is not just a few assignments and involves some logic, it makes sense to put it in a dedicated factory instead of repeating the same code everywhere.

<br/>
<br/>
<br/>
<br/>
<i>Highly inspired from <b>javascript-design-patterns-for-humans</b> repo</i>
