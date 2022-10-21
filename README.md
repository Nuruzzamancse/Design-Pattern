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

## A design pattern's purpose reflects what it does:

-   **Creational patterns**: Concern the process of object creation
-   **Structural patterns**: Deal with the composition of objects or classes
-   **Behavioral patterns**: Characterize the ways in which classes or objects interact and distribute responsibility

## **Structural design pattern:**

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

## **Types of structural design patterns**

 **Adapter Pattern**:

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

```java

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

```java
   public class Hunter {
    public void hunt(Lion lion)
    {

    }
   }
   ```
 
Now let's say we have to add a `WildDog` in our game so that hunter can hunt that also. But we can't do that directly because dog has a different interface. To make it compatible for our hunter, we will have to create an adapter that is compatible

	    ```java
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

	    ```java
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
```java
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
```java
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
```java
	    $darkTheme = new DarkTheme();
	    
	    $about = new About($darkTheme);
	    $careers = new Careers($darkTheme);
	    
	    echo $about->getContent(); // "About page in Dark Black";
	    echo $careers->getContent(); // "Careers page in Dark Black";
```
**Usage examples:** The Bridge pattern is especially useful when supporting multiple types of database servers or working with several API providers of a certain kind (for example, cloud platforms, social networks, etc.)

## Composite

> **Composite**  is a structural design pattern that lets you compose objects into tree structures and then work with these structures as if
> they were individual objects.

**Example**

 1. 

> For example, imagine that you have two types of objects:  `Products` 
> and  `Boxes`. A  `Box`  can contain several  `Products`  as well as a
> number of smaller  `Boxes`. These little  `Boxes`  can also hold some 
> `Products`  or even smaller  `Boxes`, and so on.
> 
> Say you decide to create an ordering system that uses these classes.
> Orders could contain simple products without any wrapping, as well as
> boxes stuffed with products...and other boxes. How would you determine
> the total price of such an order?
> 
> The Composite pattern suggests that you work with  `Products`  and 
> `Boxes`  through a common interface which declares a method for
> calculating the total price.
> 
> How would this method work? For a product, it’d simply return the
> product’s price. For a box, it’d go over each item the box contains,
> ask its price and then return a total for this box. If one of these
> items were a smaller box, that box would also start going over its
> contents and so on, until the prices of all inner components were
> calculated. A box could even add some extra cost to the final price,
> such as packaging cost.

 2. 

> Armies of most countries are structured as hierarchies. An army
> consists of several divisions; a division is a set of brigades, and a
> brigade consists of platoons, which can be broken down into squads.
> Finally, a squad is a small group of real soldiers. Orders are given
> at the top of the hierarchy and passed down onto each level until
> every soldier knows what needs to be done.

 
3. 

> Every organization is composed of employees. Each of the employees has
> the same features i.e. has a salary, has some responsibilities, may or
> may not report to someone, may or may not have some subordinates etc.

**Programmatic Example**

Taking our employees example from above. Here we have different employee types
```java
	    interface Employee
	    {
	        public function __construct(string $name, float $salary);
	        public function getName(): string;
	        public function setSalary(float $salary);
	        public function getSalary(): float;
	        public function getRoles(): array;
	    }
	    
	    class Developer implements Employee
	    {
	        protected $salary;
	        protected $name;
	        protected $roles;
	        
	        public function __construct(string $name, float $salary)
	        {
	            $this->name = $name;
	            $this->salary = $salary;
	        }
	    
	        public function getName(): string
	        {
	            return $this->name;
	        }
	    
	        public function setSalary(float $salary)
	        {
	            $this->salary = $salary;
	        }
	    
	        public function getSalary(): float
	        {
	            return $this->salary;
	        }
	    
	        public function getRoles(): array
	        {
	            return $this->roles;
	        }
	    }
	    
	    class Designer implements Employee
	    {
	        protected $salary;
	        protected $name;
	        protected $roles;
	    
	        public function __construct(string $name, float $salary)
	        {
	            $this->name = $name;
	            $this->salary = $salary;
	        }
	    
	        public function getName(): string
	        {
	            return $this->name;
	        }
	    
	        public function setSalary(float $salary)
	        {
	            $this->salary = $salary;
	        }
	    
	        public function getSalary(): float
	        {
	            return $this->salary;
	        }
	    
	        public function getRoles(): array
	        {
	            return $this->roles;
	        }
	    }
```
Then we have an organization which consists of several different types of employees
```java
	    class Organization
	    {
	        protected $employees;
	    
	        public function addEmployee(Employee $employee)
	        {
	            $this->employees[] = $employee;
	        }
	    
	        public function getNetSalaries(): float
	        {
	            $netSalary = 0;
	    
	            foreach ($this->employees as $employee) {
	                $netSalary += $employee->getSalary();
	            }
	    
	            return $netSalary;
	        }
	    }
```
And then it can be used as
```java
	    // Prepare the employees
	    $john = new Developer('John Doe', 12000);
	    $jane = new Designer('Jane Doe', 15000);
	    
	    // Add them to organization
	    $organization = new Organization();
	    $organization->addEmployee($john);
	    $organization->addEmployee($jane);
	    
	    echo "Net salaries: " . $organization->getNetSalaries(); // Net Salaries: 27000
   ```
[Another Example](https://www.baeldung.com/java-composite-pattern)

## Decorator

> **Decorator**  is a structural design pattern that lets you attach new behaviors to objects by placing these objects inside special wrapper
> objects that contain the behaviors.

**Example**

 1. 

> Imagine that you’re working on a notification library which lets other
> programs notify their users about important events.
> 
> The initial version of the library was based on the  `Notifier`  class
> that had only a few fields, a constructor and a single  `send` 
> method. The method could accept a message argument from a client and
> send the message to a list of emails that were passed to the notifier
> via its constructor. A third-party app which acted as a client was
> supposed to create and configure the notifier object once, and then
> use it each time something important happened.

> At some point, you realize that users of the library expect more than
> just email notifications. Many of them would like to receive an SMS
> about critical issues. Others would like to be notified on Facebook
> and, of course, the corporate users would love to get Slack
> notifications.
2.
 > Imagine you run a car service shop offering multiple services. Now how do you calculate the bill to be charged? You pick one service and dynamically keep adding to it the prices for the provided services till you get the final cost. Here each type of service is a decorator.

**Programmatic Example**

Lets take coffee for example. First of all we have a simple coffee implementing the coffee interface
```java
	    interface Coffee
	    {
	        public function getCost();
	        public function getDescription();
	    }
	    
	    class SimpleCoffee implements Coffee
	    {
	        public function getCost()
	        {
	            return 10;
	        }
	    
	        public function getDescription()
	        {
	            return 'Simple coffee';
	        }
	    }
```
We want to make the code extensible to allow options to modify it if required. Lets make some add-ons (decorators)
```java
	    class MilkCoffee implements Coffee
	    {
	        protected $coffee;
	    
	        public function __construct(Coffee $coffee)
	        {
	            $this->coffee = $coffee;
	        }
	    
	        public function getCost()
	        {
	            return $this->coffee->getCost() + 2;
	        }
	    
	        public function getDescription()
	        {
	            return $this->coffee->getDescription() . ', milk';
	        }
	    }
	    
	    class WhipCoffee implements Coffee
	    {
	        protected $coffee;
	    
	        public function __construct(Coffee $coffee)
	        {
	            $this->coffee = $coffee;
	        }
	    
	        public function getCost()
	        {
	            return $this->coffee->getCost() + 5;
	        }
	    
	        public function getDescription()
	        {
	            return $this->coffee->getDescription() . ', whip';
	        }
	    }
	    
	    class VanillaCoffee implements Coffee
	    {
	        protected $coffee;
	    
	        public function __construct(Coffee $coffee)
	        {
	            $this->coffee = $coffee;
	        }
	    
	        public function getCost()
	        {
	            return $this->coffee->getCost() + 3;
	        }
	    
	        public function getDescription()
	        {
	            return $this->coffee->getDescription() . ', vanilla';
	        }
	    }
```
Lets make a coffee now
```java
	    $someCoffee = new SimpleCoffee();
	    echo $someCoffee->getCost(); // 10
	    echo $someCoffee->getDescription(); // Simple Coffee
	    
	    $someCoffee = new MilkCoffee($someCoffee);
	    echo $someCoffee->getCost(); // 12
	    echo $someCoffee->getDescription(); // Simple Coffee, milk
	    
	    $someCoffee = new WhipCoffee($someCoffee);
	    echo $someCoffee->getCost(); // 17
	    echo $someCoffee->getDescription(); // Simple Coffee, milk, whip
	    
	    $someCoffee = new VanillaCoffee($someCoffee);
	    echo $someCoffee->getCost(); // 20
	    echo $someCoffee->getDescription(); // Simple Coffee, milk, whip, vanilla
```

 **Relations with Other Patterns**

-   [Adapter](https://refactoring.guru/design-patterns/adapter)  changes the interface of an existing object, while  [Decorator](https://refactoring.guru/design-patterns/decorator)  enhances an object without changing its interface. In addition,  _Decorator_  supports recursive composition, which isn’t possible when you use  _Adapter_.
    
-   [Adapter](https://refactoring.guru/design-patterns/adapter)  provides a different interface to the wrapped object,  [Proxy](https://refactoring.guru/design-patterns/proxy)  provides it with the same interface, and  [Decorator](https://refactoring.guru/design-patterns/decorator)  provides it with an enhanced interface.
    
-   [Chain of Responsibility](https://refactoring.guru/design-patterns/chain-of-responsibility)  and  [Decorator](https://refactoring.guru/design-patterns/decorator)  have very similar class structures. Both patterns rely on recursive composition to pass the execution through a series of objects. However, there are several crucial differences.
    
    The  _CoR_  handlers can execute arbitrary operations independently of each other. They can also stop passing the request further at any point. On the other hand, various  _Decorators_  can extend the object’s behavior while keeping it consistent with the base interface. In addition, decorators aren’t allowed to break the flow of the request.
    
-   [Composite](https://refactoring.guru/design-patterns/composite)  and  [Decorator](https://refactoring.guru/design-patterns/decorator)  have similar structure diagrams since both rely on recursive composition to organize an open-ended number of objects.
    
    A  _Decorator_  is like a  _Composite_  but only has one child component. There’s another significant difference:  _Decorator_  adds additional responsibilities to the wrapped object, while  _Composite_  just “sums up” its children’s results.
    
    However, the patterns can also cooperate: you can use  _Decorator_  to extend the behavior of a specific object in the  _Composite_  tree.
    
-   Designs that make heavy use of  [Composite](https://refactoring.guru/design-patterns/composite)  and  [Decorator](https://refactoring.guru/design-patterns/decorator)  can often benefit from using  [Prototype](https://refactoring.guru/design-patterns/prototype). Applying the pattern lets you clone complex structures instead of re-constructing them from scratch.
    
-   [Decorator](https://refactoring.guru/design-patterns/decorator)  lets you change the skin of an object, while  [Strategy](https://refactoring.guru/design-patterns/strategy)  lets you change the guts.
    
-   [Decorator](https://refactoring.guru/design-patterns/decorator)  and  [Proxy](https://refactoring.guru/design-patterns/proxy)  have similar structures, but very different intents. Both patterns are built on the composition principle, where one object is supposed to delegate some of the work to another. The difference is that a  _Proxy_  usually manages the life cycle of its service object on its own, whereas the composition of  _Decorators_  is always controlled by the client.

## Facade

Real world example

> How do you turn on the computer? "Hit the power button" you say! That is what you believe because you are using a simple interface that computer provides on the outside, internally it has to do a lot of stuff to make it happen. This simple interface to the complex subsystem is a facade.

In plain words

> Facade pattern provides a simplified interface to a complex subsystem.

**Programmatic Example**

Taking our computer example from above. Here we have the computer class
```java
    class Computer
    {
        public function getElectricShock()
        {
            echo "Ouch!";
        }
    
        public function makeSound()
        {
            echo "Beep beep!";
        }
    
        public function showLoadingScreen()
        {
            echo "Loading..";
        }
    
        public function bam()
        {
            echo "Ready to be used!";
        }
    
        public function closeEverything()
        {
            echo "Bup bup bup buzzzz!";
        }
    
        public function sooth()
        {
            echo "Zzzzz";
        }
    
        public function pullCurrent()
        {
            echo "Haaah!";
        }
    }
```
Here we have the facade

```java
    class ComputerFacade
    {
        protected $computer;
    
        public function __construct(Computer $computer)
        {
            $this->computer = $computer;
        }
    
        public function turnOn()
        {
            $this->computer->getElectricShock();
            $this->computer->makeSound();
            $this->computer->showLoadingScreen();
            $this->computer->bam();
        }
    
        public function turnOff()
        {
            $this->computer->closeEverything();
            $this->computer->pullCurrent();
            $this->computer->sooth();
        }
    }
```

Now to use the facade

	    $computer = new ComputerFacade(new Computer());
	    $computer->turnOn(); // Ouch! Beep beep! Loading.. Ready to be used!
	    $computer->turnOff(); // Bup bup buzzz! Haah! Zzzzz

## Flyweight

Real world example

> Did you ever have fresh tea from some stall? They often make more than one cup that you demanded and save the rest for any other customer so to save the resources e.g. gas etc. Flyweight pattern is all about that i.e. sharing.

In plain words

> It is used to minimize memory usage or computational expenses by sharing as much as possible with similar objects.

**Programmatic example**

Translating our tea example from above. First of all we have tea types and tea maker

```java
// Anything that will be cached is flyweight.
// Types of tea here will be flyweights.

    class KarakTea { }
    
    // Acts as a factory and saves the tea class TeaMaker {
        protected $availableTea = [];
    
        public function make($preference)
        {
            if (empty($this->availableTea[$preference])) {
                $this->availableTea[$preference] = new KarakTea();
            }
    
            return $this->availableTea[$preference];
        } }
```

Then we have the  `TeaShop`  which takes orders and serves them
```java
    class TeaShop
    {
        protected $orders;
        protected $teaMaker;
    
        public function __construct(TeaMaker $teaMaker)
        {
            $this->teaMaker = $teaMaker;
        }
    
        public function takeOrder(string $teaType, int $table)
        {
            $this->orders[$table] = $this->teaMaker->make($teaType);
        }
    
        public function serve()
        {
            foreach ($this->orders as $table => $tea) {
                echo "Serving tea to table# " . $table;
            }
        }
    }
```

And it can be used as below

```java
	    $teaMaker = new TeaMaker();
	    $shop = new TeaShop($teaMaker);
	    
	    $shop->takeOrder('less sugar', 1);
	    $shop->takeOrder('more milk', 2);
	    $shop->takeOrder('without sugar', 5);
	    
	    $shop->serve();
	    // Serving tea to table# 1
	    // Serving tea to table# 2
	    // Serving tea to table# 5
```

## Proxy

Real world example

> Have you ever used an access card to go through a door? There are multiple options to open that door i.e. it can be opened either using access card or by pressing a button that bypasses the security. The door's main functionality is to open but there is a proxy added on top of it to add some functionality. Let me better explain it using the code example below.

In plain words

> Using the proxy pattern, a class represents the functionality of another class.

**Programmatic Example**

Taking our security door example from above. Firstly we have the door interface and an implementation of door
```java
	    public interface Door {
	        public void open();
	        public void close(); }
	    
	    class LabDoor implements Door {
	        public void open() {
	            System.out.println("Opening the lab door");
	        }
	    
	        public void close() {
	            System.out.println("Close the lab door");
	        } }
```
Then we have a proxy to secure any doors that we want
```java
	    Class SecuredDoor {
	    
	        protected Door door;
	    
	        public SecuredDoor(Door door) {
	            this.door = door;
	        }
	    
	        public void open(String password) {
	            if(authenticate(password)) {
	                door.open();
	            } else {
	                System.out.println("Access Denied!!!");
	            }
	        }
	    
	        public boolean authenticate(String password) {
	            return "Test".equals(password);
	        }
	    
	    
	        public void close() {
	            door.close();
	        }   
	    }
```

And here is how it can be used
```java
    class MainTest {
        public static void main(String[] args) {
            Door door = new SecuredDoor(new LabDoor());
            door.open("invalid");
    
            door.open("Test");
            door.close();
        }
    }
```
 **Relations with Other Patterns**

-   [Adapter](https://refactoring.guru/design-patterns/adapter)  provides a different interface to the wrapped object,  [Proxy](https://refactoring.guru/design-patterns/proxy)  provides it with the same interface, and  [Decorator](https://refactoring.guru/design-patterns/decorator)  provides it with an enhanced interface.
    
-   [Facade](https://refactoring.guru/design-patterns/facade)  is similar to  [Proxy](https://refactoring.guru/design-patterns/proxy)  in that both buffer a complex entity and initialize it on its own. Unlike  _Facade_,  _Proxy_  has the same interface as its service object, which makes them interchangeable.
    
-   [Decorator](https://refactoring.guru/design-patterns/decorator)  and  [Proxy](https://refactoring.guru/design-patterns/proxy)  have similar structures, but very different intents. Both patterns are built on the composition principle, where one object is supposed to delegate some of the work to another. The difference is that a  _Proxy_  usually manages the life cycle of its service object on its own, whereas the composition of  _Decorators_  is always controlled by the client.


<i>Highly inspired from <b>javascript-design-patterns-for-humans</b> repo</i>
