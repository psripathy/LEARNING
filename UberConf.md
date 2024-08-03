### Automated Software Refactoring
  1. Use Open Rewrite to create recipies for your project or you can use from the set of avaialble recipies
  2. Recipies are nothing but set of rules/operations that you can apply on your code to perform say a migration operation.
     - Recipies can be written in multiple languages including Java
  3. On top of that Moderne also provides AI capabilities to enhance the process
  4. You can connect your repository to their service and then you can start appying the recipies written on your project or dry run, analyze results and review the changes and you can even commit the changes from here
  5. Can be used in vaious scenarios including migration, addressing security vulnerabilities, SonarQube issues etc

### Architectural Patterns: Messaging

[ArchitecturalPatternsFocusMessaging.pdf](https://github.com/user-attachments/files/16476138/ArchitecturalPatternsFocusMessaging.pdf)
  #### Domain Driven Design (DDD)
  1. Ubiqutous Language (Helps define the **Problem Space**)
     - Identify your business language by talking to domain experts and figure out the language they use, like what do they call a certain process.
     - Getting these formal terms down basically describes the business model. For example you can identify what a User/Quote means and what a Booking means
  2. Create Bounded Context (**Solution Space**)
     - This is the technical solution space where we create solutions for items from the problem space
     - Identify Domains & Sub domains from the UL.
       - Domain
         - Represents the business problem. eg. Vehicle
       - Sub Domain
         - Smaller division of Domain. For ex. Quote, Order
         - Sub domains have explicit reponsibilities and does only 1 thing so we can draw boundaries around them called bounded context        
     - Bounded context will have
       - Value Objects (Domain Object)
         - Immutable Records. VO help reduce primitive obsession
       - Entities (Domain Object)
       - Aggregate Relationship
         - Manages cluster of domain objects. Think a class Album { private Artist artist, private List<Track> tracks;}
         - Transactions should not cross aggregate boundaries.
       - Domain Services
         - Stateless objects that implements domain/business logic. Ex. Calculate tax rate for the order.
       - Application Services
         - Contains application/system specific logic like validating user security, calling domain services passing them domain objects.
         - Makes use of repositories.
  3. DDD by EventStorming
     - Brainstorm to model business process
     - Identify series of domain events over a timeline. The model is enhanced with additional concepts by identifying actors, commands, external systems etc. These elements should tell a story about how the business process works.
     - Step 1: Identifying Events(Flow)
       - Identify events that happen in the business and represent them in the past. eg. Request Submitted, Req Approved, Req Declined, Order Received, Order Shipped, Order Cancelled.
       - Represent the events in a Kanban flow (Events can be separated into groups here).
       - Also identify the Paint points if any with any given event.
       - Identify logical/pivotal events of the business flow and with that you will be able to create a swim lane diagram based on the pivotal events. eg. Shopping Cart Initialized[...] -> Order Initialized[...] -> Order Shipped[...] -> Order Received[...]
       - The swimming lane will become boundaries of your microservices.
       - This can also give you idea about what becomes messages.
     - Step 2:
       - Identify the **Actor** and **Command** that will start the events
       - **Policy** - automation that triggers the event based on the command. eg. For a Submit Order command that arrives as a message the policy(as a microservice) will then decide to call another service Ship Order 
      ![image](https://github.com/user-attachments/assets/4414e4df-9822-4687-b621-41703cc25e52)

        *Blue - Command*, *Orange - Events*, *Pink - Policy*

  4. Event Sourcing - Why events are used as messages?
     - Problem with traditional approach is with the CRUD databases when something changes records get overwritten, so no log of previous information.
     - Events are recorded on **append only** store (hence immutable) so you can go back in time to see what lead to the current state.
       ![image](https://github.com/user-attachments/assets/80959d9f-d864-4b25-b93e-cfecd71e886e)
     - TradeOffs
       - Eventual Consistency
       - Might be overkill if you don't need audit trails, history, rollback
         
  5. Event Driven Architecture (EDA)
     - System components communicate asynchronously by exchanging event messaging (publish-subscribe)
     - EDA vs Event Sourcing
       - EDA = Communication between services
       - Event Sourcing = Happens inside a service. Events designed for event sourcing represent state transitions implemented inside the service.
                    
   6. Claim Check
      - Messaging systems cannot handle large payloads
      - Solution:
        - Send a **Claim check** (an identifier) to the messaging sytem and store the payload in an external storage.
        - Send the Claim check in the message to the message broker.
        - The consumer of the message will use the Claim Check to retrive the message.
          
   7. Types of Messages - Event Vs Event Notification Vs ECST Vs Command
       - **Event**
         - Message that describes a significant change or occurance already happened.
         - Can be critical for system operation and can trigger workflow or state changes.
         - Eg. Order placed - Other services like inventory, billing, shipping should react.
         - An event cannot be cancelled.
         - Structure of event message.
         - ![image](https://github.com/user-attachments/assets/2585b9b3-6f17-494f-bc87-5a7be0dcd544)
           
       - **Event Notification**
         - Message that primarily informs subscribers of generally less critical events.
         - Primarily for awareness, logging or optional actions.
         - Eg. Payroll published.
    
       - **Event carried State Transfer (ECST)**
         - Event that carries full state/updated fields of the entity enabling (and expected) subscribers to update their state based on the event.
         - Allows consumers to cache entity state (as aggregate), which can also make consumers fault tolerant because the consumers can funtion with cached data even if the producer goes down.
         - eg. Product price or inventory level changed and all services need to update their local state.

       - **Domain Events**
         - Halfway between Event Notifications and ECST but not intended to describe aggregate state.
         - To capture and communicate changes in domain model and subscribers may update domain state, trigger workflows or handle side effects.
         - eg. A customers address has changed and you may need to trigger additional events for that rather than just a synchronization of price as in ECST.
                       
       - **Command**
         - Message that describes an operation that has to be carried out.
         - Command can be rejected.
        
   8.Materialized View
     - Are Database objects that physically store the results of the query allowing faster reads and complex aggregations.
     - eg. When order is placed an event is published to event broker which the consumer is listening for and updates it's materialized view (order count for the customer state, think woot selling map).
     
   9. CQRS (Command & Query Responsibility Seggregation)
      - Seperation of READ & write databases.
      - Write to write only DB and event streaming updates the READ database .
      
### Patterns for Microservices
   - Usual literature on Monoliths are not inherently bad and microservices is not the solution for all cases. Strong emphasis on Monolith vs Microservice decision should be based on business needs.
   - Cases for microservice
      - Business Agility. If business needs changes frequently.
      - Separation of Concerns.
      - Different part of the app has different architectural needs. (for example a certain part of the app needs more emphasis security, another part needs more performance and a different part needs extreme scale)
      - Business revenue should justify building microservices since building one is costly      
   - Best Practices
     -  Microservices should not make fine-grained call to other microservices. What it means is if a service makes a call to another service it should be able to complete the transaction with that response. Should not be going back-and-forth to get information to complete the transaction. This would also mean fewer network calls and decreased latency.
     - Business requirement should drive technology decisions. For example, Why synchronous vs Asynchronous? If synchronous satisfies your business req, stick with it because it is simpler to implement and handle errors/exception. Also the technology used matters which changes this. For example Asynchronous programming in Java 21 is simpler which changes the equation.
     - Handle network failures gracefully so you can build a resilient system. Never make calls without specifying timeouts. Always use techniques like Circuit breaker
     - Performance - Question should always be is it adequate and not super fast?
     - Scalability - Not every system needs huge scale. Evaluate and keep things simple to adequately address business needs. For example a broker pattern/Choreography is highly scalable vs an Orchestrator which may be less scalable but easy to implement and handle error.
     - Create ADR (Architecture Decision Records), very important. Capture all the Non Functional Reqs like Performance/Scalability in hard numbers. This can be evaluated periodically.
     - Sharing DB is a no-no. Don't expose your database but instead share your data. Deal the data consistency issues with eventual consistency.
     - Immediate Consistency, Availability & Fault Tolerance cannot all be provided. They are mutually exclusive - CAP Theorem.
     - Business transactions(long running) should be stitched together using technical transactions(short) - SAGA pattern. Handle Failures using Retries/Compensating transactions.
     - Make the services immutable. For updated/new versions of service bring the new services up as seperate instance before killing the current service.
            
### Becoming an Architect

### Scaling up with Virtual Threads

### Learn to Think Functionally
   - Lot of talk about the evolution of 
      
### Intelligent Spring Applications
    - Went in with a different expectation but this was mostly about using Spring libraries to connect to OpenAI. This is still the begining phase but nice to know kind of thing. 
      
### Mastering Solutions

### Creating and Maintaining Architectural Fitness Functions
    - This talk was mostly about how to maintain the architectural integrity of the project.
    - Create ADR (Architecture Decision Records)
    - Strong emphasis on Getting Feedback which is the base of Agile development. Some example of Feed back are Junit, SonarQube etc which gives you feedback about the integrity and quality of the code 
    - Employing techniques like ArchUnit (JUnit style code) to write the Architectural objectives of the project and even making it part of your CI Build
    - Adivsed to cleanup warning on the project (examples of warnings being actual bug in the code)
    - Strong emphasis on maintaining code coverage, atleast start by establishing the current base line and failing CI builds if we fall below that percentage and slowly building on top of it.
    - Strong emphasis on TDD
    
### Agile Architecture
    - 
### Coding Slow And Fast
    - This is more of a theoritical session where he talked about how to work efficiently
    - Talked about how out brain works, section 1 (fast, more intuitive) and section 2 (slow but more analytical).
    - How to engage section 2 of the brain by cutting out distractions, avoiding multi tasking, blocking calendar, employing techniques like Pomodoro.
    
### Multithreading Vs Asynchronous Programming
    - Talk centered around the how early multi threading worked and then when it became blocking and hanging on to resource and ultimately creating deadlocks making it tricky to use. Then with parallel(stream)/concurrent programming(CompletableFuture) it was better until we had to handle exceptions. The functional approach made handling exceptions difficult. With Java 21 virtual threads(similar to async/await in JS), the structure of asynchronous imperative style code started to look more like synchronous imperative style coding.
    - A lot of emphasis on immutability of objects in functional programming.
    - Strong emphasis on TDD.
