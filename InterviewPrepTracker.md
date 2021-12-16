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

### Design Patterns:

+ Singleton - Implementation of all types.
+ Factory Pattern
+ Abstract Factory
+ **Builder** : when the Object contains a lot of attributes, and some params are optional to send.
+ **Prototype** : used when the Object creation is a costly affair and requires a lot of time and resources and you have a similar object already existing.
+ **Adapter** 
    
    + [Good Example](https://www.dofactory.com/net/adapter-design-pattern)
    + Understand with example of Outbound Call - 
    + Target as Outbound Call
    + Adapter as WebserviceCallAdapter; gRPCCallAdapter; KafkaProducerCallAdapter; RabbitMQCallAdapter;
    + Adaptee as Webservice; gRPC; KafkaProducer; RabbitMQ;
    + This could be used in making a call to different services in Microservices.
    + Citi-Direct: BSI Layer acted as Target - Multiple Adapters like Kafka/MQ/Job/OutboundCalls.
    
    ![alt text](https://github.com/rshubham/Revision_Notes/blob/master/Design_Pattern_Images/Adapter.jpeg)
    
+ **Composite** 
        
     + [Good Example](https://www.dofactory.com/net/composite-design-pattern)
     +  Understand with Org Heirarchy Structure - 
     +  Component as Employee
     +  Composite as Manager
     +  Leaf as Engineer / Architect / Assistant / BA etc. (IC roles)
     
     ![alt text](https://github.com/rshubham/Revision_Notes/blob/master/Design_Pattern_Images/Composite.jpeg)
     
+ **Facade** 

     + [Good Example](https://www.journaldev.com/1557/facade-design-pattern-in-java)
     + Facade as Logical Interface of multiple Interfaces/Objects
     + **Subsystem interfaces are not aware of Facade and they shouldn’t have any reference of the Facade interface.**
     + **Facade design pattern is more like a helper for client applications, it doesn’t hide subsystem interfaces from the client. Whether to use Facade or not is completely dependent on client code.**
     + **Applied on Similar kind of Interfaces**
     + Subsystem Interfaces as Interfaces/Classes/Objects
     + Example : If I want to call LocationService, I can directly call Location Service or via Class/Interface called IntegrationService. IntegrationService will route my request to LocationService.
     + For understanding - In OT - We can directly call - BI Reports also for triggering the BI Job but we call OIH/CIP which acts as a Facade to route the request to multiple service. It's our choice to use it or not.
     
+ **Proxy** 

    + [Good Example](https://www.dofactory.com/net/proxy-design-pattern)
    + Can be understood as - DB-Proxy for MISCDH Schema
    + Proxy as NamedAccountDBProxy 'is a' DBAccount and 'has a' MISCDHAccount, example: snrohill[MISCDH]
    + Subject as DBAccount <Interface/Abstract Class> example: GSI DB Account
    + Real Subject as MISCDHAccount 'is a' DBAccount example: MISCDH
    + **maintains a reference that lets the proxy access the real subject**
    + **controls access to the real subject and may be responsible for creating and deleting it.**


+ **Decorator**

    + [Good Example](https://www.dofactory.com/net/decorator-design-pattern)
    + Can be understood as - MovieTicketBooking or any general Ticket Booking
    + Component as MovieTicketBooking - Interface/Abstract Class - has a root functionality to book() ticket.
    + Concrete Component as Online Booking/Offline Booking etc.
    + Decorator as BookingAdditionals - Interface/Abstract Class - 'is a' MovieTicketBooking.
    + Concrete Decorator as AddRefreshments - 'is a' MovieTicketBooking, with functionality as book(), addRefreshments(); we can add more Decorators like this.
    + **Decorator design pattern is helpful in providing runtime modification abilities and hence more flexible. Its easy to maintain and extend when the number of choices are more.**
    + **The disadvantage of decorator design pattern is that it uses a lot of similar kind of objects (decorators).**
    + **Decorator pattern is used a lot in Java IO classes, such as FileReader, BufferedReader etc.**
    
    + Movie Ticket Booking Decorator Example:
    
    ![alt text](https://github.com/rshubham/Revision_Notes/blob/master/Design_Pattern_Images/Decorator_MovieTicketBooking.jpeg)
    
    + Library Item Decorator Example :
    
    ![alt text](https://github.com/rshubham/Revision_Notes/blob/master/Design_Pattern_Images/Decorator_LibraryItem.jpeg)
         
    
+ Template Method
+ Mediator
+ Chain of Responsibility
+ Command
+ Strategy
+ Observer

<hr>

### SQL/PLSQL

<hr>

### Projects (Deploy all these projects in Azure VM instance)

1. [Azure Link](https://portal.azure.com/#home)
2. Azure Credentials: shivam.lynux@outlook.com/Shiv_2108

   + Spring Boot / Spring Framework: 

        + Develop REST endpoints for an application using Spring Boot.
        
        + RockPaperScissors Game using SpringBoot Rest: https://github.com/rshubham/RockPaperScissorsGame
   
        + Spring Security and JWT: 
        + Spring Security and OAuth 
        
   + Kafka
   
   + Camel
   
   + Storm

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
