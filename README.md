## Design pattern with JavaScript

### Introduction
 <i>Design patterns are solutions to recurring problems guidelines on how to tackle certain problems.</i>
 
 <blockquote>
 Design patterns represent the best practices used by experienced object-oriented software developers. Design patterns are solutions to general problems that software developers faced during software development. These solutions were obtained by trial and error by numerous software developers over quite a substantial period of time.
 </blockquote>
 
 Wikipedia describes them as

<blockquote>
In software engineering, a software design pattern is a general reusable solution to a commonly occurring problem within a given context in software design. It is not a finished design that can be transformed directly into source or machine code. It is a description or template for how to solve a problem that can be used in many different situations.
 </blockquote> 
 
### Types of design patterns
- Creational
- Structural
- Behavioral

### Creational Design Patterns
In plain words <br/>
<blockquote> Creational patterns are focused towards how to instantiate an object or group of related objects. </blockquote>

Wikipedia says <br/>

<blockquote>
<p dir="auto">
In software engineering, creational design patterns are design patterns that deal with object creation mechanisms, trying to create objects in a manner suitable to the situation. The basic form of object creation could result in design problems or added complexity to the design. Creational design patterns solve this problem by somehow controlling this object creation.
</p>
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

### Factory Method

Real world example

<blockquote>
Consider the case of a hiring manager. It is impossible for one person to interview for each of the positions. Based on the job opening, she has to decide and delegate the interview steps to different people.
</blockquote>

In plain words

<blockquote>
It provides a way to delegate the instantiation logic to child classes.
</blockquote>

<blockquote>
A Factory Pattern or Factory Method Pattern says that just define an interface or abstract class for creating an object but let the subclasses decide which class to instantiate. In other words, subclasses are responsible to create the instance of the class.
</blockquote>

The Factory Method Pattern is also known as Virtual Constructor.

Wikipedia says

<blockquote>
 In class-based programming, the factory method pattern is a creational pattern that uses factory methods to deal with the problem of creating objects without having to specify the exact class of the object that will be created. This is done by creating objects by calling a factory method—either specified in an interface and implemented by child classes, or implemented in a base class and optionally overridden by derived classes—rather than by calling a constructor.
</blockquote>

#### Programmatic Example

Taking our hiring manager example above. First of all we have an interviewer interface and some implementations for it

```javascript
/*
Interviewer interface

askQuestions()
*/

class Developer {
  askQuestions() {
    console.log('Asking about design patterns!')
  }
}

class CommunityExecutive {
  askQuestions() {
    console.log('Asking about community building')
  }
}
```

Now let us create our `HiringManager`

```javascript
class HiringManager {
        
    takeInterview() {
        const interviewer = this.makeInterviewer()
        interviewer.askQuestions()
    }
}
```
Now any child can extend it and provide the required interviewer

```javascript
class DevelopmentManager extends HiringManager {
    makeInterviewer() {
        return new Developer()
    }
}

class MarketingManager extends HiringManager {
    makeInterviewer() {
        return new CommunityExecutive()
    }
}
```
and then it can be used as

```javascript
const devManager = new DevelopmentManager()
devManager.takeInterview() // Output: Asking about design patterns

const marketingManager = new MarketingManager()
marketingManager.takeInterview() // Output: Asking about community building.
```

When to use?
<br/>

Useful when there is some generic processing in a class but the required sub-class is dynamically decided at runtime. Or putting it in other words, when the client doesn't know what exact sub-class it might need.

Advantage of Factory Design Pattern

<blockquote>
Factory Method Pattern allows the sub-classes to choose the type of objects to create.
It promotes the loose-coupling by eliminating the need to bind application-specific classes into the code. That means the code interacts solely with the resultant interface or abstract class, so that it will work with any classes that implement that interface or that extends that abstract class.
</blockquote>

<b>Usage of Factory Design Pattern</b>
- When a class doesn't know what sub-classes will be required to create
- When a class wants that its sub-classes specify the objects to be created.
- When the parent classes choose the creation of objects to its sub-classes.

<br/>
<br/>
<br/>
<br/>
<i>Highly inspired from <b>javascript-design-patterns-for-humans</b> repo</i>
