## Design pattern

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

**Structural design pattern:**

> Structural design pattern is a blueprint of how different objects and
> classes are combined together to form a bigger structure for achieving
> multiple goals altogether.

> The patterns in structural designs show how unique pieces of a system
> can be combined together in an extensible and flexible manner.
  

> So, with the help of a structural design pattern we can target and
> change specific parts of the structure without changing the entire
> structure.

**In plain words**

> Structural design patterns are mostly concerned with object
> composition or in other words how the entities can use each other

 **Types of structural design patterns** <br/>
  
 **- Adapter Pattern**:

> 	 The adapter pattern helps in converting the interface of a class
> into another interface depending on the client's requirements.


> In Adapter pattern, we convert the interface of a class into another interface that the clients expect. Adapter lets classes work together that couldn’t otherwise because of incompatible interfaces.


> The Adapter pattern, as the name implies, adapts one interface to another. It acts as a bridge between two unrelated, and sometimes even completely incompatible interfaces, similar to how a scanner acts as a bridge between a paper and a computer.

**Real world example**

 1. Example 3

> Consider that you have some pictures in your memory card and you need to transfer them to your computer. In order to transfer them you need some kind of adapter that is compatible with your computer ports so that you can attach memory card to your computer. In this case card reader is an adapter. 
2. Example 2
> Another example would be the famous power adapter; a three legged plug
> can't be connected to a two pronged outlet, it needs to use a power
> adapter that makes it compatible with the two pronged outlet.
3. Example 3
> Yet another example would be a translator translating words spoken by
> one person to another
4. Example 4 
> A computer can't store a paper as a PDF document, but a scanner, which
> combines the functionalities of both, can scan it and allow the
> computer to store it.

**Programmatic Example**

Consider a game where there is a hunter and he hunts lions.

First we have an interface  `Lion`  that all types of lions have to implement

```javascript
  public interface Lion {
   public void roar();
  }

  public class AfricanLion implements Lion{
   @Override
   public void roar() {
    System.out.println("African Lion roars");
   }	
  }

  public class AsianLion implements Lion {
   @Override
   public void roar() {
    System.out.println("Asian Lion roars");
   }
  }
```

And hunter expects any implementation of  `Lion`  interface to hunt.

```javascript
  public class Hunter {
   public void hunt(Lion lion)
   {

   }
  }
```

Now let's say we have to add a `WildDog` in our game so that hunter can hunt that also. But we can't do that directly because dog has a different interface. To make it compatible for our hunter, we will have to create an adapter that is compatible

```javascript
   // This needs to be added to the game
   public class WildDog {
    public void bark() {
     System.out.println("Wild dog bark");
    }
   }

   // Adapter around wild dog to make it compatible with our game
   public class WildDogAdapter implements Lion {

    protected WildDog wildDog;

    public WildDogAdapter(WildDog wildDog) {
     this.wildDog = wildDog;
    }

    @Override
    public void roar() {
     wildDog.bark();
    }
   }
```
And now the  `WildDog`  can be used in our game using  `WildDogAdapter`.

```javascript
   public class Main {

    public Main() {
     WildDog wildDog = new WildDog();
     WildDogAdapter wildDogAdapter =  new WildDogAdapter(wildDog);

     Hunter hunter = new Hunter();
     hunter.hunt(wildDogAdapter);
    }
   }
```

## Bridge Pattern

> **Bridge** is a structural design pattern that divides business logic or huge class into separate class hierarchies that can be developed independently. 

> These hierarchies are then connected to each other via object composition, forming a bridge-like structure. This pattern is also known as the **Handle-Body Design Pattern**.

**Real world example**

> Consider you have a website with different pages and you are supposed to allow the user to change the theme. What would you do? Create multiple copies of each of the pages for each of the themes or would you just create separate theme and load them based on the user's preferences? Bridge pattern allows you to do the second i.e.

[![With and without the bridge pattern](https://cloud.githubusercontent.com/assets/11269635/23065293/33b7aea0-f515-11e6-983f-98823c9845ee.png)](https://cloud.githubusercontent.com/assets/11269635/23065293/33b7aea0-f515-11e6-983f-98823c9845ee.png)
**Programmatic Example**

Translating our WebPage example from above. Here we have the  `WebPage`  hierarchy

```javascript
   interface WebPage
   {
       public function __construct(Theme $theme);
       public function getContent();
   }

   class About implements WebPage
   {
       protected $theme;

       public function __construct(Theme $theme)
       {
           $this->theme = $theme;
       }

       public function getContent()
       {
           return "About page in " . $this->theme->getColor();
       }
   }

   class Careers implements WebPage
   {
       protected $theme;

       public function __construct(Theme $theme)
       {
           $this->theme = $theme;
       }

       public function getContent()
       {
           return "Careers page in " . $this->theme->getColor();
       }
   }
```

And the separate theme hierarchy

```javascript
   interface Theme
   {
       public function getColor();
   }

   class DarkTheme implements Theme
   {
       public function getColor()
       {
           return 'Dark Black';
       }
   }
   class LightTheme implements Theme
   {
       public function getColor()
       {
           return 'Off white';
       }
   }
   class AquaTheme implements Theme
   {
       public function getColor()
       {
           return 'Light blue';
       }
   }
```

And both the hierarchies

```javascript
   $darkTheme = new DarkTheme();

   $about = new About($darkTheme);
   $careers = new Careers($darkTheme);

   echo $about->getContent(); // "About page in Dark Black";
   echo $careers->getContent(); // "Careers page in Dark Black";
```

**Usage examples:** The Bridge pattern is especially useful when supporting multiple types of database servers or working with several API providers of a certain kind (for example, cloud platforms, social networks, etc.)


<i>Highly inspired from <b>javascript-design-patterns-for-humans</b> repo</i>
