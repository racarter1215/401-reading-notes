# Enumumeration

### An interface, which allows different data structures to expose a common traversal API.

##### IEnumerator: defines the basic low-level protocol by which elements
in a collection are traversed—or enumerated—in a forward-only manner. 

##### Example:
##### public interface IEnumerator
##### {
#####  bool MoveNext();
#####  object Current { get; }
#####  void Reset();
##### }

##### Collections do not usually implement enumerators; instead, they provide enumerators, via the interface IEnumerable
##### Example:
##### public interface IEnumerable
##### {
#####  IEnumerator GetEnumerator();
##### }

##### IEnumerator and IEnumerable: nearly always implemented in conjunction with their extended generic versions
##### public interface IEnumerator<T> : IEnumerator, IDisposable
##### {
#####  T Current { get; }
##### }
##### public interface IEnumerable<T> : IEnumerable
##### {
#####  IEnumerator<T> GetEnumerator();
##### }
  
##### When to Use the Nongeneric Interfaces: see page 305

#####  Iterator: a feature that assists in writing collections like a foreach statement assists in consuming collections. 
#####  Example of writing a class that implements IEnumerator directly:
##### public class MyIntList : IEnumerable
##### {
#####  int[] data = { 1, 2, 3 };
#####  public IEnumerator GetEnumerator()
##### Collections
##### Enumeration | 307
#####  {
#####  return new Enumerator (this);
#####  }
#####  class Enumerator : IEnumerator // Define an inner class
#####  { // for the enumerator.
#####  MyIntList collection;
##### int currentIndex = -1;
#####  public Enumerator (MyIntList collection)
#####  {
#####  this.collection = collection;
#####  }
#####  public object Current
#####  {
#####  get
#####  {
#####  if (currentIndex == -1)
#####  throw new InvalidOperationException ("Enumeration not started!");
#####  if (currentIndex == collection.data.Length)
#####  throw new InvalidOperationException ("Past end of list!");
#####  return collection.data [currentIndex];
#####  }
#####  }
#####  public bool MoveNext()
#####  {
#####  if (currentIndex >= collection.data.Length - 1) return false;
#####  return ++currentIndex < collection.data.Length;
#####  }
#####  public void Reset() { currentIndex = -1; }
#####  }
##### }
##### Implement

##### IEnumerable<T> (and IEnumerable): Provides some functions
##### ICollection<T> (and ICollection): Provides more functions 
##### IList <T>/IDictionary <K,V>: Provide all functions
  
##### Linked List
##### LinkedList<T> implements IEnumerable<T> and ICollection<T> but not IList<T>
##### Queue<T> and Queue are FIFO data structures that can Enqueue and Dequeue 
  
##### Stack<T> and Stack are LIFO data structures that can Push and Pop

### Enums
##### They are value type that lets you specify groups of numeric constants
##### Enum Conversion example:
##### int i = (int) BorderSide.Left;
##### BorderSide side = (BorderSide) i;
##### bool leftOrRight = (int) side <= 2;

##### Flags: These should always be applied to an enum type when its members are combinable.

### Collections
##### Example of Collection using foreach
##### var salmons = new List<string>();
##### salmons.Add("chinook");
##### salmons.Add("coho");
##### salmons.Add("pink");
##### salmons.Add("sockeye");

##### // Iterate through the list.
##### foreach (var salmon in salmons)
##### {
#####     Console.Write(salmon + " ");
##### }
##### // Output: chinook coho pink sockeye

### Enumeration Types

##### Example of enum types:
##### enum Season
##### {
#####     Spring,
#####     Summer,
#####     Autumn,
#####     Winter
##### }

##### Examples of enums with Flags
##### [Flags]
##### public enum Days
##### {
#####     None      = 0b_0000_0000,  // 0
#####     Monday    = 0b_0000_0001,  // 1
#####     Tuesday   = 0b_0000_0010,  // 2
#####     Wednesday = 0b_0000_0100,  // 4
#####     Thursday  = 0b_0000_1000,  // 8
#####     Friday    = 0b_0001_0000,  // 16
#####     Saturday  = 0b_0010_0000,  // 32
#####     Sunday    = 0b_0100_0000,  // 64
#####     Weekend   = Saturday | Sunday
##### }

##### public class FlagsEnumExample
##### {
#####     public static void Main()
#####     {
#####         Days meetingDays = Days.Monday | Days.Wednesday | Days.Friday;
#####         Console.WriteLine(meetingDays);
#####         // Output:
#####         // Monday, Wednesday, Friday

#####         Days workingFromHomeDays = Days.Thursday | Days.Friday;
#####         Console.WriteLine($"Join a meeting by phone on {meetingDays & workingFromHomeDays}");
#####         // Output:
#####         // Join a meeting by phone on Friday

#####         bool isMeetingOnTuesday = (meetingDays & Days.Tuesday) == Days.Tuesday;
#####         Console.WriteLine($"Is there a meeting on Tuesday: {isMeetingOnTuesday}");
#####         // Output:
#####         // Is there a meeting on Tuesday: False

#####         var a = (Days)37;
#####         Console.WriteLine(a);
#####         // Output:
#####         // Monday, Wednesday, Saturday
#####     }
##### }







