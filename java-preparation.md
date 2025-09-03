# Java Preparation
## OOPs Concepts(Object Oriented Programing)
### Encapsulation 
**Bind data with methods as one unit**
example getters and setters main data will define as private and controls data using public methods by getter and setters
### Inheritance
**One Object features can inherits to another.Inheritance `is a` relationship**
Using extends we inherits all functionality to other class.We can override these functionality on implemented class
using implement we can inheritance all methods in Interface to any class or Interface itself
### Polymorphism
**Single method behave multiple forms**

* **Runtime Polymorphism** Method overriding inheritance same method same parameters with different functionality

* **Compile time Polymorphism** Method Overloading save method different parameters
### Abstraction 
 Hide complexity using Abstraction class and Interfaces

**Relationships in JAVA Composition and Aggregation and inheritance**
* **Inheritance `is a` relationship**
* **Composition and Aggregations are `has a` relationships**
* **Composition** without child parent object will not exist independently 
* **Aggregation** both parent and child will exist independently
## Collections
* **Collection** is root interface.Which is implemented by every List,Set,Queue
* **Collections** is Utility class used for sort(), reverse(), min(), max(),

* In Collections 2 type of interfaces there
    *   List
        *   ArrayList
        *   LinkedList
        *   Vector --> Syncronized
        *   Stack  | LIFO | push(add element) | pop (Remove element last) |peek (Read last element will not remove)
    * Set
        *   HashSet |Unordered set
        *   TreeSet | Order Set(Natural Order) 
        *   LinkedHashSet | Insersion order
    * Queue
        * PriorityQueue | Ordered elements based on Priority By default item with lowest value will have heighest priority |
		* offer() -->Insert Elemet
		* pop read and remove from Top
		* peek only read not remove 
        * ArrayDeque | It will suport both FIFO and LIFO | ddFirst(), addLast(), removeFirst(), and removeLast()
    *   Map
        *   HashMap |No order
        *   TreeMap | natural order
        *   LinkedHashMap |insertion order of keys
        *   Hashtable | syncronized
        *   ConcurrentHashMap |sumcronozed | New implementation |It divides the map into segments or "buckets," and locks only the affected segment during write operations
  
| Class  |Best For   | Features  |
|---|---|---|
| ArrayList | Fast lookup | Resizable array, maintains insertion order |
| LinkedList | Fast insert/delete | Doubly linked list, ordered |  
|  HashSet | Fast set ops  | No duplicates, unordered  | 
|TreeSet|Sorted set|Uses Red-Black Tree
|LinkedHashSet|Insertion order
|HashMap|Fast key-value map|Unordered, allows null
|TreeMap|Sorted map|Keys are sorted

Java Serialization