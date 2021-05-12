
**Data Structure**
@ Prof. Chris Murphy from Penn
```Java
@ Note by Gary Zhang
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


### Java/JUnit Refresher

### Implement Data Structrues

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
- ArrayList: A data type similar to an array but allowing for a dynamically resizable array implementation. The overhead is the number of array positions that are currently unused.
- Head: A Node object that is typically used to denote the first Node in a LinkedList instance.
- IndexOutOfBoundsException: A runtime error that indicates a attempt to reach an index that does not exist in the object of the given data type.
- LinkedList: A class that uses Node objects to store the list elements. Nodes also include pointers/links to other nodes in the list since they are not stored in contiguous memory addresses.
- Link/Pointer: A variable whose value is the memory address of another value. In a LinkedList, its value is typically the location of another Node in the list.
- Node: A supporting object that forms the building block for a LinkedList. It typically contains fields that store the list element as well as a pointer or link to other Nodes.
- Tail: A Node object that is typically used to denote the last Node in a LinkedList instance.
- Stack: A data structure that works like a LinkedList but only has two allowed modifying operations; push which adds an element to the top of the stack, and pop which removes the element at the top of the stack.
- Queue: A data structure that works like a LinkedList but only has two allowed modifying operations; add which adds an element to the rear of the queue, and remove which removed the element at the front of the queue.
- FIFO (First In, First Out) Data Structure: A data structure where the first element added is the first one removed. In other words, elements are removed from in the same order that they are added. A Queue is an example of a FIFO data structure.
- LIFO (Last In, Last Out) Data Structure: A data structure where the last element added is the first one removed. In other words, elements are removed in the reverse order in which they were added. A Stack is an example of a LIFO data structure.
- Java Collections Framework: A java-provided collection of implementations for common objects, data structures, and interfaces. Examples include the LinkedList class, ArrayList class, and the List interface.

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


## M4: HashSets

## M5: Binary Search Trees

## M6: Self-Balancing Binary Search Trees

## M7: Tree Variation

## M8: Graphs

## M9: Intro. Software Design

## M10: Software Design Principle

## M11: Software Design Patterns

## M12: Writing Good Code

## M13: Software Efficiency

## M14: Special Topic: Concurrency

## M15: Group Project & Final
