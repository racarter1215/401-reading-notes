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

