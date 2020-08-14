# Hash Tables

### Hash: the result of some algorithm taking an incoming string and converting it into a value that could be used for either security or some other purpose.

### Bucket: what is contained in each index of the array of the hashtable. Each index is a bucket

### Collision: what happens when more than one key gets hashed to the same location of the hashtable

##### HashTables: data structure that utilize key value pairs. This means every Node and Bucket has a a key and a value

##### HashTables are a thing so that they can store the key into a data structure, and quickly retrieve the value. They do this through a hash

##### Hash codes: turns a key into an integer. They should never have randomness to them and the same key should always produce the same hash code.

##### Example of creating a hash:
Key = "Cat"
Value = "Josie"

67 + 97 + 116 = 280

280 * 599 = 69648

69648 % 1024 = 16

Key gets placed in index of 16. 

##### Collisions are solved by changing the initial state of the buckets. 

##### Instead of starting them all as null we can initialize a LinkedList in each


### Hashing Implementation:
##### An element is converted into an integer by using a hash function. This element can be used as an index to store the original element, which falls into the hash table.
##### The element is stored in the hash table where it can be quickly retrieved using hashed key.

##### hash = hashfunc(key)
##### index = hash % array_size

##### Hash Function: any function that can be used to map a data set of an arbitrary size to a data set of a fixed size, which falls into the hash table. 
###### The values returned by a hash function are called hash values, hash codes, hash sums, or simply hashes.

##### Big 3 for good hasing mechanism: easy to compute, uniform distribution, and less collision
##### Link to hash table examples:
https://www.hackerearth.com/practice/data-structures/hash-tables/basics-of-hash-tables/tutorial/

### Wikipedia Link: https://en.wikipedia.org/wiki/Hash_table
