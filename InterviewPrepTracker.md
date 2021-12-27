### DS Algo:
<hr>

1. DS - revise all the DS basic questions - Linked Lists, Binary Tree, BST, Graphs :: This should be on my tips.
2. Algo -
    
   + Searching and Sorting
   + Arrays - normal algo related
   + Recursion questions
   + Greedy
   + DP
   + Backtracking

<hr>

### Java:

1. Core Java Basic:
        
   + OOPS concepts
   + Abstract Classes vs Interface ? 
   + Polymorphism
   + Inheritance
   + JVM / Memory Model / Garbage Collector
   
        + [Garbage Collection Working](https://javarevisited.blogspot.com/2011/04/garbage-collection-in-java.html#axzz7FKNhlkRJ)
   + Strings
   + resources:
        1) [OOPS Programming Questions](https://javarevisited.blogspot.com/2020/05/object-oriented-programming-questions-answers.html#axzz7Dp4B87DM)
        2) [Design Pattern Problems](https://javarevisited.blogspot.com/2012/06/20-design-pattern-and-software-design.html#axzz7Dp4B87DM)
        3) [Design Vending Machine](https://javarevisited.blogspot.com/2016/06/design-vending-machine-in-java.html#axzz7Dp4B87DM)

    + Collections:
        
        + Lists
        + LinkedList
        +  Queue
        +  HashTable
        +  Vector
        +  HashMap : Concurrent HashMap
        +  Iterators - Fail Safe and Fail Fast Iterators
    
    + Multithreading Questions

<hr>

### Design Patterns

  Go to this link for Design Pattern notes : [DesignPatternNotes](https://github.com/rshubham/Revision_Notes/blob/master/DesignPatterns.md) 

<hr>

### SQL/PLSQL

<hr>

### Projects (Deploy all these projects in Azure VM instance)

1. [Azure Link](https://portal.azure.com/#home)
2. Azure Credentials: c2hpdmFtLmx5bnV4QG91dGxvb2suY29tL1NoaXZfMjEwOA==

   + Spring Boot / Spring Framework: 

        + Develop REST endpoints for an application using Spring Boot.
        
        + RockPaperScissors Game using SpringBoot Rest: [RockPaperScissorsGame](https://github.com/rshubham/RockPaperScissorsGame)
   
        + Spring Security and JWT: [SpringSecurity using JWT](https://github.com/rshubham/springSecurityApp)
        + Spring Security and OAuth 
        
   + Kafka
   
   + Camel
   
   + Storm
   
   + JMS - How it implements different design patterns (Observer, Mediator etc.)

<hr>

### OOPS Concepts:

The key technical differences between an abstract class and an interface are:

1. Abstract classes can have constants, members, method stubs (methods without a body) and defined methods, whereas interfaces can only have constants and methods stubs.

2. Methods and members of an abstract class can be defined with any visibility, whereas all methods of an interface must be defined as public (they are defined public by default).

3. When inheriting an abstract class, a concrete child class must define the abstract methods, whereas an abstract class can extend another abstract class and abstract methods from the parent class don't have to be defined.

4. Similarly, an interface extending another interface is not responsible for implementing methods from the parent interface. This is because interfaces cannot define any implementation.

5. A child class can only extend a single class (abstract or concrete), whereas an interface can extend or a class can implement multiple other interfaces.

6. A child class can define abstract methods with the same or less restrictive visibility, whereas a class implementing an interface must define the methods with the exact same visibility (public).

<hr>

[Software Design Interview Questions](https://javarevisited.blogspot.com/2012/06/20-design-pattern-and-software-design.html#axzz7Dp4B87DM)

[Static from non-static Context](https://javarevisited.blogspot.com/2012/02/why-non-static-variable-cannot-be.html#axzz7Dp4B87DM)


<hr>

### MagicBricks Prep

+ DS/Algo:
    
    + Graphs (/ n-ary Tree):
        
        + Generate Graph for normal edges
        + Generate Graph for weighted edges
        + Topological Sort - (Kahn's Algo, etc.)
        + Find the shortest Path (Dijkstra's Algo)
        + Print the Minimum Spanning Tree - (Kruskal's Algo)
        + Loop Detection in a Graph (Floyd Warshall Algo)
        
   + Greedy:
   
        + Fractional Knapsack Problem
        + Jump Game Problem
   
   + Recursion:
   
        + Print all the Permutations of a String/Array
        + Islands Problem (BFS)
        + Robots - find the unique path (DFS)
        
   + DP:
        
        + Longest Palindromic Substring
        + Subset Sum
        + 0/1 Knapsack Problem
        + Buy/Sell Stock Problem
        
   + Trees (BT/BST):
   
        + Problem to check whether a tree is a BST or not?
        + Left/Right/Top/Bottom View of a BT
        + LCA of a BT
        + Height of a BT
        
   + Linked-Lists:
   
        + Reverse a linked-list
        + k-node reversal of a Linked-List
        + Loop Detection in a Linked-List (Floyd Warshall Algo)
        + Add two numbers stored in a linked list
        
   + Arrays/Strings:
   
        + Binary Search Algo
        + Sorting Algo - Merge Sort/Quick Sort
        + find kth smallest/largest element in a list/array.
        + Trapping Rainwater Problem
        + Leetcode Rainwater Problem

<hr>

### My Experience

#### MagicBricks

**Round 1:**

   1. Microservices: How services interact in Microservices, Circuit-Breaker, REST API
   2. Spring Boot : Profiling, Annotations, Diff between MVC and Boot, Hibernate - ORM, Actuators.
   3. Java 8: Lambda Expressions.
   4. Diff between String, String Builder, String Buffer - which is suitable to use in multithreaded envt.
   5. Kafka : How Producer and Consumer works in Kafka.

<hr>

###From Shivam

**2017**

 + **Magic softwares (wasted my time in this company don't even think about it)**
    
    + Thread pool executors types and difference in them.
    + Scenarios which threadpool to use.
    + Arraylist vs linkedlist -- why to use arraylist over linkedlist when the same can be done with linkedlist also.
    + How can a singleton class be breaked apart from multi-threading like clonable, serializable etc.
    + Why use microservices when they are difficult to manage.
    + Difference between IOC and DI and how BeanFactory manages them
    + What is application context
    + Difference between merge and update in hibernate
    + Sessionfactory vs session
    + Immutable classes
    + String pool -- moving object from string pool to heaps.
    + Mark and sweep algorithm of GC, how GC identifies which object to be removed etc and how it reaches it.
    + Permutation algorithm.

**Jabong -- SDE2**

   + **1st Round**
 
   1. Find cousins of nodes in a given BST (code also)
   2. Sorted Lists in java -- keeping lists always sorted -- need to create AVL tree -- balanced binary tree (no code only discussion)

   + **2nd Round**

   1. Merge Sort in array (code)
   2. Design a vending machine found in metro station.
   3. Finding a number in sorted rotated Array (code)

    Rejected after this round 

**2018**

**Times Internet TOI team**

   + **1st Round**

   + Memory allocation with new key word.
   + Size of instance object in memory.
   + Random num function with next random nu etc
   + Design your own cache system.
   + Microservices architecture discussion for current project.
   + Which database to use in which scenarios like why postgres over mysql
   + Thread interrrupt.

  Rejected after this round

Times Internet -- TOI Big data team:
1st Round :-
Dictionary design -- trie tree with code
Design question -- abstract factory pattern
Design Reco engine

FreeCharge 2018 :-

Round 1 :-
Decoding the number to digit -- https://www.geeksforgeeks.org/count-possible-decodings-given-digit-sequence/ (code)
LRU Cache DS design (code and DS)
Round 2 :-
 Design of A/B testing tool, expression evaluator
Threadpool design
Rejected after 2nd Round -- considering me for SSE

OYO Rooms -- 2018:-

Round 1
Find sum of path from root to leaf (code)
2nd question I don't remember (cide)
Round 2 :
      1.  Design your own OYO -- rooms, hotels, customer, mapping etc
  
 Round 3 :
Lowest common ancestor in binary tree -- with recursion (code)
Design the DS with every operation of insertion, deletion, update and search in O(1) -- discussion
Rejected with feedback poor DS

MakeMyTrip -- 2017:-
  1st Round
minimum number of platforms required with given time and platform number. (cide)
sorting the number such that number before decimal is sorted in desc and after decimal in asc (code)
flattening of linkedlist, in-place flattening. (code)
Rejected

LensKart 2018 :-
  1st Round Telephonic
Basic java questions -- working of hashmap, what will happen on inserting same key with same hashcode and equals and what will it returns etc
Swapping number in a linkedlist of size 2
DS question I forgot
Serialziation
If parent class is serialized and child class is not, will data store in db.
2nd Round F2F :-
Question on tree traversal don't remember (code)
LFU cache design
SOLID Design principles
3rd Round :
Data structure for setting data for recommendation engine
CI/CD
Docker containerization
Singleton design pattern
Abstract classes

4th Round :
Heap dump analysis
Thread dump analysis
Stop the world GC
Lock in Mutithreading
question I don't remember, it was on DP
e-commerce site design
REJECTED after final round

LensKart 2019 :-
   1.  Immutable classes & usage
   2. If an object is mutable in immutable classes how to fix that
   3. producer consumer problem of mutithreading
   4. how to remove deadlock in java
   5. challenges in microservices
   6. printing sum of child to parent node ( code )
   7. finding the 2nd max element from stream -- max heap (code)
   8. compareTo method overriden with multivalue to compare.
   
Rejected after 1st round because of java knowledge

Zomato 2019 :-
1st Round :-
Number of island in a matrix -- https://www.geeksforgeeks.org/find-number-of-islands/  (code)
Design a tinyUrl service
Mysql db replication 
Some db queries for 2nd max etc
Indexes in db discussion
Tech discussion for golang and java


2017 -- full stack developer role :-

1st Round :- Hacker rank
 1. String encoding -- aabbbccc transcode into a2b3c3
 2. Knapsack problem  of dynamic programming.

2nd Round :- Coder Pad
 1.  Given an array with numbers, find the pair of integers where sum is some number (0 sum is the base case where my test case failed) 
 2.  One more question I forgot

3rd Round :- F2F in Bangalore
 1. Department, Student and faculty db design -- find the 2nd max student with marks from CS department.

2. Writing queries using ORM
3. Communication between threads like wait and notify, race condition etc.
not remember much from this round

4th Round :-
 1. Authentication system design.
 2. Addition of cache framework.
 3. Load Balancer working.
 4. Design custom cache.

5th round :-
 1. Exception cases.
 2. Angular questions related to providers, services etc.
 3. Design Parking lot

Not selected

2018 -- Backend Associate 

1st round :- Hackerrank
Questions don't remember

2nd Round :- coderpad
 1. check that if any subarray with given sum exists.
 2. Monday -1 ... Sunday -7 , decode the working day from a given number

3rd round (telephonic) :-
 1, Explaination of projects
 2. Thread Safe classes -- singleton and synchronized 
 3. monitor lock in java
 4. producer consumer problem
 5. Treemap vs Hashmap internal difference

4th Round :- f2f (banglore)
 1, Explaination of projects
 2. Design your own custom Hashmap. (Custom java map)
 3. custom put and get 
 4. Stream of objects are coming with stock value in rs and a given time, you need to find the highest stock value in a given time frame t1 and t2. (Binary searchig on time)
  Changed the question if you need to find the top 5 stocks at any time. (Max heap) 
5. Find the maximum value from stack.

5th round :- f2f 
 1. Process a big file of more than 30 GB on a single machine (he was south indian maniac didn't wanted to hire any north indian) 
2. Define machine learning, recommendation engine.

Not selected

GS bar is very-2 high and interview process is a mamoth

Morgan Stanley :-

2014

Round 1 :- hacker rank
1. find number of common elements in two arrays count.
2. Dont remember but was quiet tough question

Round 2 :-
 1. Parking lot problem
 2. Implementing Stack using 2 queues
 3. Merge sort in linkedlist.

Not selected

<hr>

**Intro**

         I'm working as a Senior Application Developer with Oracle with Customer Data Integrations Team. My role involves multiple responsibilities like to design and develop the tools and applications for multiple teams within Oracle Application Labs. I have developed multiple applications with different technologies like Java, pl/sql and implemented the CI/CD pipeline as well.
         
 