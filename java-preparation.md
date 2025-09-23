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


##   Why we need imutability
  1.    In Hashing we required immutable Keys
  2.    Immutable Objects are by default thread safe
  **how to create Immutable Object**
        1.    Declare class with final
        2.    All variables private and final 
        3.  No setters from Object cunstructor only we can modify data
        4.    If fields are mutable Objects we need to return copy of Object in reads so we Object will not change.
## Java Serialization
Converting java object to bite code is called Serialization
* To serialize a object we need to  implement Serializable interface.
  * Serializable interface is marker interface(No methods).JVM will identify Objects implemented by Serializable are serializable and it will allow to serialize
  * serializable interfaces have 2 default methods `writeObject` ,`readObject` are there.we can override these methods to customize the serialization.
  
        try (FileOutputStream fileOut = new FileOutputStream("person.ser");
			ObjectOutputStream out = new ObjectOutputStream(fileOut)) {
			out.writeObject(person);
			System.out.println("Serialized data is saved in person.ser");
		} catch (Exception e) {
			e.printStackTrace();
        } 

         try (FileInputStream fileIn = new FileInputStream("person.ser");
             ObjectInputStream in = new ObjectInputStream(fileIn)) {
            Person person = (Person) in.readObject();
            System.out.println("Deserialized Person:");
            System.out.println("Name: " + person.name);
            System.out.println("Age: " + person.age);
        } catch (Exception e) {
            e.printStackTrace();
        }
        
        private void writeObject(ObjectOutputStream oos) throws IOException {
        oos.defaultWriteObject();      // Write non-transient fields
        oos.writeInt(age + 5);         // Custom logic (e.g., obfuscate)
    }
      * Any field we dont want to serialize we have to use `transient` key word
      * Example for usecase password should not wite as bite stream or we need to encript and decript while doing serialization.In that cases we are overide the writeObject and readObject to customize default behavior.
*  If we need to more felxibility in serialization we need to use `Externalizable` interface.Need to overide `writeExternal`,`readExternal`

##  Concurency
 1. Extend Thread class and overide Run method
 2. Implement Runnable interface and implement run method.
   
    Thread t=new Thread(()->{
        System.out.println("Hellooo")
        });
    t.start();
 3. Exicutor services
 	Executor ex =ExicutorService.newFixedThreadPool(5);
 		 ex =ExicutorService.newCachedThreadPool() Reuses existing thread if no thread is empty creates new thred
 		 ex =ExicutorService.newSingleThreadExecutor() sinle thread
 		 ex =ExicutorService.newScheduledThreadPool()
      CompletionService<Result> ecs
         = new ExecutorCompletionService<Result>(ex);
         ecs.invokeAll(List of callables)
         
         ecs.take() will take first completed task

**Concurrent Collections**
	ConcurrentHashMap
	CopyOnWriteArrayList and CopyOnWriteArraySet
	BlockingQueue
**Atomic Variables**
	AtomicInteger, AtomicLong, AtomicBoolean, AtomicReference
Synchronizers: High-level synchronization aids:

**CountDownLatch**: Allows one or more threads to wait until a set of operations being performed in other threads completes.

**CyclicBarrier**: A synchronization aid that allows a set of threads to all wait for each other to reach a common "barrier point" before continuing. Can be reused.

**Semaphore**: A counting semaphore that controls access to a shared resource using a counter. It can limit the number of threads accessing a resource at once.

**Exchanger**: A synchronization point at which threads can pair up and swap objects.

**Locks (java.util.concurrent.locks)**: More flexible and powerful alternatives to the synchronized keyword.

**Lock interface**: Provides more control over locking, including tryLock() (non-blocking), timed lock attempts, and interruptible locking.

**ReentrantLock**: A reentrant mutual exclusion Lock that implements the Lock interface. A thread can acquire the same lock multiple times.

**ReadWriteLock**: Divides access into read and write locks. Multiple threads can acquire the read lock concurrently, but only one thread can acquire the write lock exclusively.


Difference between HashMap, ConcurrentHashMap, and Hashtable
 🔹 Difference between Iterator and ListIterator
 🔹 Difference between Comparator & Comparable
 🔹 How does Java manage memory (heap, stack, garbage collection)?
 🔹 Why is String immutable?
 🔹 final, finally, and finalize()
 🔹 What happens inside a HashMap during hash collision?
 🔹 Checked vs Unchecked exceptions — and when to use custom ones
 🔹 Java 8 Streams — performance vs readability
 🔹 Abstract class vs Interface
 🔹 Thread lifecycle
 🔹 Thread communication mechanisms
 🔹 Monitoring tools and their configuration in projects
 🔹 Usage & benefits of JpaRepository
 🔹 Singleton class
 🔹 @controller vs @RestController
 🔹 Configuring DB into the project 
 🔹 why is Java8 is more famous than other version like Java11, Java17

ACID principle
A- Automacy ->All operations in transsions should all success or all failed
C-Consistency ->Data should be consistency before the transation and after the transassion
I-Integredity ->If more then one transsions is running in DB it should be serialized and commit one by one
D- Durability ->After transsation is completed data should not lost even db creashed

## Java 8 Default Method Conflict Resolution Rules
* Rule 1: Class wins over interface
	class Parent {
       public void show() {
        System.out.println("Parent's show");
        }
    }

    interface A {
        default void show() { System.out.println("A's show"); }
    }

    class Child extends Parent implements A {}

    public class Test {
        public static void main(String[] args) {
            new Child().show(); // Parent's sh}
* Rule 2: More specific interface wins
    interface A {
        default void show() { System.out.println("A's show"); }
    }

    interface B extends A {
        default void show() { System.out.println("B's show"); }
    }
    class MyClass implements B {}
    public class Test {
        public static void main(String[] args) {
            new MyClass().show(); // B's show
        }
    }

* Rule 3: Explicit override required (diamond problem)
	* If two unrelated interfaces provide the same default method, the implementing class must  override it and explicitly choose.
    interface A {
        default void show() { System.out.println("A's show"); }
    }

    interface B {
        default void show() { System.out.println("B's show"); }
    }

    class MyClass implements A, B {
        @Override
        public void show() {
            // Custom choice
            A.super.show(); 
            // Or B.super.show();
        }
    }

    public class Test {
        public static void main(String[] args) {
            new MyClass().show(); // A's show (if A.super.show() chosen)
        }
    }

## Java Method Overloading Resolution Rules
  1. Exact Match Preferred
        void test(int x) { System.out.println("int"); }
        void test(long x) { System.out.println("long"); }

    test(5); // int → exact match

* Widening > Boxing > Varargs
    Order of preference when resolving:
    Widening primitive conversion
    Boxing/unboxing
    Varargs

    void show(long x) { System.out.println("widening"); }
void show(Integer x) { System.out.println("boxing"); }
void show(int... x) { System.out.println("varargs"); }

show(10); // widening → long

3. Widening Beats Boxing
Allowed widenings:

byte → short → int → long → float → double

char → int → long → float → double

❌ Not allowed:

Narrowing (e.g., double → int).
void print(long x) { System.out.println("long"); }
void print(Integer x) { System.out.println("Integer"); }

print(5); // long (widening)

4. Boxing Beats Varargs

void display(Integer x) { System.out.println("Integer"); }
void display(int... x) { System.out.println("varargs"); }

display(5); // Integer (boxing)

5. Ambiguity Leads to Compilation Error
void fun(Integer x, int y) {}
void fun(int x, Integer y) {}

fun(10, 10); // ❌ ambiguous → compiler error
6. Null Argument Resolution

If null is passed, the most specific applicable overload is chosen.

If multiple reference types are equally valid, ambiguity occurs.

void test(String s) { System.out.println("String"); }
void test(Object o) { System.out.println("Object"); }

test(null); // String (more specific than Object)


void test(String s) {}
void test(StringBuilder sb) {}

test(null); // ❌ ambiguous → compiler error

7. Autoboxing and Widening Together

Java does not allow both at the same time.

Example: int → Integer → long is invalid.
void check(Long x) { System.out.println("Long"); }

check(5); // ❌ compile error (int → Integer → Long not allowed)
