# Classes in C#

### A type defined as a class is a reference type

#####  Initially when you declare a variable of a reference type, it's null until you explicitly create an instance of the class by using the new operator or assign it a compatible object

##### Example: 
##### //Declaring an object of type MyClass.
##### MyClass mc = new MyClass();

##### //Declaring another object of the same type, assigning it the value of the first object.
##### MyClass mc2 = mc;

##### When the object is created, sufficient memory is placed on the managed heap for that object, and the variable holds only a reference to the location of said object. Types on the managed heap require overhead both when they are allocated and when they are reclaimed by the automatic memory management functionality of the CLR, which is known as garbage collection. However, garbage collection is also highly optimized and in most scenarios, it does not create a performance issue.

##### You declare classes by using the class keyword followed by a unique identifier, like so:

##### //[access modifier] - [class] - [identifier]
##### public class Customer
##### {
#####    // Fields, properties, methods and events go here...
##### }

##### Keyword follows an access level
##### for example public, anyone can make instances of it

### Creating Objects

##### Classes and objects are different: classes define objects, objects are entities based on classes
##### create objects using "new", like so:
##### Customer object1 = new Customer();

##### You can reassign objects like other variables, like this:
##### Customer object3 = new Customer();
##### Customer object4 = object3;

##### Class inheritance: you can inherit from any other interface or class that is not defined as sealed, and other classes can inherit from your class and override class virtual methods.

##### Derivation: a class is declared by using a base class from which it inherits data and behavior
##### Example:
##### public class Manager : Employee
##### {
#####     // Employee fields, properties, methods and events are inherited
#####     // New Manager fields, properties, methods and events go here...
##### }

##### When a class declares a base class, it inherits all the members of the base class EXCEPT THE CONSTRUCTORS!
##### Put it all together and you get:

##### using System;

##### public class Person
##### {
#####     // Constructor that takes no arguments:
#####     public Person()
#####     {
#####         Name = "unknown";
#####     }

#####     // Constructor that takes one argument:
#####     public Person(string name)
#####     {
#####         Name = name;
#####     }

#####     // Auto-implemented readonly property:
#####     public string Name { get; }

#####     // Method that overrides the base class (System.Object) implementation.
#####     public override string ToString()
#####     {
#####         return Name;
#####     }
##### }
##### class TestPerson
##### {
#####     static void Main()
#####     {
#####         // Call the constructor that has no parameters.
#####         var person1 = new Person();
#####         Console.WriteLine(person1.Name);

#####         // Call the constructor that has one parameter.
#####         var person2 = new Person("Sarah Jones");
#####         Console.WriteLine(person2.Name);
#####         // Get the string representation of the person2 instance.
#####         Console.WriteLine(person2);

#####         Console.WriteLine("Press any key to exit.");
#####         Console.ReadKey();
#####     }
##### }
##### // Output:
##### // unknown
##### // Sarah Jones
##### // Sarah Jones

### Constructors

##### Whenever a class or struct is created, its constructor is called. 
##### Constructors set default values, limit instantiation, and write flexible readable code.
##### If you don't have a constructor, C# gives you a generic one that instantiates the object and sets member variables to the default values
##### Constructor syntax:

##### public class Person
##### {
#####    private string last;
#####    private string first;

#####    public Person(string lastName, string firstName)
#####    {
#####       last = lastName;
#####      first = firstName;
#####    }

#####    // Remaining implementation of Person class.
##### }

##### If you can make a  constructor in a  single statement, you can use an expression body definition.

##### Example:

##### public class Location
##### {
#####    private string locationName;

#####    public Location(string name) => Name = name;

#####    public string Name
#####    {
#####       get => locationName;
#####       set => locationName = value;
#####    }
##### }

##### Static constructors: Initialize static type and are paramaterless
##### Example:

##### public class Adult : Person
##### {
#####    private static int minimumAge;

#####    public Adult(string lastName, string firstName) : base(lastName, firstName)
#####    { }

#####    static Adult()
#####    {
#####       minimumAge = 18;
#####    }

#####    // Remaining implementation of Adult class.
##### }

### Properties

##### It's a member that provides aloose way to read, write, or compute values of a private field.

##### Properties are actually special methods called accessors.
##### Properties: expose a public way to get/set values while hiding implementation or verification code.
##### A GET property accessor is used to return the property value, and a SET property accessor is used to assign a new value.
##### The value keyword is used to define the value being assigned by the set accessor.
##### Backing Fields: Example:
##### using System;

##### class TimePeriod
##### {
#####    private double _seconds;

#####    public double Hours
#####    {
#####        get { return _seconds / 3600; }
#####        set {
#####           if (value < 0 || value > 24)
#####              throw new ArgumentOutOfRangeException(
 #####                   $"{nameof(value)} must be between 0 and 24.");

#####           _seconds = value * 3600;
#####        }
#####    }
##### }

##### class Program
##### {
#####    static void Main()
#####    {
#####        TimePeriod t = new TimePeriod();
#####        // The property assignment causes the 'set' accessor to be called.
#####        t.Hours = 24;

#####       // Retrieving the property causes the 'get' accessor to be called.
#####       Console.WriteLine($"Time in hours: {t.Hours}");
#####    }
##### }
##### // The example displays the following output:
##### //    Time in hours: 24

##### Expression body definitions:

##### using System;

##### public class Person
##### {
#####    private string _firstName;
#####    private string _lastName;

#####    public Person(string first, string last)
#####    {
#####       _firstName = first;
#####       _lastName = last;
#####    }

#####    public string Name => $"{_firstName} {_lastName}";
##### }

##### public class Example
##### {
#####    public static void Main()
#####    {
#####       var person = new Person("Magnus", "Hedlund");
#####       Console.WriteLine(person.Name);
#####    }
##### }
##### // The example displays the following output:
##### //      Magnus Hedlundusing System;

### Stack and Heap

##### Stack: keeps track of what's executing in code
##### Heap: keeps track of objects
##### A frame is how stacks keep track of what method is being called, can only get one after the next
##### A heap you can grab whatever object whenever
##### Value types: list found here: https://www.c-sharpcorner.com/article/C-Sharp-heaping-vs-stacking-in-net-part-i/
##### Pointer: Also called a reference
##### It's a chunk of space in memory that points to another space in memory

### Garbage Collection

##### It's an an automatic memory manager
##### Benefits: don't have to manually release memory, puts objects on heap neatly, memory safety(object can't use other object memory), reclaims objects not being used and clears memory for further use
##### CLR Memory concepts: found here: https://docs.microsoft.com/en-us/dotnet/standard/garbage-collection/fundamentals
##### 
