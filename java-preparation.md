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
        *   Vector
        *   Stack
    * Set
        *   HashSet
        *   TreeSet
        *   LinkedHashSet
    * Queue
        * PriorityQueue
        * ArrayDeque
    *   Map
        *   HashMap
        *   TreeMap
        *   LinkedHashMap
        *   Hashtable
        *   ConcurrentHashMap
  
| Class  |Best For   | Features  |
|---|---|---|
| ArrayList | Fast lookup | Resizable array, maintains insertion order |
| LinkedList | Fast insert/delete | Doubly linked list, ordered |  
|  HashSet | Fast set ops  | No duplicates, unordered  | 
|TreeSet|Sorted set|Uses Red-Black Tree
|LinkedHashSet|Insertion order
|HashMap|Fast key-value map|Unordered, allows null
|TreeMap|Sorted map|Keys are sorted