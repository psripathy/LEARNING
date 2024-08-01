### Automated Software Refactoring
  1. Use Open Rewrite to create recipies for your project or you can use from the set of avaialble recipies
  2. Recipies are nothing but set of rules/operations that you can apply on your code to perform say a migration operation.
     - Recipies can be written in multiple languages including Java
  3. On top of that Moderne also provides AI capabilities to enhance the process
  4. You can connect your repository to their service and then you can start appying the recipies written on your project or dry run, analyze results and review the changes and you can even commit the changes from here
  5. Can be used in vaious scenarios including migration, addressing security vulnerabilities, SonarQube issues etc

### Architectural Patterns: Messaging
  #### Domain Driven Design (DDD)
  1. Ubiqutous Language (Helps define the *Problem Space*)
     - Identify your business language by talking to domain experts and figure out the language they use like what do they call a certain process.
     - Getting these formal terms down basically describes the business model. For example you can identify what a User/Quote means and what a booking means
  2. Create Bounded Context (*Solution Space*)
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
         - Contains application/system specific logic like validating user security, calling domain services passing the domain objects
         - Makes use of repositories

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
