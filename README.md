
**Data Structure and Software Design**
@ Prof. Chris Murphy from Penn
```Java
@ Note by Puran Zhang
```

This course focuses on data structures, software design, and advanced Java. The
course starts off with an introduction to data structures and the basics of the analysis of
algorithms. Important data structures covered include arrays, lists, stacks, queues,
trees, hash tables, sets, maps, and graphs. The course also focuses on software design
and advanced Java topics such as software architecture, code understandability, and
multithreading

[Syllabus](https://d18ky98rnyall9.cloudfront.net/aq17msSNQrqte5rEjcK6cw_f5286be666614367aa13b0163c5847f1_CIT-594---Syllabus---Summer-2021_v3.pdf?Expires=1620950400&Signature=OloHjhnosryoGgU2f7rU5B9hlofbTX0zwdsnwUApP5VGSvuMogvJdKi-DhACNCxJ6aym-QN2ou81rwy~5B~wfxKBDCtGproGvwtui5gP6rEXJWC1XwJvWfxRGShmJBbfv8YgcmMwk7evzF50pc0brTpCNRIabwV-fUM5VFvcdtM_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A)
* Concept Comprehension 14 Quizzes: 14%
* Individual programming 8 assignments: 58.5%
* Group Project: 15%
* Final Exam: 12.5%

## M1: Into. Data Structure

Module Learning Objectives
- Understand the importance of data structures in developing high quality software.
- Describe the implementation of key functionality in the Java ArrayList class.
- Use Java Generics to develop more generalized data structures.

Module Glossary
- ArrayList: A data type similar to an array but allowing for a dynamically resizable array implementation. The overhead is the number of array positions that are currently unused.
- Generics: A feature of Java that allows the programmer to define a class as using a “generic” type for some/all parameters. This allows different instances of the class to be instantiated with different data types. The programmer using the class declares the specific type for the instance when creating it

Key Concepts & Examples
- Data structures affect both internal and external software quality. How the data is organized can affect
    - Efficiency of the program (speed/memory usage)
    - Ease of understanding the program (for maintenance/testing/etc)
- An ArrayList
    - Wraps an underlying array of elements and provides common functionality for using and manipulating it
    - Allows us to add more elements beyond the capacity of the underlying array by creating a new one and copying over all elements
- ArrayLists provide common functionality such as
    - Adding/Removing elements
    - Fetching an element from a certain location
    - Determining whether the ArrayList contains a certain value
- Generics are a feature of Java that allows different instances of the class to be instantiated with different data types.
    - Unlike using Object as the parameter type, this ensures that the declared data type in instantiation remains the same for the created instance.
    - For example, if an ArrayList is instantiated as an ```Java ArrayList<String>```, then only elements of type String can be added to the ArrayList.

### Software Quality

**Perspectives on Software Quality:**
- **Transcendental 先验**：can be recognized but not defined or measured.
- **User**: satisfies end-user's needs
- **Manufacturer**: conforms to specification (regradless of what users want)
- **product**: based onn ninternal characteristics of the code itself
- **value-based**: depends on what someone is willing to pay for it

**Definition of Software Quality:**
- **External**: executable program running on hardware in some environment
    - **Functionality**: adheeres to specifications
    - **Reliability**: maintains leveel of performance
    - **Usability**: ease with which useeers can perform tasks
    - **Efficiency**: minimal use of resources
    - **Security**: confidentiality, integrity, availability
- **internal**: code as human-readble text
    - **Stability**: modifyig one part has limited effect on others
    - **Changeability**: ease with which code can be changed
    - **Analyzability**: readability and undeerstandability
    - **Testability**: controllability, obseervability
    - **Reusability**: can be used in a varity of applications

### Java/JUnit Refresher
Read Data Structures & Algorithms, 6th ed, Chapter 1: Java Primer, Chapter 2: Object-Oriented Design

Practice: The rainfall method below is intended to determine the average amount of rainfall for each month as indicated by the input array. However, in this case, negative values should be ignored, so the method should only determine the average of the non-negative values, i.e. those that are greater than or equal to 0.

```Java
public class Main {
  
  public static double rainfall(double[] readings) {
    // implement this method!
    //Select non-negative
    int len=0;
    //average
    double total=0;
    for(int i=0; i<readings.length; i++){
      if (readings[i]>=0){
        total += readings[i];
        len++;
      }
    }
    return total/len;
  }
  
  public static void main(String[] args) {
    double[] readings = { 84, 73.5, 22.1, 0.0, 11.1, -5.2, 4.8, -19.4, 33.1, 0.0, 15.3, 22.1};
    System.out.println(rainfall(readings));   
  }
}
```

**Software Development Lifestyle (SDLC)**
- **Requirement**: what are we going to build?
- **Design**: how are we going to build it?
- **Implementation**: let's build it!
- **Testing**: did we build it right?
- **Maintenance**: how do we make it better?

**Software Testing Basics**
- Types of testing
    - **Unit test**: test small piece of code; intuition is that bugs will be easier to find/fix
    - **Integration test**: test several units based on expected interactions
    - **System test**: test entire system (via UI)
    - **Acceptance test**: end-users determine whether the system meets their needs
- Test case: consist of input, Expected output/behavior, Actual output/Behavior
    - Result = pass if expected = actual; Result = fail if expected = actual
    - Steps
- Fault: static defect in code; difference between actual implementation and theoretically correct implementation
- Soundness: expected output is correct wrt specification
    - False negative: expected = actual because test is unsound
    - False positive: 

**Writing JUnit Tests**

```Java
public class MaxTracker{
    protected int max = 0;
    protected int count = 0;
    
    public boolean update(int value){
        count++;
        
        if(count ==1 || value > max){
            max =value;
            return true;        
        }
        else return false;    
    }
    public int getMax(){return max;}
    public int getCount(){return count;}
}


public class MaxTrackerTest{
    protected MaxTracker mt; //object to be tested
    
    @before //Invoke before each test case
    public void SetUp(){
        mt = new MaxTracker();//Create a new object for each test
    }
    
    @Test // Run as a test case
    public void thisIsABadTest(){
        mt.update(20); // Don't assume the method you are testing works correctly
        
        assetTrue(mt.update(50));// Check side effects (change of state) in addition to return value
    }
    
    @Test
    public void testGreaterThanMaxNotFirstUpdate(){
        // initialize the state directly if possible
        mt.max=44;
        mt.count=4;// Directly set these
        
        // invoke the method to be tested
        boolean returnValue = mt.update(50); // only call the method you are testing once
        
        // check output
        assertTrue("incorrect return valu when input is greater than curreent max", returnValue);
        // Use a meaningful error message
        
        //check side effects
        int expected = 50;
        int actual = mt.getMax();//Check the object's state
        assertEquals("max not correctly updated when input is greater than current max", expected, actual);
        //Expected goes first
        
        expected = 5;
        actual = mt.getCount();
        assertEquals("count not correcctly updated wen input is greater than current max", expected, actual);
    }
}
```

**Summary: writing good tests**

* Create a new object in the @Before method
* Do **not** rely on side effects of the method you are testing (or of other methods)
* Directly manipulate its fields to put it into the state in which you want to test
* Check side effects, not just return valyes
* Use meaningful error messages

### Implement Data Structrues

**ArrayList in Java**

* The java.util.ArrayList class can store a collection of elements and allows for common operations suchas:
    * Adding elements
    * Removing elements
    * Access elements by their ID/position
    * Searching for elements
* Programmers can use an ArrayList without having to know how it works
* The ArrayList wraps an underlying array of data

```Java
public class StringArrayList{
    protected String[] data;
    protected int size=0;
    
    public StringArrayList(int capacity){
        data = new String[capacity];
    }
    
    public void add(String value){
        if(size == data.length){
            increaseCapacity();
        }
        data[size++]=value;
    }  
    
    private void increaseCapacity(){
        String[] newData = new String[data.length * 2];
        System.arraycopy(data, 0, newData, 0, size);
        data = newData;
    }
    
    public void add(int index, String value){
        if (index<0 || index >= size){
            throw new IndexOutOfBoundsException();
        }
        if (size == data.length){
            increaseCapacity();
        }
        System.arraycopy(data, index, data, index + 1, size - index);
        data[index] = value;
        size++;
    }
}
```
* An ArrayListwraps a underlying array of elements and provides common functionality for using and manipulating it.
* ArrayLists allow us to add more elements beyond the capacity of the underlying array by creating a new one and copying over all elements.
* Always use the java.util.ArrayList calss and not your own implementation.


**Generic Data Structure**

* Programmer who **writes** the class definition creates a "generic" class that includes parameters for diffeerent tupes that it uses.
* Programmer who **uses** the class and creats an instance of it indicates the specific types for that instance.

Benefits of using Java Generics
- allow the user of a class to specify the datatype that the class will use internally
- allow for the creation of generalized classes that do not require casting of method return values.
    - We could create a generalized class that uses Objects, but callers would need to cast method return values; using Generics, the caller does not have to do any casting.
- reduce the amount of duplicated (or very similar) code in a system.

```Java
public class ObjectArrayList{
    protected Object[] data;
    
    public void add(Object value){
        ...
    }
    
    public Object get(int inndex){
        ...
    }
}
```

```Java
public class GenericArrayList<E>{ // type parameter <E> for elemnet, <T> for general case

    protected E[] data; // E[]: an array of elements
    ...
}

public void add(E value){// call E to specify the parameeter of the add method
    ...
}
    
public E get(int index){// See E: replace it with the type that was specified when an object of this class was created
    ...
}

public GenericArrayList(int capacity){
    data = (E[])new Object[capacity];
}

GenericArrayList<String> strings = new GenericArrayList<>();
strings.add("banana");
String s = string.get(0);

GenericArrayList<Dog> dogs = new GenericArrayList<>();
dogs.add(new Dog("Pearl")); // add dog object
Dog d = dogs.get(0);

```

define a class to hold a pair of values using Java Generics

```Java
public class Pair<T> {
	
	private T one, two;
	public Pair(T t1, T t2) {
		one = t1;
		two = t2;
	}
	public T getOne() { return one; }
	public T getTwo() { return two; }
	
}
```

### Project 1

## M2: LinkedLists

Module Learning Objectives
- Describe the limitations of ArrayLists with respect to common operations we may want to perform on a collection of values.
- Identify the component parts of a LinkedList.
- Modify a LinkedList by adding or removing one or more values from the front, middle, or rear.
- Access an element of a LinkedList by its index.
- Determine whether a LinkedList contains a specified value.
- Apply LinkedLists to solve a problem in Java.
- Implement Stacks and Queues in the Java programming language

Module Glossary
- **ArrayList**: A data type similar to an array but allowing for a dynamically resizable array implementation. The overhead is the number of array positions that are currently unused.
- **Head**: A Node object that is typically used to denote the first Node in a LinkedList instance.
- **IndexOutOfBoundsException**: A runtime error that indicates a attempt to reach an index that does not exist in the object of the given data type.
- **LinkedList**: A class that uses Node objects to store the list elements. Nodes also include pointers/links to other nodes in the list since they are not stored in contiguous memory addresses.
- **Link/Pointer**: A variable whose value is the memory address of another value. In a LinkedList, its value is typically the location of another Node in the list.
- **Node**: A supporting object that forms the building block for a LinkedList. It typically contains fields that store the list element as well as a pointer or link to other Nodes.
- **Tail**: A Node object that is typically used to denote the last Node in a LinkedList instance.
- **Stack**: A data structure that works like a LinkedList but only has two allowed modifying operations; push which adds an element to the top of the stack, and pop which removes the element at the top of the stack.
- **Queue**: A data structure that works like a LinkedList but only has two allowed modifying operations; add which adds an element to the rear of the queue, and remove which removed the element at the front of the queue.
- **FIFO (First In, First Out) Data Structure**: A data structure where the first element added is the first one removed. In other words, elements are removed from in the same order that they are added. A Queue is an example of a FIFO data structure.
- **LIFO (Last In, Last Out) Data Structure**: A data structure where the last element added is the first one removed. In other words, elements are removed in the reverse order in which they were added. A Stack is an example of a LIFO data structure.
- **Java Collections Framework**: A java-provided collection of implementations for common objects, data structures, and interfaces. Examples include the LinkedList class, ArrayList class, and the List interface.

Key Concepts & Examples

**ArrayList Limitations:** ArrayLists have a number of limitations which include:
- Having a fixed number of elements in the underlying array.
- Inserting a value between two others can be slow
- Searching for a value can be slow

**LinkedList:** A data structure that is used to store a list of elements as a collection of Nodes that are linked together. These Nodes are stored in non-contiguous memory addresses. 

**Adding Elements to a LinkedList:** We can add elements to a LinkedList in 3 ways.
1. At the head of the list – using LinkedList.addFirst(E element)
2. At the tail of the list – using LinkedList.addLast(E element)
3. At a specified index of the list – using LinkedList.add(int index, E element)

**Removing Elements from a LinkedList:** We can remove elements from a LinkedList in 3 ways:

1. From the head of the list – using LinkedList.removeFirst()
2. From the tail of the list – using LinkedList.removeLast()
3. From a specified index of the list – using LinkedList.remove(int index)

**Searching for Elements in a LinkedList:** We can check if a LinkedList contains a specified element/value – using LinkedList.contains(E value)

**Retrieving Elements from a LinkedList:** We can access the element at a specified index of
the LinkedList (without removing it from the list) – using LinkedList.get(int index)

**Stack:** A data structure similar to a LinkedList in which elements elements must be inserted
and removed from only one end (either the top/head or the bottom/tail). This ensures that the
Stack is a LIFO (Last In, First Out) data structure in which elements are removed in the
reverse order that they are added to the Stack

**Stack Operations:** The Stack data structure has 4 main operations:
1. Stack.push(E value) - This method places the specified element at the top of the Stack.
2. Stack.pop() - This method returns and removes the element of the top of the Stack.
3. Stack.peek() - This method returns (but does not remove) the element at the top of the Stack.
4. Stack.empty() - This method tests if the Stack is empty.

**Queue:** A data structure similar to a LinkedList in which elements must be added to one
end, and removed only from the opposite end. This ensures that the Queue is a FIFO (First
In, First Out) data structure in which elements are removed in the same order as they are
added to the Queue.

**Queue Operations:** The Queue data structure has 4 main operations:
1. Queue.add(E value) - This method places the specified element at the rear of the Queue.
2. Queue.remove() - This method returns and removes the element at the front of the Queue.
3. Queue.peek() - This method returns (but does not remove) the element at the front of the Queue.
4. Queue.empty() - This method tests if the Queue is empty

Read Chapter 3: Fundamental Data Structures of our course textbook Data Structures & Algorithms; pay particular attention to Section 3.2: Singly Linked Lists

### Limitation of ArrayLists

* Fixed number of elements in the underlying array
* Cannot easily insert a value between two others
* Searching for a value can be very slow

```Java
ArrayList<String> dogs = new ArrayList<String>(4);
names.add("Socks");
names.add("Logan");
names.add("Riley");
names.add("Pearl"); // already full

names.add("Lucy");//Create a new one that is 2x and copy all

names.add(1, "Moxie");//all get shifted by 1; when full create a new one

if (names.contains("Logan")) {//
    
if (names.contains("McBaine")) {// time-consuming as loop all
```

### Data stored in LinkedList
- LinkedLists allow us to address some of the limitations of ArrayLists
- A LinkedList is a collection of nodes that are linked together, one following the other
- The “head” and “tail” nodes tell us where the LinkedList starts and ends
- We can add and remove elements at the head, at the tail, or at a specified index
- We can also get an element by its index, and search for a value

![](LinkedList.png)

**LinkedList.add**
- We can add a value to a LinkedList in one of three places:
    - front: link new node to current head; point head at new node
    - rear: link tail node to new node; point tail at new node
    - middle: link new node to one that follows it; link previous node to new node
- Adding values to a LinkedList does not require shifting values in memory, just updating the links

```Java
public void addLast(E value){
        Node newNode = new Node(value);
        if (head == null) {//case: this is the only node in LinkedList
            head = newNode;
        } else {
            tail.next = newNode;
        }
        tail = newNode;
    }
```
![](ll1.png)

**LinkedList.remove**
- We can remove a value from a LinkedList in one of three places:
    - front: point head at node following old head
    - rear: point tail at node preceding old tail
    - middle: link previous node to one that follows node being removed
- Removing values from a LinkedList does not require shifting values in memory, just updating the links

```Java
public void remove(int index) {
    Node current = head;
    for (int i = 0; i < index - 1; i++) {
        current = current.next;
    }//i-2 to i-1
    current.next = current.next.next;
}
```
![](ll2.png)

**Searching in a LinkedList**
- We can search for a value in a LinkedList by starting at the head and comparing the target to each node’s value, one at a time
- If we get to the end and haven’t found the target, then it’s not in the LinkedList

**Finding LinkedList Data by Index**
- We can access an element in a LinkedList using a 0-based index, as we would in an array
- This requires starting at the head and following links until we arrive at the index we’re looking for

```Java
public E get(int index) {
    Node current = head;
    for (int i = 0; i < index; i++) {
        current = current.next;
    }//i-1 to i
    return current.value;
}
```

```Java
public class LinkedList<E> {
    class Node { //define node class
        E value; 
        Node next; //reference/link to next node
        Node(E value) { // node constructor
            this.value = value;
        }
    }
    protected Node head = null;//linkedList initially empty
    protected Node tail = null;
    
    public void addFirst(E value) {
        Node newNode = new Node(value);
        newNode.next = head;
        head = newNode;
        if (tail == null) {//case: this is the only node in LinkedList
            tail = newNode;
        }
    }
    
    public void add(int index, E value) {
        if (index < 0) throw new IndexOutOfBoundsException();
        if (index == 0) { addFirst(value);} // add to head
        else {
            Node newNode = new Node(value);
            Node current = head;
            for (int i = 0; i < index - 1; i++) {
                if (current == null) throw new IndexOutOfBoundsException(); //null so we past the tail
                current = current.next;//i-2 to i-1
            }
            if (current.next == null) { tail = newNode; } //add to tail
            newNode.next = current.next;
            current.next = newNode;
            }
    }
    
    public void removeFirst() {
        if (head != null) {
            head = head.next;
        }
        if (head == null) {//empty LinkedList
            tail = null;
        }
    }
    
    public void removeLast() {
        if (head == null) { //empty list
            return;
        } else if (head == tail) {
            //single element list
            head = null;
            tail = null;
        } else {
            Node current = head;
            while (current.next != tail) {
                current = current.next;
            }//now curent.next = tail
            tail = current;
            current.next = null;
        }
    }

    public void remove(int index) {
        if (index < 0) throw new IndexOutOfBoundsException();
        else if (index == 0) removeFirst();
        else {
            Node current = head;
            for (int i = 0; i < index - 1; i++) {
                if (current == null) throw new IndexOutOfBoundsException();
                current = current.next;
            }
            current.next = current.next.next;
            if (current.next == null) {
                tail = current;
            }
        }
    }
    
    public boolean contains(E value) {
        Node current = head;
        while (current != null) {
            if (current.value.equals(value)) {
                return true;
            }
            current = current.next;
        }
        return false;
    }
    
    public E get(int index) {
        if (index < 0) {
            throw new IndexOutOfBoundsException();
        } else {
            Node current = head;
            for (int i = 0; i < index; i++) {
                if (current == null || current.next == null) {
                    throw new IndexOutOfBoundsException();//too far
                }
                current = current.next;
            }
            return current.value;
        }
    }

}

```


### LinkedList in Java API

**Limitations of Using an ArrayList**
1. Fixed number of elements in the underlying array
2. Cannot easily insert a value between two others

```Java
java.util.LinkedList<E>

LinkedList()// Constructs an empty list

LinkedList(Collection<? extends E> c) // Constructs a list containing the elements of the specified collection, in the order they are returned by the collection’s iterator.

add(E element)// adds element to end (tail) of list; same as addLast

add(int index, E element) //adds element at specified index in list

addFirst(E element)// adds element to front (head) of list

addLast(E element) // adds element to end (tail) of list

set(int index, E element) //replaces element at at specified index with specified element

remove() //returns and removes the first element (head) of the list; same as removeFirst

removeLast() //returns and removes the element at the end of the list (tail)

remove(int index)//returns and removes the element at the specified index of the list

contains(E element)// indicates whether the list contains the specified element

get(int index) // returns the element at the specified index in list

getFirst() // returns the first element of the list (head)

getLast() //returns the last element of the list (tail)

```

Using **java.util.LinkedList**

```Java
import java.util.LinkedList;
...
LinkedList<Integer> numbers = new LinkedList<>();//generics

Scanner in = new Scanner(System.in);
int input = 0;

while (true) {
    System.out.print("Enter a number: ");
    input = in.nextInt();
    if (input == 0) {
        break;
    }
    numbers.add(input);
}

System.out.print("Enter another number: ");
input = in.nextInt();
if (numbers.contains(input))
    System.out.println(input + " is in the list");
else
    System.out.println(input + " is not in the list");
```

**LinkedLists and ArrayLists**

- Both implement the java.util.List interface
- This interface defines basic List operations including:
    - add
    - remove
    - contains
    - get by index
- Other code can use a List without needing to know how these methods are implemented

**Using java.util.List**
```Java
import java.util.List;//this code don't know what list we get
...
public int replaceMax(List<Integer> values, int replaceWith) {//all list have same method
    int maxValue = values.get(0);//first value
    int index = 0;
    
    for (int i = 0; i < values.size(); i++) {
        int value = values.get(i);
        if (maxValue < value) {
            maxValue = value;
            index = i;
        }
    }
    values.set(index, replaceWith);//replaces element at at specified index with specified element
    return maxValue;
}
```

**Summary: LinkedList and List**

- ``java.util.LinkedList<E> ``: LinkedList implementation in Java API
- ``java.util.List<E>`` : common interface of LinkedList and ArrayList classes
- List is an **abstract data type**: the code that uses it knows what it does but not how it does it

[Java Collections Framwork](https://docs.oracle.com/javase/8/docs/technotes/guides/collections/overview.html)

Read and  pay particular attention to the "Introduction," "Interfaces," and "Implementations" sections:

### Variations of LinkedLists

read Chapter 6: Stacks, Queues, and Deques, Chapter 7: List and Iterator ADTs

#### Stack
Here we want a List that will only be able to:
- add to the front
- and also remove from the front


**Stack**: A stack is a **Last In, First Out (LIFO)** data structure: the last element added is the first one removed

A data structure that works like a LinkedList but only has two operation
- push : add the specified element to the top of the stack
- pop : remove the element from the top of the stack

Although stack and queue can be implemented using LinkedLists, these
are abstract data types

**Stack.java**
```Java
import java.util.LinkedList;

public class Stack<E> {
    private LinkedList<E> list = new LinkedList<E>();
    public void push(E value) {
        list.addFirst(value);
    }
    
    public E pop() {
    if (list.isEmpty())
        return null;
    return list.removeFirst();
    }
}
```


```Java
java.util.Stack<E>

empty() // tests if stack is empty
push(E element) // places the specified element on top of stack
pop() // returns and removes element on top of stack
peek() // returns (but does not remove) element on top of stack, peek 偷看
```
TextEditor Example
```Java
import java.util.Stack
public class TextEditorHistory {
    protected Stack<String> history = new Stack<>();//field
    public TextEditorHistory() { }//?
    
    public void addToHistory (String operation) {
        history.push(operation);
    }
    
    public boolean canUndo() {//if we can undo the last operation
        return !history.empty();
    }
    
    public String undo() {
        if (!canUndo()) {
            return null;
        }
        return history.pop();
    }
}
```

#### Queue
Here we want a List that will only be able to:
- add to the rear
- remove from the front


**Queue**: A queue is a **First In, First Out (FIFO)** data structure: the first element added is the first one removed; 
a data structure that works like a LinkedList but only has two operations
- add : adds the specified element to the rear of the Queue
- remove : removes the element at the front of the Queue

**Queue.java**
```Java
import java.util.LinkedList;
public class Queue<E> {
    private LinkedList<E> list = new LinkedList<E>();
    public void add(E value) {
        list.addLast(value);
    }
    public E remove() {
        if (list.isEmpty())
            return null;
        return list.removeFirst();
    }
}
```
    
```Java
java.util.Queue<E>

isEmpty() //tests if the queue is empty

add(E element) //places the specified element at rear of
queue

remove() //returns and removes element at front of queue

peek()//returns (but does not remove) element at front of
queue
```

```Java
import java.util.*;//import all the classes and interfaces within java. util package
public class EventAvailableCapacity {
        protected Queue<Integer> ticketRequests = new LinkedList<Integer>();
    protected int availableCapacity;
    
    public EventAvailableCapacity(int maxCapacity) {
        availableCapacity = maxCapacity;
    }
    
    public void addTicketRequest(int numPeople) {
        ticketRequests.add(numPeople);
    }
    
    public int processUntilNoCapacity() {
        int numRequestsProcessed = 0; //number of requests
        while (!ticketRequests.isEmpty()) {
            int remainAfterRequest = (availableCapacity - ticketRequests.peek());
            if (remainAfterRequest < 0) return numRequestsProcessed;
            availableCapacity -= ticketRequests.remove();
            numRequestsProcessed++;
        }
    return numRequestsProcessed;
    }
}
```

#### Doubly LinkedList

Each Node in a Doubly LinkedList has two links: one to the next Node, and one to the previous. In the same way that the tail’s next Node is null, the head’s previous Node is null, to indicate that nothing comes before it.

### Project

#### LinkedList: encapsulated 封装 dt stru class. 
Implement the following static methods in the MyLinkedList.java file:

- reverse: Reverse the elements (list nodes, not just the values) in place.

- removeMaximumValues: Same behavior as part 1, but applied in place.

- containsSubsequence: Should return true or false as described in part 1. However, if the MyLinkedList other, the container of the other list, is null, the operation is undefined (unlike the case of the empty list) and this method should return null. Note that unlike part 1 where containsSubseqence return type is boolean, here the return type is Boolean to allow for the trinary result

## M3: Analyzing Data Structure

Module Learning Objectives
- Understand the mathematical concept of asymptotic and Big-Oh notation.
- Evaluate the Big-Oh complexity of common data structure operations.

Module Glossary
- **Algorithm Complexity:** The number of operations that are required to perform an algorithm
- **Amortized Analysis:** A technique we use to determine an algorithm’s complexity by accounting for its overall cost over time.
- **Asymptotic Notation:** When describing Big-Oh complexity, we define our complexity $g(n)$ such that as our input size n increases, the number of operations will ultimately be upper- and lower-bounded by our more general function, $g(n)$. This is known as asymptotic notation.
- **Big-Oh Notation:** Notation that allows us to express the complexity in mathematical terms. This allows us to perform mathematical operations with complexity as we look at other data structures.
- **Constant Complexity:** If the number of operations is independent of the number of elements or the size of the data structure used, an algorithm is said to exhibit constant complexity. This is denoted as $O(1)$ complexity in Big-Oh notation.
- **Linear Complexity:** If the number of operations is linearly proportional to the number of elements, an algorithm is said to exhibit linear complexity. This is denoted as $O(n)$ complexity in Big-Oh notation.

Key Concepts & Examples
- **Algorithm Complexity** gives us an idea of how the number of operations in an algorithm relates to the number of elements/size of data structures used (i.e. constant, linear, exponential, etc.).
    - However, it does not necessarily give an indication of the exact computation time, which is dependent on hardware.
- **When Evaluating Algorithm** Complexity we always do so for the worst case. This is because lots of algorithms perform the same in the best case or even in the average case, but dramatically differently in the worst case.
- **Big-Oh Notation** allows us to express the complexity in mathematical terms. Big-Oh notation is always expressed as $O(g(n))$, where $g(n)$ is a general function (e.g. n if linear, $n^2$ for quadratic, etc.), this allows us to meaningfully compare algorithm complexities efficiently, while ignoring whatever affects our hardware or other factors may have on execution time.
- **Combining Big-Oh Complexities**
    - If a function A is $O(n)$, and we want to evaluate function B which runs operation A n times.
        - The complexity of the function B is $O(n × n) = O(n^2)$
    - If a function A is $O(n^2)$ , another function B is and we want to evaluate a function C, that runs the functions A followed by the function B
        - The complexity of C is therefore $O(n^2+n )$ , but since with Big-Oh notation we only care about the highest-order terms, this actually means that the complexity of C is simply $O(n^2)$
            - Note that ignoring the lower order terms only works if the variables are the same, for complexities with multiple variables, for example $O(n^2+m)$, we cannot just discard the m because it may or may not be larger than $n^2$
- **Evaluating the Complexity of a Function** (Example in 4.4) When evaluating the complexity of a piece of code, the main things to do are:
    - Go through the code line by line, and account for the amount of time taken by each line.
        - Typically single operations are $O(1)$, whereas lines that call other functions, will have the complexity of that function
        - Look for the use of loops, and what they are conditioned on (ni.e is the number of loop iterations a function of the number of inputs vs some constant number)
- **Amortized Analysis** is often used, for determining the complexity of an algorithm that has some degree of uncertainty or non-determinism by considering its behavior when used multiple times, instead of just a single time. This allows us to get a more accurate representation of the algorithm’s complexity by accounting for its overall cost over time.

Read Chapter 4: Algorithm Analysis



## M4: HashSets

Module Learning Objectives
- Describe the use of hash functions and hash codes in a HashSet.
- Implement a HashSet in Java.
- Resolve collisions in a HashSet using open addressing and separate chaining.
- Implement a self-resizing HashSet in Java.
- Evaluate the Big-Oh complexity of a self-resizing HashSet.
- Apply Sets to solving problems in Java.
- Apply Maps to solving problems in Java.

Module Glossary
- **Amortized Complexity**: An algorithm’s complexity calculated by looking at the total cost for the series of operations and amortizing this total cost over the full series. This is an alternative view to assuming the worst-case cost which can be an overestimate.
- **Collision**: In a hash system, this refers to the case where two elements are mapped to the same index in the underlying array.
- **Hash Code**: The value returned by a Hash Function that determines the numeric (integer) mapping of this element.
- **Hash Function**: A function/method that takes an input and returns an integer based on that input’s value. A Hash Function must be deterministic.
- **HashMap**: A data structure that associates a set of keys with corresponding values (each key to a specific value). It is also sometimes referred to as an associative array.
- **HashSet**: A set in which elements are placed in their respective array locations based on their hash code.
- **LoadFactor**: An attribute of the HashSet object that represents the acceptable average load, or number of elements, for each bucket. This is typically a value between 0 and 1.
- **Open Addressing**: A solution approach to hash collisions in which a new element is placed in the next available index (including wraparound indices) in the array if its own index is already occupied (A collision has occurred).
- **Probing**: In Open Addressing, this is the process of looking for an available spot/index in which to place the new element.
- **Separate Chaining**: A solution approach to hash collisions in which more than one element can be associated with the same slot/index of the underlying array. This is typically achieved by placing the elements in a LinkedList at that index, with new nodes being chained/added to the existing LinkedList in an occupied slot.
- **Set**: A data structure that represents a collection of distinct elements. Usually based on an underlying array structure.

Key Concepts & Examples
- The contains operation in __List__ implementations is O(n) since, in the worst case, we need to compare every element in the List against the target value.
- We can use a __hash function__ to calculate an element’s __hash code__, which can then be used to determine the spot where that element would belong in an underlying array; such a data structure is known as a __HashSet__.
- The add, remove, and contains operations are O(1) in a HashSet, assuming there are no __collisions__, which occur when multiple elements are hashed to the same slot in the underlying array.
- Collisions can be resolved using __open addressing__ or __separate chaining__.

**HashSets** as can easily devolve into LinkedLists if all elements end up hashing to the same
bucket, causing us to lose the O(1) complexity we were aiming for. This is mitigated using
- __Dynamic Resizing__ where the number of buckets is increased once the HashSet gets too full.
- A HashSet is determined to be “too full” if the average number of elements per bucket (total number of elements / number of buckets) exceeds a predetermined __loadFactor__
- In the Java HashSet implementation, the default load factor is ¾ (but can be changed in the constructor)

**HashSet Resizing**
- Create a new underlying array of LinkedLists that is double the current array’s size
- Initialize each element of the array to be an empty LinkedList
- For each element in the old underlying array
    - Calculate the index it should go to in the new array (based on hashcode and new array size)
    - Add the element to the LinkedList in the corresponding array index

Even though resizing is a costly operation, it allows searches, insertions and removals to
remain ~O(1) in the future, thus making it more efficient than simply letting the HashSet
devolve into a set of overly long LinkedLists.

__HashSets exhibit the properties of mathematical sets__, therefore, no duplicate elements
are allowed in a HashSet.

A **HashMap** is a data structure that associates a set of keys with corresponding values
(each key mapped to a specific value). Typical HashMap operation include
- Adding key/value pairs using: __put(K key, V value)__
- Fetching the value associated with a specific key using: __get(K key)__
- Determining if the map contains a particular key using: __containsKey(K key)__
- Removing key/value pairs using: __remove(K key)__

## M5: Binary Search Trees

Module Learning Objectives
- Describe the limitations of a HashSet.
- Implement a Binary Search Tree in Java.
- Understand how a Binary Search Tree is used to keep elements in sorted order.
- Use a Binary Search Tree to solve problems in Java.

Module Glossary
- __Binary Search Tree (BST)__: A data structure comprised of nodes and links in which values can be stored in a sorted order and each node has an associated value as well as links to two child nodes. The left child of a node always contains a smaller= value and the right child contains a larger value than the parent node. Note: all the elements in the left sub-tree of a node are of lesser value than that node. Similarly, all elements in the right sub-tree of a node are of a higher value than that node.
- __Child Node__: In a tree, a child node is one that is pointed to by another node. I.e. there is a link from another node pointing towards it.
- __Inorder Traversal__: A strategy for traversing BSTs in which we recursively traverse the left sub-tree, followed by the root, followed by the right subtree. This traversal method leads to visiting nodes in sorted order.
- __Leaf Node__: In a tree, a node that has no children, in other words, both of its pointers point to null, is called a leaf node.
- __Node__: In a tree, a node is a data object that is typically used as a building block of. In a BST, a typical node contains fields for storing a value as well as links to two children (either or both of which can be null).
- __Parent Node__: In a tree, a node P that directly points to another node A is called its parent; P is the parent node of A.
- __Postorder Traversal__: A strategy for traversing BSTs in which we recursively traverse the left sub-tree, followed by the right subtree, followed by the root.
- __Preorder Traversal__: A strategy for traversing BSTs in which we recursively traverse the root, followed by the left sub-tree, followed by the right subtree.
- __Root Node__: In a tree, this is the topmost node of the tree. All other nodes are descendents of this node. In a balanced BST, this will typically be the median of the sorted set of values in the tree.
- __TreeSet__: A variant of the Set interface implementation in which data is stored in sorted order. TreeSets are generally implemented using an underlying BST data structure.

Key Concepts & Examples

- __Tree__: A tree is a data structure composed of nodes.
    - Each node has a value and links to zero or more nodes, called child nodes.
    - There is a single root node at the top of the tree.
    
- __Binary Tree__: A binary tree is a type of tree where each node has exactly two children, a left
and a right. Either or both children can be null.

- __Binary Search Tree__: A Binary Search Tree is a type of Binary Tree where the nodes are ordered.
    - A BST maintains its ordering by following these properties:
        - Each node’s value is greater than all the values to its left, i.e. its left subtree
        - Each node’s value is less than all the values to its right, i.e., its right subtree
    - A subtree is a tree whose nodes are a subset of a tree. In a BST, each subtree follows the constraints above.
        - BSTs help us efficiently store and retrieve data in a sorted order.
- __Binary Search Tree Operations__: We can perform the following operations on a BST and keep the tree ordered. For any node, smaller values are in the left subtree and larger values are in the right subtree. The following operations can be implemented with recursion
    - Search
    - Add
    - Remove
        - When a node is removed, it should be replaced with the largest value in its left subtree
- __Binary Search Tree Inorder Traversal__: If we want to explore all the values of a BST in order, we perform inorder traversal. This method also uses recursion. We first traverse a node’s left subtree, visit the node itself, and then traverse the right subtree. 
- __Tree Sets__
    - Binary Search Trees are implemented in the Java Collections Framework in the TreeSet class
    - TreeSet and HashSet both implements the Set interface
    - Although HashSet operations are more efficient, TreeSets are more appropriate when data needs to be stored in sorted order

## M6: Self-Balancing Binary Search Trees

Module Learning Objectives
- Evaluate the Big-Oh complexity of Binary Search Tree operations.
- Describe the implementation of a self-balancing binary search tree.

Module Glossary
- __Red-Black Tree (RBT)__: A balanced variation of a binary search tree that must satisfy a set of four rules in order to qualify as an RBT. 
    1. Each node is colored red or black.
    2. All null nodes are colored black. 
    3. Every red node has two black child nodes. 
    4. Every path from any node to any null node must have the same number of black nodes (not counting the node itself).
- __Black Height__: The number of black nodes along a path from any node to any null node in an RBT.
- __Rotation__: An operation performed on a node in order to make the overall tree more balanced. It generally affects the relationships between the node, its children and its grandchildren by shifting the order of links between them.
- __AVL Tree__: A self-balancing binary search tree named after Adelson-Velskii and Landis that uses rotations to maintain balance.
- __Balance Factor__: A metric used in AVL trees to determine whether a node is balanced. The Balance Factor is the difference between the height of a node’s left subtree and that of its right subtree. An AVL tree is balanced if the absolute value of the Balance Factor of every node is 1 or 0.

Key Concepts & Examples

- __Binary Search Tree Complexity__: In each step of a search, add or remove operation on a
BST, we reduce the number of elements we need to consider by half. This is O(log2n) for
each operation. However this is only true if the tree is __balanced__.

- __Self-balancing BST__: is one that adjusts itself when elements are added/removed to try to minimize the height.

- __Red-Black Tree__: is a type of self-balancing BST. 
    - A RBT must satisfy the following rules
        1. Each node is colored red or black
        2. All null nodes are colored back
        3. Every red node has two black child nodes
        4. Every path from any node to any null node must have the same number of black nodes (no counting the node itself), the black height of the tree
    - A value can be added to a RBT by initially placing it in the appropriate position of the BST and coloring it red
    - Recoloring and Rotation can be used to ensure that the RBT maintains its properties and remains balanced

- __AVL Tree__: another type of BST. It satisfies the property that the Balance Factor of every node is -1, 0, or 1, and uses rotations to maintain balance.

## M7: Tree Variation

Module Learning Objectives
- Understand the structure of a Max-Heap.
- Understand how a Max-Heap can be implemented in Java using an array representation.
- Understand the structure of a Trie.

Module Glossary
- __Max-Heap__: a binary tree data structure in which the value of any node is always greater than that of its children, ensuring that the largest value node is the root of the tree.
- __Array representation__: a way of representing the values in a tree using an array instead of nodes and links, such that the locations of a node’s parent and children can be determined based on the node’s index.
- __PriorityQueue__: the Java Collections Framework implementation of a Min-Heap.
- __Trie__: a tree-like data structure that is efficient at storing strings, in which each node holds a single character, and the nodes that are children of a node represent characters that follow that character in strings/values in the collection.

Key Concepts & Examples
- A __Max-Heap__ is a complete binary tree
    - Each level of the tree is filled before the next
    - Each level of the tree is filled in from left to right with no gaps
    - It also satisfies the heap property: each node has a greater value than its children, and thus all of its descendants
    - Finding the largest value in the Max-Heap can be done in O(1) time.
    - Adding a value and removing the largest value can be done in O(log n) time.

    - A Max-Heap can be implemented using array representation:
        - A heap with max height h will have an array size of 2h -1
        - The root of the tree is in array index 0
        - If a node is at index k…
            - Its left child is at index 2k+1
            - Its right child is at index 2k+2
            - Its parent is at index (k-1)/2

    - When a value is added to a Max-Heap, it is always placed in the rightmost available spot of the deepest level of the tree, i.e. in the first open spot of the array representation, and it “bubbles up” until it reaches a point at which the heap property is satisfied.

    - When the largest value is removed from a Max-Heap, it is replaced with the rightmost value of the deepest level of the tree, i.e. in the last spot of the array representation, and it “bubbles down” until it reaches a point at which the heap property is satisfied.

- A __Trie__ is a tree-based data structure for storing strings in order to support fast pattern matching. 
    - It satisfies the following properties:
        1. Each node, except the root is labeled with a character from the alphabet
        2. The children of an internal node have distinct labels
        3. Each leaf node is associated with a string, such that the concatenation of the labels of the nodes on the path from root to leaf yields that particular string
    - Strings can be added or removed by starting at the root and following paths to affected nodes
    - Special nodes can be used to indicate the termination of strings in case one is a prefix of others
    - All operations are O(m) where m is the length of the string, assuming a node stores its child nodes in an O(1) data structure

## M8: Graphs

Module Learning Objectives
- Understand the structure of a graph.
- Implement a graph in Java.
- Apply Breadth-First and Depth-First Search algorithms on a graph.
- Evaluate the Big-Oh complexity of graph operations.

Module Glossary
- __Adjacency List__: One of the common ways of representing a graph in code. A mapping of nodes to a list of the nodes with which they share an edge.
- __Adjacency Matrix__: One of the common ways of representing a graph in code. A 2D array in which the value of [x,y] represents the weight of the edge from x to y. In an unweighted graph, it will typically be simply a 1 to indicate the presence of an edge.
- __Breadth First Search (BFS__): A graph traversal algorithm where all immediate neighbors are visited before any more distant neighbors (e.g. neighbors of neighbors) are visited. The order in which nodes/vertices are visited is typically maintained using a Queue in BFS implementations.
- __Connected Component__: A subgraph (part of a larger graph) in which each node is reachable from any other node in the same subgraph.
- __Connected Graph__: A graph in which all nodes are reachable from all other nodes (either directly or through some path in the graph). The opposite of a disconnected graph, in which one or more nodes are not reachable from every other node.
- __Cycle__: A path where the start and end node are the same.
- **Cyclic Graph**: A graph that contains at least one cycle. The opposite of an acyclic graph, which contains no cycles.
- **Degree of a Node**: The number of each edges that a node has. In a directed graph these are split into in-degree (the number of edges pointing towards the node) and out-degree (the number of edges pointing away from the node).
- __Depth First Search (DFS)__: A graph traversal algorithm in which all univisited neighbors of a node N are recursively visited before moving on to the next unvisited node in the graph and applying the same strategy.
- __Directed Graph__: A graph in which the edges between nodes encode a specific direction to the relationship between the two nodes. The opposite of an undirected graph.
- __Edge__: An object representing a link between two vertices (nodes) in a graph. These edges can be weighted (have some value attached to the link between two nodes) or unweighted. They can also be directed (point from one node to another) or undirected. Attributes such as weight and direction are typically stored as fields of the Edge object.
- __Edge Set__: One of the common ways of representing a graph in code. A set of objects representing edges in the graph.
- __Graph__: A data structure that consists of two main types of components, nodes (vertices) and edges connecting them. In a graph, each node can have an arbitrary number of edges to other nodes.
- In-Edge of a Node: In a directed graph, this is an edge that points towards this node from another node.
- __Neighbor__: In a graph, a neighbor to a node A is any node that shares an edge with that node A. In a directed graph, a node is only considered a neighbor of node A if it is the destination node of one of the out-edges of node A.
- __Node/Vertex__: One of the components of a graph. They generally contain some fields to store information about the elements contained in the graph.
- __Out-Edge of a Node__: In a directed graph, this is an edge that points away from this node to another node.
- __Path__: In a graph, a path is a list of nodes from a start node to an end node in which each successive pair of nodes is connected by an edge.
- __Weighted Graph__: A graph in which all edges have an associated numerical value (weight). The opposite of an unweighted graph, in which all edges are assumed to have the same (or no) weight.

Key Concepts & Examples
- **Graphs** are useful for representing relationships and distances between elements.
    - A graph is composed of nodes and edges
    - **Nodes** typically stores information about the objects contained in a graph. Each node can have an arbitrary number of edges to other nodes.
    - **Edge**: an object representing a relationship between two nodes in a graph. These can be weighted or unweighted, and directed or undirected
    - A **path** is a list of nodes in which each successive pair of nodes is connected by an edge
    - A **cycle** is a path where the start and end node are the same
    - A **connected graph** is a graph in which all nodes are reachable from all other nodes 
- **Representing Graphs**:
    - Graphs can be represented in various ways including:
        - Adjacency Matrix: 2-dimensional array in which value of [x,y] represents the weight of the edge from x to y.
        - Edge Set: A set of objects representing the edges in a graph.
        - Adjacency List: A mapping of nodes to a lists of other nodes with which they share an edge.
- **Traversing Graphs:**
    - **Breadth First Search (BFS)** is a systematic way of traversing a graph in which we:
        - Start with a source node
        - Then visit all its neighbors
        - Then visit all their neighbors
        - And so on, until the target node is found
    - **Depth First Search (DFS)**
        - considers one of the starting node’s neighbors, then one of its neighbors, then one of its neighbors…
        - And then considers other neighbors only when it can’t go any “deeper”

## M9: Intro. Software Design

Module Learning Objectives
- Identify the aspects of software quality.
- Convert a plain-English description of requirements into a domain model.
- Represent a model using a UML class diagram.
- Convert a UML class diagram into a Java implementation.

Module Glossary

- __Aggregation__: A relationship between two classes that indicates that one class is part of the other, but can exist independently on its own.
- __Association__: One of the possible relationships in a UML diagram (denoted by a solid line). It indicates that the two classes it connects go together in some way.
- __Composition__: A relationship between two classes that indicates that one class is part of the other, but cannot exist without the class to which it belongs.
- __Dependency__: One of the possible relationships in a UML diagram (denoted by a dashed line). It indicates that a class A uses the attributes/operations of another class B, but B is not a part of the class A.
- __Design__: In a software development process model, design is typically used to refer to the process of converting the requirements of the system to the implementation (E.g. plain english to Java or Pseudocode).
- __Domain Modeling__: An activity that occurs early in the design stage, where the concepts (classes) that are necessary t o represent the program/system are identified. In this process, the concepts’ properties, behaviors, and relationships are also identified.
- __Class Diagram__: A visual representation of classes, their attributes and operations, and their relationships.
- __Generalization__: A relationship between two Objects that indicates that one Object is a specialization of another. (Example: A Person is a generalization of Professor, and a Professor may have additional attributes/operations).
- __Grammatical Parsing__: An approach in which roles in the design are based on the parts of speech used to specify the system in the English description. For example, Nouns tend to be translated to classes or attributes, Adjective to subclasses or attributes, and Verbs to operations or relationships.
- __Has-A Relationship__: One of the possible relationships between classes in a UML diagram. There are two types of such a relationship which are: aggregation (denoted by a line ending with an empty diamond-shaped arrowhead), and composition (denoted by a line ending with a filled diamond-shaped arrowhead).
- __Is-A Relationship__: One of the possible relationships between classes in a UML diagram. There are two types of such a relationship which are: generalization (denoted by a solid line ending with a triangular arrowhead), and realization (denoted by a dashed line ending with a triangular arrowhead).
- __Realization__: A relationship between two Objects that indicates that one Object is an actualization/realization of another. An Object A that is realized by another Object B, is generally an abstract concept, meaning that Object A has no notion of existence without being a specific type of object Object B (Example: Dog, Cat, and Human, are all realizations of the abstract type Animal).
- __Software Development Life Cycle (SDLC)__: A set of 5 stages that are typically part of creating a software product. These stages are Requirements Elicitation, Design, Implementation, Testing, and Maintenance.
- __Unified Modeling Language (UML)__: A language/notation used for modeling and visualizing software design. UML has been an industry standard since the late 90s.

Key Concepts & Examples
- __Process Models__ typically define
    - The relative amount of time spent in each stage of the SDLC
    - The roles of individuals and organizations
    - The input and output for each stage
    - The iteration between stages
- __Domain Modeling__ is an activity that occurs early in the design stage, where the concepts (classes) that are necessary to represent the program/system are identified. In this process, the concepts’ properties, behaviors, and relationships are also identified. This is typically achieved using
    - Grammatical Parsing where roles in the design are assigned based on the parts of speech used to specify the system in the English description. Typically, we translate them using
        - Nouns : classes or attributes
        - Adjective :subclasses or attributes
        - Verbs : operations or relationships
- __UML Class Diagrams__ are used to present a visual representation of classes, their attributes and operations, and their relationships. These diagrams can then be easily translated to working code.
- There are 4 main types of relationships between classes.
    - “Is-a” relationships
        - Generalization
        - Realization
    - “Has-a” or “contains” relationships
        - Composition
        - Aggregation
    - “Uses” relationships
        - Dependency
    - “Association” relationships
        - Association
- __Relationships__ between classes can also have an associated multiplicity which indicates how many instances of one class A can be related to another class B and vice versa.
    - N : denotes a multiplicity of exactly N objects/instances
    - * : denotes a multiplicity of zero or more objects/instances
    - M..N : denotes a multiplicity with a minimum of M and a maximum of N objects.

## M10: Software Design Principle

Module Learning Objectives
- Identify the aspects of internal software quality.
- Understand how design principles relate to software quality.
- Apply design principles in order to create high quality software.

Module Glossary
- __Abstraction__: This refers to the notion that components (classes) should be able to use other components with minimal knowledge of the details of their implementation.
- __Analyzability__: An aspect of software internal quality that refers to the ease with which a programmer can read, understand, and reason about code.
- __Changeability__: An aspect of software internal quality that refers to the ease with which a programmer can change codes
- __Cohesion__: The notion of how well parts of a class (such as attributes and methods) “go together”, and whether it makes sense for them to be grouped together.
- __Controllability__: An aspect of testability that refers to the ability to put code into the state you want to test.
- __External Quality__: This refers to the quality of the software as it runs on hardware in some execution environment (i.e. speed, memory, security, etc.)
- __Functional Independence__: This refers to the notion that components (classes/modules) should have minimal dependence on other components.
- __Internal Quality__: This refers to the quality of the code as text that humans need to read and write (i.e. analyzability, changeability, stability, testability, and reusability)
- __Modularity__: A concept in software quality that refers to the idea that each module (or class) is only responsible for a single part of the functionality of the overall system.
- __Monolith__: This refers to a software architecture in which a single piece of code (a single main function for example) is responsible for the functionality of the entire program.
- __Observability__: An aspect of testability that refers to the ability to examine the state of the code you’re testing
- __Reusability__: An aspect of software internal quality that refers to the ease with which code can be reused in other applications.
- __Software Architecture__: The process of dividing a software system into a subsystems that address major parts of functionality.
- __Stability__: An aspect of software internal quality that refers to the extent to which the code is tolerant of changes to other parts of the code.
- __Testability__: An aspect of software internal quality that refers to the ease with which code can be tested.
- __Three-Tier Architecture__: An example of software architecture in which the system is split up into three subsystems. These tiers are the Data, Logic, and Presentation tiers

Key Concepts & Examples
- __Software Internal Quality__ refers to the quality of the code as text that humans need to read and write, aspects of it include
    - __Analyzability__ which refers to the readability and understandability of code.<br>
    This is necessary so that a programmer can easily
        - Identify and fix defects
        - Add /improve functionality
        - Understand how an algorithm/solution is implemented
    - __Changeability__ which refers to the ease with which code can be changed.<br>
    Highly changeable code allows a programmer to easily
        - Fix defects
        - Add/improve functionality
        - Incorporate new code
        - Improve other aspects of software quality
    - **Reusability** which refers to the ease with which code can be reused in other applications. Reusable code allows a programmer to
        - Reduce time spent developing new code
        - Reduce the likelihood that new code will contain defects
    - **Stability** which refers to the idea that modifying one part of the code should have a limited effect on others. High stability allows a programmer to
        - Make changes in one part of the code without being required to make changes in other parts. This has the added benefit of reducing the time/effort required to change code.
    - **Testability** which refers to the controllability and observability of code. High testability allows a programmer to easily
        - Create test cases
        - Identify and fix defects
        - Increase confidence that software is working correctly
 - __Software Architecture__ refers to the process of dividing a software system into a subsystems that address major parts of functionality.
     - Each subsystem should be able to do its work with minimal dependency on other subsystems and minimal knowledge of their implementation.
- __Three-Tier Architecture (TTA)__ is when the system is split up into three subsystems.
    - __Data__: The bottom tier of TTA, it contains all the code that handles functionality related to storing and retrieving data. It doesn’t interact with the user or do any processing of the data, it just makes it possible for the rest of the program to access whatever data it needs to use.
    - __Logic__: The middle tier of TTA, this is where the program performs calculations, makes decisions, etc. This part of the code doesn’t interact with the user either, and it doesn’t do anything with storing and retrieving data.
    - __Presentation__: The top tier of TTA and is also known as the user interface tier. This is where all user interaction occurs, no data processing or storage is handled in this tier.
- __Modularity__ is one of three important design concepts that help achieve high internal quality. It refers to the notion that each module (or class) is only responsible for a single part of the functionality of the overall system.
    - By splitting up the functionality into separate modules, we make the code easier to read and understand, easier to test and debug, easier to reuse, and most of all, easier to change.
- __Function Independence__ is one of three important design concepts that help achieve high internal quality. It refers to the notion that modules should be able to perform their own tasks with minimal dependence on other modules.
    - By my allowing a module to perform its tasks with minimal dependence on other modules, we make it easier to understand, test, and reuse on its own, but most of all, it makes the class easier to change without having to change other modules.
- __Functional Independence__ is achieved by
    - Minimizing the complexity of interfaces between modules
    - Minimizing the control that one module has over another
- __Abstraction__ is one of three important design concepts that help achieve high internal quality. It refers to the notion that a module should be able to use other modules with minimal knowledge of the details of their implementation. I.e. a module should only care what another module does if it will be using it, and not how it is done.
    - This mostly helps with improving stability, as changes to the internal details of other modules should have no effect on the module using them, since it never depended on those details anyway.

## M11: Software Design Patterns

Module Learning Objectives
- Understand the structure of common software design patterns in Java.
- Apply software design patterns to solve problems in Java.

Module Glossary
- **Design Pattern**: a general reusable solution to a commonly occurring problem; a description or template for how to solve a problem that can be used in many different situations.
- **Creational Patterns**: design patterns that seek to separate the code that creates an object from the code that uses it.
- **Structural Patterns**: design patterns that address problems such as:
    - how do we assemble the constituent parts of an object?
    - how do we define the relationships between classes?
    - how do we combine objects into larger structures?
- **Behavioral Patterns**: design patterns that address problems such as:
    - how do objects communicate?
    - how are responsibilities assigned to different objects?

Key Concepts & Examples

**Singleton Pattern**: Creational pattern that ensures that there is only one instance of a class,
and that it can be accessed easily
- make the class’ constructor private
- expose a public static method that returns the singleton instance

Factory Method Pattern: Creational pattern that uses inheritance to separate the code that
uses another class from the code that creates it
- Class A has a dependency on Class B
- Class A contains code to use Class B
- Subclasses of A override a “factory method” used to create an instance of the desired subclass of B

**Bridge Pattern**: Structural pattern that maintains separate inheritance hierarchies of
concepts (abstractions) and things that uses them (implementors) and “bridges” them using
aggregation so that Client only needs to work with abstraction

**Strategy Pattern**: Behavioral pattern in which we create classes to specify certain
“strategies” that can be used as part of a larger algorithm

**Observer Pattern**: Behavioral pattern in which a Subject has a set of Observers that can be
notified when an event occurs. Observers can be added and removed as the program runs

## M12: Writing Good Code

Module Learning Objectives
- Determine the ways in which the readability and understandability of code can be improved.
- Apply techniques to improve the understandability of code.

Module Glossary
- **Code Smells**: A term used to describe indications of bad design or bad internal quality in code.
- **Dictionary Words**: Words that occur in everyday language. These are good to use as variable names, as they tend to be easier to read/recognize, in comparison to words that are made up.
- **Duplicate Code**: One of the most common code smells that occurs when we use the same (or very similar) code in multiple places by copy and pasting it in multiple locations.
- **Extract Method**: A refactoring pattern used to address duplicate code in which we pull out, or extract, the code that’s duplicated and put it in a new method, and then invoke that method wherever we had the original duplicate code.
- **Extract Superclass**: A refactoring pattern where we create a new common superclass that contains a method that can be used in multiple subclasses
- **Readability**: In code, readability is the ease with which the reader can identify and differentiate tokens and their syntactic purpose.
- **Refactoring**: An activity by which we modify code but don’t change its functionality. Generally, the purpose of refactoring is to improve readability/understandability, or reduce the number of lines of code.
- **Syntactic Purpose**: For a token this is defined as what the function of the token is in that particular position in the statement of code.
- **Understandability**: In code, understandability is the ease with which a reader can identify the semantic meaning of code (i.e. what the code does).

Key Concepts & Examples

__Code readability__ is the ease with which the reader can identify and differentiate tokens and
their syntactic purpose. It is important because people need to read code in order to:
- Fix bugs
- Add features
- Understand how a problem was solved
- Improve quality: efficiency, security, etc.

Code readability is affected by the following factors:
- Use of whitespace
- Identifier length
- Use of dictionary words
- Variation among identifiers

__Code understandability__ is the ease with which a reader can identify the semantic meaning
of code.
To improve code understandability
- Use meaningful identifier names
- Use indentation and spacing
- Use punctuation
- Use comments

__Refactoring__ an activity by which we modify code but don’t change its functionality.
Why should we refactor?
- Improve the internal quality of code
- Simplify future code changes
- Reduce the amount of code to maintain

When should we refactor?
- Constantly!
- When you see code (or are writing code) that doesn’t adhere to the intended design
- As a way of understanding the code

How should we refactor?
- Carefully!
- Make small changes before big ones
- Be careful about:
    - Introducing bugs
    - Breaking “published” interfaces
    - Unnecessarily decreasing external quality
    
What should we refactor?
- Code smells: indication of bad design
- Code that is hard to read or hard to understand
- Code that does not adhere to conventions
- Code that is unnecessary or in the wrong place

__Duplicate Code__ is the most common code smell. Two ways of dealing with duplicate code
include:
- Extract Method: Create a new method that can be used in multiple places
    - Assumes duplicate code is in the same class
- Extract Superclass: Create a new common superclass that contains a method that
can be used in multiple subclasses

## M13: Software Efficiency

Module Learning Objectives
- Understand the tradeoffs between efficiency and other aspects of quality.
- Accurately evaluate the execution time of a piece of software.
- Apply software programming techniques to improve the efficiency of code.

Module Glossary
- __Wall-Clock Time__: elapsed “real” time between two events, as would be measured by a wall clock, stopwatch, etc. This can lead to inaccuracies when measuring software execution time because of other factors, e.g. operations being performed by the Java Virtual Machine, operating system, hardware, etc.
- __Lazy evaluation__: programming technique in which we evaluate expressions only when we know we’ll need the results
- __Lazy initialization__: programming technique in which we only create objects when we know we’re going to need them
- __Memoization__: programming technique in which we keep a Map of inputs (arguments) to outputs (results) and return the result from the Map if the same input is seen more than once. This will lead to more memory utilization but may greatly reduce execution time.
- __Method Inlining__: micro-optimization technique in which we replace method call with method body
- __Loop Unrolling__: micro-optimization technique in which we replace for-loop with multiple instances of body
- __Constant Folding__: micro-optimization technique in which we replace literal numerical expression with result
- __Strength Reduction__: micro-optimization technique in which we replace complex operations with simpler ones

Key Concepts & Examples

Software quality is about __tradeoffs__: improving one aspect of external quality may harm other
aspects of external quality and/or internal quality. If we make our code faster, we may also
make it:
- harder to understand
- harder to change
- less likely to provide the correct functionality
- less secure
- likely to use more memory
- more time-consuming to develop

Software efficiency rules of thumb:
- Always use the right data structure.
- Make the common case fast.
- Don’t do work unnecessarily.
- Be careful about accidentally harming other aspects of quality.

Execution time can be measured by various mechanisms:
- Use Java System methods to measure execution time of small pieces of code.
- Use UNIX “time” command to measure execution time of entire program.
- Use profiling tools for more detailed information.

To avoid doing unnecessary work:
- Don’t check conditions unnecessarily
- Don’t call methods unnecessarily
- Don’t redo work you’ve already done
- Use the Java API when possible
- Use lazy evaluation, lazy initialization, and memoization
- Take advantage of short-circuit boolean operators
- Use micro-optimizations sparingly, especially if they may harm understandability

## M14: Concurrency in Java

Module Learning Objectives
- Implement concurrent code using Java threads.
- Understand the behavior of concurrent code and how it can lead to race conditions.
- Apply synchronization in order to address race conditions.

Module Glossary
- __Concurrency__: A feature of some programming languages that allows a program to execute different parts of the code at the same time. In Java, this is achieved using Threads.
- __Critical Section__: A piece of code where a race condition could occur.
- __Heap__: The area of memory where objects are stored. It is also where static and global variables are stored.
- __Mutual Exclusion__: The process of ensuring that critical sections of code are only ever executed by a single thread at a time (i.e. making sure that access to that critical section is mutually exclusive for different threads). This is necessary to avoid inaccurate results being caused by race conditions.
- __Race Condition__: In threading, a race condition can occur when multiple threads are trying to modify the same piece of data. This this can lead to not only non-deterministic results, but also incorrect behavior if the results of operations are lost.
- __Stack__: The area of memory where local variables and method arguments are stored. A stack also holds its own program counter, which holds the address of the next instruction to execute.
- __Synchronized Method__: One of the ways of ensuring mutual exclusion in Java. This ensures that only one thread at a time can execute this method for a given object.
- __Synchronized Blocks__: A more fine-grained approach to ensure mutual exclusion than synchronizing a whole method, by only locking a section of the function. This allows us to have a critical section that’s smaller than an entire method, and also to have multiple critical sections that can be run simultaneously. Each synchronized block relies on an object as its lock. If an object is locked, then no other thread can enter a synchronized block that is using it. But another thread can enter a synchronized block that’s using a different object.

Key Concepts & Examples
Some rules of thumb for __software efficiency__ include:
- Always use the right data structure!
- Don’t do work unnecessarily.
- Don’t allocate memory unnecessarily.
- Do more than one thing at a time

Doing more than one thing at a time in a program is called concurrency. For example,
- Performing two parts of a calculation simultaneously
- Reading data from one source while writing to another
- Blocking/waiting for some input while performing some calculation

To achieve concurrency, we use **threads**.
- __Threads__ are separate lines of execution in the same process (running program)
- Each thread has its own
    - stack (local variables, method arguments)
    - program counter (address of next instruction to be executed)
- Threads in the same process share:
    - heap (space in memory where objects are stored)
    - static variables
    
In Java,
- Thread classes can extend the java.lang.Thread class or implement the java.lang.Runnable interface
- Represents the starting point of a separate line of execution in the running program
    - start() : launch a new line of execution
    - run() : entry point to new line of execution
    
Using threads in Java:
- We use threads to solve “embarrassingly parallel” processes.
- Typically, N threads each do 1/Nth of the work, and then the sub-solutions are combined to create the solution
- Care must be taken to wait for all the threads to finish!

Thread non-determinism
- Multiple threads can be used to perform different operations simultaneously, even on the same object
- This can lead to **non-deterministic** results because the ordering of the execution of the threads is not guaranteed

Thread race conditions
- When multiple threads operate on the same piece of data, this can lead to not only non-deterministic results, but also incorrect behavior if the results of operations are lost. These are called **race conditions**.

Thread synchronization
- Synchronization, or **mutual exclusion**, can be used to address race conditions.
    - **Mutual exclusion**: only allow one thread at a time to execute the critical section where a race condition could occur
    - **Synchronized method**: only one thread at a time may execute that method (or any other synchronized methods) on that object
    - If a thread is executing a synchronized method on an object, any other thread that tries to execute a synchronized method on the same object will need to wait for the first thread to finish
- Synchronized methods ensure that only one thread at a time can enter those methods.
- Synchronized blocks provide more fine-grained access

## M15: Group Project & Final
