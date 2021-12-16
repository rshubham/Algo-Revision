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
    
+ Mediator
+ Chain of Responsibility
+ Command
+ Strategy
+ Observer