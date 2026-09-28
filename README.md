# **🧠 Low-Level Design — Zero →  Interview Ready**

A structured journey from **OOP fundamentals → design principles → design patterns → domain modeling → clean architecture → concurrency → machine coding → real-world LLD problems → interview mastery**.

**Learning approach:** Every topic is learned from first principles, followed by real-world examples, Java implementation, design trade-offs, common mistakes, interview questions, and practical exercises.

## **🗺️ Curriculum**

```
🧠 LOW-LEVEL DESIGN — ZERO → 60+ LPA INTERVIEW READY
│
├── 00. LLD FOUNDATIONS
│   ├── 00.1 What is LLD?                              [30 min]     ✅
│   ├── 00.2 HLD vs LLD                               [30 min]      ✅
│   ├── 00.3 Why LLD Exists                           [30 min]      ✅
│   ├── 00.4 Requirements → Design                    [45 min]      ✅
│   ├── 00.5 Functional vs Non-Functional Requirements [30 min]     ✅
│   ├── 00.6 Identifying Objects & Responsibilities   [45 min]      ✅
│   ├── 00.7 Abstraction & Modeling                  [45 min]       ✅
│   └── 00.8 LLD Interview Approach                  [1 hr] ⭐      ✅
│
├── 01. OBJECT-ORIENTED PROGRAMMING
│   ├── 01.1 Class & Object                            [45 min]     ✅
│   ├── 01.2 State & Behavior                          [30 min]     ✅
│   ├── 01.3 Encapsulation                             [45 min]     ✅
│   ├── 01.4 Abstraction                               [45 min]     ✅
│   ├── 01.5 Inheritance                               [45 min]     ✅
│   ├── 01.6 Polymorphism                              [1 hr]       ✅
│   ├── 01.7 Composition                               [1 hr] ⭐    ✅
│   ├── 01.8 Association / Aggregation / Composition   [1 hr]       ✅
│   ├── 01.9 Interface vs Abstract Class              [45 min]      ✅
│   ├── 01.10 Favor Composition Over Inheritance      [45 min] ⭐   ✅
│   └── 01.11 SOLID-Friendly OOP                      [1 hr]        ✅ 
│
├── 02. UML & DESIGN REPRESENTATION
│   ├── 02.1 Why UML?                                  [20 min]     ✅ 
│   ├── 02.2 Class Diagram                             [1 hr] ⭐    ✅ 
│   ├── 02.3 Object Diagram                            [30 min]     ✅
│   ├── 02.4 Sequence Diagram                          [1 hr] ⭐    ✅
│   ├── 02.5 Activity Diagram                          [45 min]     ✅
│   ├── 02.6 State Diagram                             [45 min]⭐   ✅
│   ├── 02.7 Dependency Relationships                  [45 min]     ✅
│   ├── 02.8 Mermaid for GitHub                        [30 min]
│   └── 02.9 Reading Diagrams in Interviews            [30 min]
│
├── 03. DESIGN PRINCIPLES
│   ├── 03.1 Single Responsibility Principle           [1 hr] ⭐
│   ├── 03.2 Open/Closed Principle                     [1 hr] ⭐
│   ├── 03.3 Liskov Substitution Principle             [1 hr] ⭐
│   ├── 03.4 Interface Segregation Principle           [1 hr] ⭐
│   ├── 03.5 Dependency Inversion Principle             [1 hr] ⭐
│   ├── 03.6 DRY                                      [30 min]
│   ├── 03.7 KISS                                     [30 min]
│   ├── 03.8 YAGNI                                    [30 min]
│   ├── 03.9 Separation of Concerns                   [45 min]
│   ├── 03.10 Law of Demeter                          [45 min]
│   ├── 03.11 Tell, Don't Ask                         [45 min]
│   ├── 03.12 Program to an Interface                 [45 min]
│   └── 03.13 Principle Trade-offs                    [1 hr] ⭐
│
├── 04. COUPLING, COHESION & CODE QUALITY
│   ├── 04.1 What is Coupling?                         [45 min]
│   ├── 04.2 Types of Coupling                         [45 min]
│   ├── 04.3 What is Cohesion?                         [45 min]
│   ├── 04.4 High Cohesion / Low Coupling              [1 hr] ⭐
│   ├── 04.5 Dependency Management                     [45 min]
│   ├── 04.6 Immutability                              [45 min]
│   ├── 04.7 Side Effects                              [30 min]
│   ├── 04.8 Maintainability                           [30 min]
│   └── 04.9 Extensibility                             [45 min]
│
├── 05. CREATIONAL DESIGN PATTERNS
│   ├── 05.1 Why Creational Patterns?                  [30 min]
│   ├── 05.2 Factory Method                            [1 hr] ⭐
│   ├── 05.3 Abstract Factory                          [1 hr]
│   ├── 05.4 Builder                                   [1 hr] ⭐
│   ├── 05.5 Prototype                                 [45 min]
│   ├── 05.6 Singleton                                 [1 hr] ⭐
│   └── 05.7 Pattern Selection & Trade-offs            [1 hr] ⭐
│
├── 06. STRUCTURAL DESIGN PATTERNS
│   ├── 06.1 Adapter                                   [1 hr] ⭐
│   ├── 06.2 Decorator                                 [1 hr] ⭐
│   ├── 06.3 Facade                                   [45 min] ⭐
│   ├── 06.4 Proxy                                    [1 hr] ⭐
│   ├── 06.5 Composite                                 [1 hr]
│   ├── 06.6 Bridge                                   [1 hr]
│   ├── 06.7 Flyweight                                [45 min]
│   └── 06.8 Pattern Selection & Trade-offs            [1 hr]
│
├── 07. BEHAVIORAL DESIGN PATTERNS
│   ├── 07.1 Strategy                                 [1 hr] ⭐
│   ├── 07.2 Observer                                 [1 hr] ⭐
│   ├── 07.3 Command                                  [1 hr] ⭐
│   ├── 07.4 State                                    [1 hr] ⭐
│   ├── 07.5 Chain of Responsibility                  [1 hr] ⭐
│   ├── 07.6 Template Method                          [45 min]
│   ├── 07.7 Iterator                                [45 min]
│   ├── 07.8 Mediator                                [45 min]
│   ├── 07.9 Memento                                [45 min]
│   ├── 07.10 Visitor                                [1 hr]
│   └── 07.11 Null Object                            [30 min]
│
├── 08. DESIGN PATTERN APPLICATION
│   ├── 08.1 Pattern vs Principle                     [45 min] ⭐
│   ├── 08.2 Combining Multiple Patterns              [1 hr] ⭐
│   ├── 08.3 Avoiding Overengineering                 [45 min] ⭐
│   ├── 08.4 Identifying Patterns from Requirements   [1 hr] ⭐
│   └── 08.5 Refactoring Bad Designs                  [1.5 hr] ⭐
│
├── 09. DOMAIN MODELING
│   ├── 09.1 Entities                                  [45 min] ⭐
│   ├── 09.2 Value Objects                             [45 min] ⭐
│   ├── 09.3 Aggregates                                [1 hr] ⭐
│   ├── 09.4 Aggregate Roots                           [45 min]
│   ├── 09.5 Domain Services                           [45 min]
│   ├── 09.6 Repositories                             [45 min]
│   ├── 09.7 Domain Events                             [1 hr] ⭐
│   ├── 09.8 Invariants                                [1 hr] ⭐
│   └── 09.9 Rich vs Anemic Domain Models              [1 hr]
│
├── 10. ARCHITECTURE & APPLICATION STRUCTURE
│   │
│   ├── 10.1 Layered Architecture                      [1 hr] ⭐
│   ├── 10.2 Presentation Layer                        [30 min]
│   ├── 10.3 Application Layer                         [45 min]
│   ├── 10.4 Domain Layer                              [1 hr] ⭐
│   ├── 10.5 Infrastructure Layer                      [45 min]
│   ├── 10.6 Dependency Direction                      [1 hr] ⭐
│   │
│   ├── 10.7 MVC Architecture                          [1 hr] ⭐
│   │   ├── Model
│   │   ├── View
│   │   ├── Controller
│   │   └── Request Flow
│   │
│   ├── 10.8 MVP Architecture                          [30 min]
│   ├── 10.9 MVVM Architecture                         [45 min]
│   │
│   ├── 10.10 Modular Architecture                    [45 min] ⭐
│   ├── 10.11 Package-by-Layer                         [30 min]
│   ├── 10.12 Package-by-Feature                       [45 min] ⭐
│   ├── 10.13 Project / Package Structure              [45 min] ⭐
│   │
│   ├── 10.14 Clean Architecture                       [1.5 hr] ⭐
│   ├── 10.15 Hexagonal Architecture                   [1 hr] ⭐
│   ├── 10.16 Onion Architecture                       [1 hr]
│   ├── 10.17 Ports & Adapters                         [1 hr]
│   │
│   ├── 10.18 Modular Monolith                         [1 hr] ⭐
│   ├── 10.19 Microservices Architecture               [1 hr]
│   ├── 10.20 Event-Driven Architecture                [1 hr] ⭐
│   ├── 10.21 CQRS                                    [1 hr]
│   ├── 10.22 Event Sourcing                           [1 hr]
│   └── 10.23 Choosing the Right Architecture          [1 hr] ⭐
│
├── 11. DEPENDENCY INJECTION
│   ├── 11.1 What is Dependency Injection?             [45 min] ⭐
│   ├── 11.2 Constructor Injection                     [45 min] ⭐
│   ├── 11.3 Setter Injection                          [30 min]
│   ├── 11.4 Interface-Based DI                        [45 min]
│   ├── 11.5 IoC vs DI                                [45 min] ⭐
│   ├── 11.6 DI Containers                             [45 min]
│   └── 11.7 Spring Dependency Injection               [1 hr] ⭐
│
├── 12. JAVA FOR LLD
│   ├── 12.1 Classes & Objects                         [45 min]
│   ├── 12.2 Interfaces & Abstract Classes             [45 min]
│   ├── 12.3 Access Modifiers                          [30 min]
│   ├── 12.4 Collections                               [1 hr]
│   ├── 12.5 Generics                                  [1 hr]
│   ├── 12.6 Enums                                    [30 min]
│   ├── 12.7 Records                                  [30 min]
│   ├── 12.8 Functional Interfaces                     [45 min]
│   ├── 12.9 Lambdas                                  [45 min]
│   ├── 12.10 Streams                                 [1 hr]
│   ├── 12.11 Exception Design                         [45 min]
│   ├── 12.12 equals / hashCode / toString             [45 min] ⭐
│   └── 12.13 Java Features Used in LLD               [1 hr] ⭐
│
├── 13. CONCURRENCY & THREAD-SAFE DESIGN
│   ├── 13.1 Process vs Thread                         [30 min]
│   ├── 13.2 Race Conditions                           [45 min] ⭐
│   ├── 13.3 Critical Sections                         [30 min]
│   ├── 13.4 Synchronization                           [45 min]
│   ├── 13.5 Locks                                    [45 min] ⭐
│   ├── 13.6 synchronized                             [45 min]
│   ├── 13.7 volatile                                 [45 min]
│   ├── 13.8 Atomic Operations                         [45 min]
│   ├── 13.9 Concurrent Collections                   [1 hr]
│   ├── 13.10 Deadlocks                               [1 hr] ⭐
│   ├── 13.11 Thread Pools                             [1 hr] ⭐
│   ├── 13.12 ExecutorService                         [1 hr]
│   ├── 13.13 Producer-Consumer                       [1 hr] ⭐
│   ├── 13.14 Thread-Safe Classes                     [1 hr] ⭐
│   └── 13.15 Designing for Concurrency               [1 hr] ⭐
│
├── 14. PERSISTENCE & DATA ACCESS
│   ├── 14.1 Repository Pattern                        [1 hr] ⭐
│   ├── 14.2 DAO Pattern                               [45 min]
│   ├── 14.3 ORM Concepts                              [45 min]
│   ├── 14.4 Entity Mapping                            [45 min]
│   ├── 14.5 Transaction Boundaries                    [1 hr] ⭐
│   ├── 14.6 Unit of Work                              [45 min]
│   ├── 14.7 Identity Map                              [45 min]
│   ├── 14.8 Caching at Object Level                  [45 min]
│   └── 14.9 Persistence Trade-offs                   [45 min]
│
├── 15. API & SERVICE DESIGN
│   ├── 15.1 Service Responsibility                   [45 min]
│   ├── 15.2 Controller / Service / Repository        [1 hr] ⭐
│   ├── 15.3 DTOs                                     [45 min] ⭐
│   ├── 15.4 Request / Response Modeling              [45 min]
│   ├── 15.5 Validation                               [45 min]
│   ├── 15.6 Error Handling                            [1 hr] ⭐
│   ├── 15.7 Idempotency                              [1 hr] ⭐
│   ├── 15.8 Retry & Failure Handling                 [1 hr]
│   └── 15.9 API Evolution                             [45 min]
│
├── 16. ADVANCED LLD CONCEPTS
│   ├── 16.1 Immutability & Thread Safety              [1 hr]
│   ├── 16.2 State Machines                            [1.5 hr] ⭐
│   ├── 16.3 Rule Engines                              [1.5 hr] ⭐
│   ├── 16.4 Plugin Architecture                       [1 hr]
│   ├── 16.5 Event-Driven Object Design               [1 hr] ⭐
│   ├── 16.6 Extensible Pricing Systems              [1 hr] ⭐
│   ├── 16.7 Configurable Workflows                   [1 hr]
│   ├── 16.8 Scheduling Systems                       [1.5 hr] ⭐
│   ├── 16.9 Rate Limiter Design                       [1.5 hr] ⭐
│   ├── 16.10 Cache Design                             [1 hr] ⭐
│   └── 16.11 Notification Systems                    [1 hr] ⭐
│
├── 17. LLD MACHINE-CODING
│   ├── 17.1 Machine-Coding Fundamentals              [1 hr] ⭐
│   ├── 17.2 Requirement Clarification                 [45 min]
│   ├── 17.3 Class Identification                      [45 min]
│   ├── 17.4 API Design                               [45 min]
│   ├── 17.5 Extensibility                            [1 hr] ⭐
│   ├── 17.6 Error Handling                            [45 min]
│   ├── 17.7 Concurrency                              [1 hr]
│   ├── 17.8 Testing                                  [1 hr] ⭐
│   ├── 17.9 Refactoring During Interview             [45 min]
│   └── 17.10 Time Management                         [30 min]
│
├── 18. CLASSIC LLD INTERVIEW PROBLEMS
│   ├── 🟢 Beginner
│   │   ├── Parking Lot                                [2 hr] ⭐
│   │   ├── Library Management                         [2 hr]
│   │   ├── Tic-Tac-Toe                                [2 hr] ⭐
│   │   ├── Vending Machine                            [2 hr] ⭐
│   │   └── Splitwise                                  [2 hr] ⭐
│   │
│   ├── 🟡 Intermediate
│   │   ├── Elevator System                            [2.5 hr] ⭐
│   │   ├── ATM                                        [2 hr]
│   │   ├── Car Rental System                          [2.5 hr]
│   │   ├── Movie Ticket Booking                       [2.5 hr] ⭐
│   │   ├── Library + Reservation                      [2 hr]
│   │   ├── Hotel Booking                              [2.5 hr]
│   │   └── Food Delivery                              [3 hr] ⭐
│   │
│   └── 🔴 Advanced
│       ├── Ride Sharing / Uber                        [3 hr] ⭐
│       ├── Notification System                        [3 hr] ⭐
│       ├── Payment System                             [3 hr] ⭐
│       ├── Rate Limiter                               [3 hr] ⭐
│       ├── Logging Framework                          [3 hr] ⭐
│       ├── File System                                [3 hr] ⭐
│       ├── Cache                                      [3 hr] ⭐
│       ├── Job Scheduler                              [3 hr] ⭐
│       ├── Pub/Sub System                             [3 hr] ⭐
│       └── Rule Engine                                [3 hr] ⭐
│
├── 19. LLD + BACKEND INTEGRATION
│   ├── 19.1 LLD in Spring Boot                        [1 hr] ⭐
│   ├── 19.2 Controllers & Services                    [45 min]
│   ├── 19.3 Repository & JPA                          [1 hr]
│   ├── 19.4 Dependency Injection                     [45 min]
│   ├── 19.5 Transactions                              [1 hr]
│   ├── 19.6 Project / Package Structure              [1 hr] ⭐
│   ├── 19.7 Modular Spring Boot Design                [1 hr] ⭐
│   ├── 19.8 Redis Integration                         [1 hr]
│   ├── 19.9 Kafka / Event Integration                 [1 hr]
│   ├── 19.10 External Service Integration             [1 hr]
│   └── 19.11 Production-Ready Service Design         [1.5 hr] ⭐
│
├── 20. DESIGN REVIEW & REFACTORING
│   ├── 20.1 Identify Code Smells                      [1 hr] ⭐
│   ├── 20.2 God Object                                [45 min]
│   ├── 20.3 God Service                               [45 min]
│   ├── 20.4 Tight Coupling                            [45 min]
│   ├── 20.5 Shotgun Surgery                          [45 min]
│   ├── 20.6 Feature Envy                              [45 min]
│   ├── 20.7 Primitive Obsession                       [45 min]
│   ├── 20.8 Refactoring Patterns                     [1 hr] ⭐
│   └── 20.9 Design Review Checklist                  [1 hr] ⭐
│
└── 21. INTERVIEW MASTERY
    ├── 21.1 30-Minute LLD Interview Strategy          [1 hr] ⭐
    ├── 21.2 Requirement Clarification                 [45 min] ⭐
    ├── 21.3 Identify Core Entities                    [45 min]
    ├── 21.4 Define Responsibilities                   [45 min]
    ├── 21.5 Define Relationships                      [45 min]
    ├── 21.6 Select Patterns                           [45 min] ⭐
    ├── 21.7 Handle Follow-up Requirements             [1 hr] ⭐
    ├── 21.8 Discuss Trade-offs                        [1 hr] ⭐
    ├── 21.9 Explain Design Clearly                    [1 hr] ⭐
    ├── 21.10 Code Walkthrough                         [1 hr]
    ├── 21.11 LLD Mock Interviews                     [10 × 1 hr] ⭐
    └── 21.12 Final Interview Revision                [3 hr] ⭐
```