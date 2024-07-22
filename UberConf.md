Automated Software Refactoring
  1. Use Open Rewrite to create recipies for your project or you can use from the set of avaialble recipies
  2. Recipies are nothing but set of rules/operations that you can apply on your code to perform say a migration operation.
     - Recipies can be written in multiple languages including Java
  3. On top of that Moderne also provides AI capabilities to enhance the process
  4. You can connect your repository to their service and then you can start appying the recipies written on your project or dry run, analyze results and review the changes and you can even commit the changes from here
  5. Can be used in vaious scenarios including migration, addressing security vulnerabilities, SonarQube issues etc

2. Architectural Patterns: Messaging

3. Patterns for Microservices
   - Usual literature on Monoliths are not inherently bad and microservices the only right solution. Strong emphasis on Monolith vs Microservice decision should be based on business needs.
   - Cases for microservice
      - Business Agility. If business needs changes frequently.
      - Separation of Concerns. The domain 
      - Different part of the app has different architectural needs. (for example a certain part of the app needs more emphasis security, another part needs more performance and a different part needs extreme scale)
      - Business revenue should justify building microservices since building one is costly      
   - Common pitfalls
     -  Microservices should not make fine-grained call to other microservices. What it means is if a service makes a call to another service it should be able to complete the transaction with that response. Should not be going back-and-forth to get information to complete the transaction. This would also mean fewer network calls and decreased latency
     - Business requirement should drive technology decisions. For example, Why synchronous vs Asynchronous? If synchronous satisfies your business req, stick with it because it is simpler to implement and debug.
     - Use appropriate version numbers. Also consider versioning your entity.
     - Handle network failures gracefully so you can build a resilient system. Never make calls without specifying timeouts. Always use techniques like Circuit breaker
     - 
     - 
            
4. Becoming an Architect

5. Scaling up with Virtual Threads

6. Learn to Think Functionally
   - Lot of talk about the evolution of 
      
7. Intelligent Spring Applications
    - Went in with a different expectation but this was mostly about using Spring libraries to connect to OpenAI. This is still the begining phase but nice to know kind of thing. 
    - 
8. Mastering Solutions

9. Creating and Maintaining Architectural Fitness Functions
    - This talk was mostly about how to maintain the architectural integrity of the project
    - String emphasis on Getting Feedback which is the base of Agile development. Some example of Feed back are Junit, SonarQube etc which gives you feedback about the integrity and quality of the code 
    - Employing techniques like ArchUnit (JUnit style code) to write the Architectural objectives of the project and even making it part of your CI Build
    - Adivsed to cleanup warning on the project (examples of warnings being actual bug in the code)
    - String emphasis on maintaining code coverage, atleast start by establishing the current base line and failing CI builds if we fall below that percentage and slowly building on top of it.
    - Strong emphasis on TDD
    
10. Agile Architecture
    - 
11. Coding Slow And Fast
    - This is more of a theoritical session where he talked about how to work efficiently
    - Talked about how out brain works, fast (section 1, more intuitive) and slow (section 2, more analytical).
    - How to engage slow/section 2 of the brain by cutting out distractions, avoiding multi tasking, blocking calendar, employing techniques like Pomodoro.
    
12. Multithreading Vs Asynchronous Programming
    - Talk centered around the how early multi threading worked and then when it became blocking and hanging on to resource and ultimately creating deadlocks making it tricky to use. Then with parallel(stream)/concurrent programming(CompletableFuture) it was better until we had to handle exceptions. The functional approach made handling exceptions difficult. With virtual threads(similar to async/await in JS) since Java 21, the structure of asynvhronous imperative style code started to look more like synchronous imperative style coding.
    - A lot of emphasis on immutability of objects in functional programming.
    - String emphasis on TDD.
