## Design Patterns:

<hr>

### Creational Pattern

+ Singleton - Implementation of all types.
+ Factory Pattern
+ Abstract Factory
+ **Builder** : when the Object contains a lot of attributes, and some params are optional to send.
+ **Prototype** : used when the Object creation is a costly affair and requires a lot of time and resources and you have a similar object already existing.

<hr>

### Structural Pattern

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
         
<hr>

### Behavioral Pattern
    
+ **Template Method**

    + [Good Example](https://www.journaldev.com/1763/template-method-design-pattern-in-java)
    + Can be understood as BatchProcessing in OT
    + Template as DataImport
    + Implementation as Import Mgmt, FBDI or we can say BI Report
    + **All non-abstract methods of java.io.InputStream, java.io.OutputStream, java.io.Reader and java.io.Writer.**
    + **Template method should consists of certain steps whose order is fixed and for some of the methods, implementation differs from base class to subclass. Template method should be final.**
    + **Methods in base class with default implementation are referred as Hooks, and they are intended to be overridden by subclasses, if you want some methods to be not overridden, you can make them final, for example in our case we can make buildFoundation() method final because if we don’t want subclasses to override it.**
    + OT Batch Template Method Example with Adapter Structure:
    
    ![alt text](https://github.com/rshubham/Revision_Notes/blob/master/Design_Pattern_Images/TemplateMethod.jpeg)
    
+ **Mediator**

    + [Good Example](https://www.journaldev.com/1730/mediator-design-pattern-java)
    + Can be understood a multiple services having dependencies on each other thus creating tight coupling between them. We can take example of BookingService and Location Service.
    + Mediator as ParkingIntegrationService
    + Mediator Concrete as BookingLocationIntegrator 'is a' ParkingIntegrationService.
    + Colleague Classes as BookingService and LocationService - who are inter-dependent.
    + **Mediator promotes loose coupling by keeping objects from referring to each other explicitly, and it lets you vary their interaction independently.**
    + **Example in JDK**
     
      + java.util.Timer class scheduleXXX() methods
      + Java Concurrency Executor execute() method.
      + java.lang.reflect.Method invoke() method.
    + **Java Message Service (JMS) uses Mediator pattern along with Observer pattern to allow applications to subscribe and publish data to other applications.**
    + **We should not use mediator pattern just to achieve lose-coupling because if the number of mediators will grow, then it will become hard to maintain them.**
    + My Example - BookingService and LocationService
    
    ![alt text](https://github.com/rshubham/Revision_Notes/blob/master/Design_Pattern_Images/Mediator.jpeg)

+ **Chain of Responsibility**

    + [Good Example 1](https://www.journaldev.com/1617/chain-of-responsibility-design-pattern-in-java)
    + [Good Example 2](https://www.dofactory.com/net/chain-of-responsibility-design-pattern)
    + Can be understood as Functionality of Role Based Approval System
    + Chain Handler as RequestApprover 
    
        + approve()
        + reject()
        + setNextApprover(RequestApprover approver)
        + RequestApprover approvalChain;
        
    + Concrete Handler as FirstLevelApprover, SecondLevelApprover,..., NthLevelApprover
    + Client as Client who will call Handler
    + **Every object in the chain should have reference to the next object in chain to forward the request to, its achieved by java composition.**
    + **Chain of Responsibility design pattern is good to achieve lose coupling but it comes with the trade-off of having a lot of implementation classes and maintenance problems if most of the code is common in all the implementations.**
    + **Examples in Java**
    
        + java.util.logging.Logger#log()
        + javax.servlet.Filter#doFilter()
        
    + **Comments** 
    
        + You may set or change the next handler during runtime. You also may not know beforehand which are the handlers that should be used, allowing the client to set them as desired. As an example, you could have many Validator classes which can be called in a certain order. But that depends on the validation. So you apply CoR and make good use out of the possibility of combining different validators ordered in so many different ways. Suppose you want to validate an email address. You need to check if the e-mail is correctly formed, if it exists, and if contains bad words. To do this job, you may have three different classes, and you can arrange them in any order – so you might as well let the client decide its own priority.
        + I commonly see that there is repeated code in the concrete classes just like the implementation of your dispense methods. The intent of this design pattern is nice, but dont forget the DRY principle and it is a must in my humble opinion. I always use abstract classes for cor design pattern to eliminate duplicate code.
    
    + **Examples**
    
        + Approver System
        
     ![alt text](https://github.com/rshubham/Revision_Notes/blob/master/Design_Pattern_Images/ChainOfResponsibility_Approver.jpeg)
     
    + BatchProcessor System
                
      ![alt text](https://github.com/rshubham/Revision_Notes/blob/master/Design_Pattern_Images/ChainOfResponsibility_BatchProcessor.jpeg)

+ **Command**

    + [Good Example](https://www.journaldev.com/1624/command-design-pattern)
    + Can be understood as TV-Remote Command Example.
    + Invoker as TVRemoteControl
    + Command as TVCommand - Interface/Abstract Class
    + Concrete Command as TurnTVOnCmd, TurnTVoffCmd, TurnVolUpCmd, etc. 'is a' TV Command and 'has a' 'TV'
    + Receiver as TV 
        
        + turnOn()
        + turnOff()
        + turnVolUp()
        + turnVolDown()
    
    + **Command implementation classes chose the method to invoke on receiver object, for every method in receiver there will be a command implementation. It works as a bridge between receiver and action methods.**
    + **The drawback with Command design pattern is that the code gets huge and confusing with high number of action methods and because of so many associations.**
    + **Runnable interface (java.lang.Runnable) and Swing Action (javax.swing.Action) uses command pattern.**
    + Example
        
        + Generic
        
        ![alt text](https://github.com/rshubham/Revision_Notes/blob/master/Design_Pattern_Images/Command_Generic.jpeg)
        
        + TV Example
        
        ![alt text](https://github.com/rshubham/Revision_Notes/blob/master/Design_Pattern_Images/Command_TV.jpeg)
        
        + Runnable Example
        
        ![alt text](https://github.com/rshubham/Revision_Notes/blob/master/Design_Pattern_Images/Command_Runnable.jpeg)
        
+ **Strategy**

    + [Good Example 1](https://www.journaldev.com/1754/strategy-design-pattern-in-java-example-tutorial)
    + [Good Example 2](https://www.dofactory.com/net/strategy-design-pattern)
    + Strategy pattern is used when we have multiple algorithm for a specific task and client decides the actual implementation to be used at runtime.
    + We define multiple algorithms and let client application pass the algorithm to be used as a parameter.
    + One of the best example of strategy pattern is Collections.sort() method that takes Comparator parameter. Based on the different implementations of Comparator interfaces, the Objects are getting sorted in different ways.
    + This can be understood as Payment Service Example
    + Strategy as PaymentStrategy - what way to make payment?
    + Concrete Strategy - Cash/Card/UPI/Paypal/Wallet/Crypto
    + CalledObject - the object on which we need to implement a strategy on.
    + **We could have used composition to create instance variable for strategies but we should avoid that as we want the specific strategy to be applied for a particular task. Same is followed in Collections.sort() and Arrays.sort() method that take comparator as argument.**
    + **Strategy Pattern is very similar to State Pattern. One of the difference is that Context contains state as instance variable and there can be multiple tasks whose implementation can be dependent on the state whereas in strategy pattern strategy is passed as argument to the method and context object doesn’t have any variable to store it.**
    + **Example**
    
        + Sorting
        
         ![alt text](https://github.com/rshubham/Revision_Notes/blob/master/Design_Pattern_Images/Strategy_Sort.jpeg)
         
         + PaymentService with Decorator Pattern
         
         ![alt text](https://github.com/rshubham/Revision_Notes/blob/master/Design_Pattern_Images/Strategy_Payment_Decorator.jpeg)

+ **Observer** 

    + [Good Example](https://www.journaldev.com/1739/observer-design-pattern-in-java)
    + Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
    + Can be understood a Publish-Subscribe Pattern, where multiple entities are there to subscribe and publish events.
    + Subject as Order/booking Service Interface
    + Concrete Subject as ScheduledOrder/OfflineOrder 'is a' Order/Booking
    + Observer as NotificationService; PaymentService; InventoryService; DeliveryService;
    + Concrete Observer - concrete implementation of Observer.
    + Subject can:
    
        + register(Observer observer);
        + unregister(Observer observer);
        + notifyObservers();
        + getUpdates(Observer observer);
        
    + Observer can:
    
        + setSubject(Subject subject);
        + update()
        
    + **Java provides inbuilt platform for implementing Observer pattern through java.util.Observable class and java.util.Observer interface.**
    + **Java Message Service (JMS) uses Observer design pattern along with Mediator pattern to allow applications to subscribe and publish data to other applications.**
    + **Model-View-Controller (MVC) frameworks also use Observer pattern where Model is the Subject and Views are observers that can register to get notified of any change to the model.**
    + **Implementation in Java**
    
        + java.util.EventListener in Swing
        + javax.servlet.http.HttpSessionBindingListener
        + javax.servlet.http.HttpSessionAttributeListener
        
    + **Example**
    
        + Ecommerce Implementation
        
        ![alt text](https://github.com/rshubham/Revision_Notes/blob/master/Design_Pattern_Images/Observer_Ecom_Example.jpeg)
        
        + (Java) Messaging Service - my Design for Observer
        
        ![alt text](https://github.com/rshubham/Revision_Notes/blob/master/Design_Pattern_Images/Observer_MyDesign_JMS.jpeg)
        