# 04. CODE QUALITY & OBJECT DESIGN

🏷️ Tags: `#LLD` `#CodeQuality` `#ObjectDesign` `#Java` `#Coupling` `#Cohesion` `#DependencyManagement` `#Immutability` `#SideEffects` `#Maintainability` `#Extensibility`

---

# 04.1 Types of Coupling

🏷️ Tags: `#Coupling` `#DesignQuality` `#LLD`

---

## ❓ Problem

Classes/modules rarely work in isolation. They depend on other classes, data, or behavior.

The problem is not **having dependencies**. The problem is having **unnecessary or overly strong dependencies**.

Example:

```
class OrderService {
    void process(Order order) {
        order.internalCounter = 10;
    }
}
```

`OrderService` now knows how `Order` stores its internal state.

A change inside `Order` can therefore break `OrderService`.

---

## 📋 Prerequisites

- Classes and objects
- Encapsulation
- Interfaces
- SOLID principles
- Dependency Inversion Principle
- Program to an Interface

---

## 🎯 Why This Exists

Coupling helps answer:

> **"How strongly does one module depend on another?"**

The goal is generally:

> **Reduce unnecessary coupling, not eliminate coupling.**

Some coupling is unavoidable because useful systems must communicate.

---

## 🧠 Core Concept

### 1. Content Coupling

One module directly accesses or modifies another module's internals.

```
class A {
    void process(B b) {
        b.internalCounter = 10;
    }
}
```

Mental model:

```
"I know your internals and modify them."
```

This is very tight coupling.

---

### 2. Common Coupling

Multiple modules depend on shared global/common data.

```
class GlobalConfig {
    static String currency = "INR";
}
```

```
class OrderService {
    void process() {
        System.out.println(GlobalConfig.currency);
    }
}
```

Multiple components are coupled through shared state.

---

### 3. Control Coupling

One component passes information that controls another component's behavior.

```
void processOrder(Order order, boolean sendNotification) {
    if (sendNotification) {
        // send notification
    }
}
```

The caller is partly controlling the internal execution path.

Mental model:

```
"I'll tell you which path to execute."
```

---

### 4. Stamp Coupling

A large object/structure is passed even though only part of it is required.

```
void calculateTax(Order order) {
    double amount = order.getAmount();
}
```

If the method only needs `amount`, passing the entire `Order` exposes more information than necessary.

---

### 5. Data Coupling

Only the required data is passed.

```
void calculateTax(double amount) {
    // calculate
}
```

This is generally preferable to stamp coupling when the additional object context isn't needed.

---

### 6. Message Coupling

Components communicate through messages/contracts without needing to know the implementation internals.

Example:

```
class OrderConfirmedEvent {
    private final long orderId;

    OrderConfirmedEvent(long orderId) {
        this.orderId = orderId;
    }
}
```

A publisher can publish the event without knowing what every consumer does internally.

---

## 🌍 Real-World Analogy

Think about a restaurant.

### Content coupling

A waiter enters the kitchen and changes the chef's ingredients directly.

### Control coupling

You tell the chef:

> "Cook this order, but skip step 3."

### Data coupling

You simply provide:

> "Table 10, 2 pizzas."

### Message coupling

You place an order through the restaurant's ordering system. The kitchen receives the order message without the customer knowing its internal workflow.

---

## ❌ Bad Design

```
class OrderService {

    void process(Order order) {
        order.status = "PAID";
        order.internalCounter = 10;
    }
}
```

`OrderService` knows the internal representation of `Order`.

---

## ✅ Better Design

Expose behavior instead of internal state:

```
class Order {

    private String status;

    void markAsPaid() {
        this.status = "PAID";
    }
}
```

```
class OrderService {

    void process(Order order) {
        order.markAsPaid();
    }
}
```

Now the internal representation can change without requiring `OrderService` to know about it.

---

## 💻 Code Example

### Stamp Coupling

```
class TaxCalculator {

    double calculateTax(Order order) {
        return order.getAmount() * 0.18;
    }
}
```

### Data Coupling

```
class TaxCalculator {

    double calculateTax(double amount) {
        return amount * 0.18;
    }
}
```

If tax calculation genuinely requires only the amount, the second design communicates that dependency more precisely.

---

## 🗺️ Diagram

```
flowchart LR
    A[Content Coupling] --> B[Common Coupling]
    B --> C[Control Coupling]
    C --> D[Stamp Coupling]
    D --> E[Data Coupling]
    E --> F[Message Coupling]

    A --> G[Tighter]
    F --> H[Looser]
```

> This hierarchy is a useful conceptual model, not an absolute rule for every architecture.

---

## 🏢 Real-World Application

Coupling appears everywhere:

```
Service → Repository
Service → Payment Gateway
Service → Database
Producer → Event
Consumer → Event
Controller → Service
```

The practical question is:

> **Does this dependency expose more knowledge than necessary?**

---

## ⚖️ Trade-offs

### Lower coupling

**Pros**

- Easier testing
- Easier replacement
- Easier maintenance
- Fewer ripple effects

**Cons**

- Additional abstractions may increase complexity
- Too much indirection can make simple code harder to follow

Do not introduce abstractions merely to reduce every dependency.

---

## 🎯 Interview Questions

### Q1. Is coupling always bad?

**Answer:** No.

Dependencies are necessary. The goal is to reduce **unnecessary or overly strong coupling**.

### Q2. What is stamp coupling?

**Answer:** Passing a larger object/structure when the receiver only needs part of it.

### Q3. Difference between stamp and data coupling?

```
Stamp → pass whole object
Data  → pass only required data
```

### Q4. What is control coupling?

**Answer:** Passing a flag or control parameter that determines which behavior the receiving component executes.

---

## 🧪 Practice Problem

Given:

```
class OrderService {

    void calculate(Order order) {
        System.out.println(order.getCustomer().getAddress().getCity());
    }
}
```

Identify the coupling/design issue and explain how you would reduce unnecessary knowledge.

---

## ⚠️ Mistakes / Gotchas

- Don't say "all coupling is bad."
- Don't confuse coupling with cohesion.
- Passing an object is not automatically stamp coupling; it depends on whether only part of the object is actually needed.
- Don't introduce an interface merely because an interface exists.
- Lower coupling must be balanced against unnecessary abstraction.

---

## 🔑 Key Takeaways

- Coupling measures dependency **between** modules.
- Content coupling exposes internals.
- Control coupling uses parameters to control behavior.
- Stamp coupling passes more data than necessary.
- Data coupling passes only required data.
- Message coupling communicates through contracts/messages.
- The goal is **low unnecessary coupling**, not zero coupling.

---

## 🧾 Key Takeaways

```
COUPLING
├── Content   → access internals
├── Common    → shared global data
├── Control   → control another module's behavior
├── Stamp     → pass large object, use small part
├── Data      → pass required data
└── Message   → communicate through messages/contracts

BETWEEN classes/modules
↓
Prefer lower unnecessary coupling
```

---

## 🔗 Related Concepts

- Dependency Management
- Dependency Inversion Principle
- Program to an Interface
- Encapsulation
- Law of Demeter
- Cohesion

---

## 🚧 Pending / Related Topics

- Detailed dependency management → **04.3**
- High Cohesion / Low Coupling → covered as a design principle earlier

---

# 04.2 Types of Cohesion

🏷️ Tags: `#Cohesion` `#CodeQuality` `#LLD`

---

## ❓ Problem

A class can contain many methods and still be poorly designed.

The key question is:

> **Do the responsibilities inside this class actually belong together?**

---

## 📋 Prerequisites

- Classes and responsibilities
- SRP
- Object-oriented design
- Coupling

---

## 🎯 Why This Exists

Cohesion measures the relationship **inside** a module/class.

```
Cohesion → inside
Coupling → between
```

Generally:

> **Higher cohesion is desirable.**

---

## 🧠 Core Concept

### 1. Coincidental Cohesion

Completely unrelated responsibilities are grouped together.

```
class Utility {

    void sendEmail() {}

    void compressImage() {}

    void calculateTax() {}

    void saveOrder() {}
}
```

There is no meaningful reason for these operations to belong together.

---

### 2. Logical Cohesion

Operations are logically related by category but represent different actual responsibilities.

Example:

```
void handle(String type) {
    if (type.equals("EMAIL")) {
        // email
    } else if (type.equals("SMS")) {
        // SMS
    } else if (type.equals("PUSH")) {
        // push
    }
}
```

They are all "notification-related," but different behaviors are being grouped behind one operation.

---

### 3. Temporal Cohesion

Responsibilities are grouped because they happen at the same time.

Example:

```
class ApplicationStartup {

    void initializeDatabase() {}
    void loadConfiguration() {}
    void initializeCache() {}
}
```

These operations happen during startup.

---

### 4. Procedural Cohesion

Operations are grouped because they follow a particular execution sequence.

```
validate()
   ↓
calculate()
   ↓
save()
   ↓
notify()
```

The grouping comes primarily from the procedure/order of execution.

---

### 5. Communicational Cohesion

Operations work on the same data.

For example, methods inside an `Order` dealing with the same order state/data.

---

### 6. Sequential Cohesion

The output of one operation becomes the input to another.

```
A
↓ output
B
↓ output
C
```

---

### 7. Functional Cohesion

Everything in the module contributes to one well-defined purpose.

```
class TaxCalculator {

    double calculateTax(Order order) {
        return order.getAmount() * 0.18;
    }
}
```

The class has a clear purpose:

```
Calculate tax
```

---

## 🌍 Real-World Analogy

Think of a toolbox.

### Coincidental cohesion

A box containing:

```
Hammer
Passport
Laptop charger
Cooking spoon
```

### Functional cohesion

A box containing tools specifically for electrical repair.

Everything inside serves the same purpose.

---

## ❌ Bad Design

```
class Utility {

    void sendEmail() {}
    void compressImage() {}
    void calculateTax() {}
    void saveOrder() {}
}
```

The class has unrelated responsibilities.

---

## ✅ Better Design

```
class EmailService {
    void sendEmail() {}
}

class ImageCompressor {
    void compressImage() {}
}

class TaxCalculator {
    void calculateTax() {}
}

class OrderRepository {
    void saveOrder() {}
}
```

Each class has a clearer responsibility.

---

## 💻 Code Example

```
class TaxCalculator {

    double calculateTax(Order order) {
        return order.getAmount() * 0.18;
    }
}
```

This is strongly cohesive because the class exists for one closely related purpose.

---

## 🗺️ Diagram

```
flowchart LR
    A[Coincidental] --> B[Logical]
    B --> C[Temporal]
    C --> D[Procedural]
    D --> E[Communicational]
    E --> F[Sequential]
    F --> G[Functional]

    A --> H[Lower Cohesion]
    G --> I[Higher Cohesion]
```

> This ordering is a useful textbook-style model; exact terminology/hierarchy can vary.

---

## 🏢 Real-World Application

Good service boundaries often aim for high cohesion:

```
OrderService
PaymentService
PricingService
InventoryService
NotificationService
```

The exact boundaries depend on the domain. Splitting everything into tiny classes is not automatically better.

---

## ⚖️ Trade-offs

High cohesion generally improves:

- readability
- maintainability
- testing
- change isolation

But excessive decomposition can produce:

```
Class A → Class B → Class C → Class D → Class E
```

with little actual value.

The goal is **meaningful responsibility boundaries**, not maximum number of classes.

---

## 🎯 Interview Questions

### Q1. What is cohesion?

**Answer:** How strongly the responsibilities inside a module/class belong together.

### Q2. Which is generally preferred?

**Answer:** High cohesion.

### Q3. Difference between cohesion and coupling?

```
Cohesion → relationship inside a module
Coupling → dependency between modules
```

### Q4. What is functional cohesion?

**Answer:** The elements of a module work together to perform one well-defined purpose.

---

## 🧪 Practice Problem

Analyze:

```
class UserService {

    void registerUser() {}
    void calculateTax() {}
    void compressImage() {}
    void sendEmail() {}
}
```

Identify the cohesion problem and suggest meaningful boundaries.

---

## ⚠️ Mistakes / Gotchas

- Don't confuse cohesion with coupling.
- High cohesion does not mean "one method per class."
- Don't split classes merely to make them smaller.
- SRP and cohesion are related but not identical.
- A class can have several methods and still be highly cohesive.

---

## 🔑 Key Takeaways

- Cohesion is about what belongs **inside** a module.
- High cohesion means responsibilities are strongly related.
- Coincidental cohesion is weak.
- Functional cohesion is strong.
- High cohesion usually improves maintainability.
- Don't over-fragment the design.

---

## 🧾 Key Takeaways

```
COHESION
├── Coincidental → unrelated
├── Logical → same category
├── Temporal → same time
├── Procedural → same sequence
├── Communicational → same data
├── Sequential → output → input
└── Functional → one clear purpose

INSIDE class/module
↓
Prefer high meaningful cohesion
```

---

## 🔗 Related Concepts

- SRP
- Low Coupling
- Maintainability
- Separation of Concerns
- Dependency Management

---

## 🚧 Pending / Related Topics

- High Cohesion / Low Coupling was covered earlier as a design principle.
- Maintainability → **04.6**

---

# 04.3 Dependency Management

🏷️ Tags: `#DependencyManagement` `#DI` `#DIP` `#Java` `#LLD`

---

## ❓ Problem

A class needs other objects to perform its work.

The design problem appears when the class:

1. directly creates replaceable dependencies
2. depends on concrete implementations unnecessarily
3. hides important dependencies

Example:

```
class OrderService {

    private Razorpay razorpay = new Razorpay();

}
```

---

## 📋 Prerequisites

- Interfaces
- Dependency Inversion Principle
- Program to an Interface
- Coupling
- Java constructors

---

## 🎯 Why This Exists

Dependency management answers:

> **What does this class depend on, and who should provide those dependencies?**

The important distinction:

```
DIP = design principle
DI  = implementation technique
```

---

## 🧠 Core Concept

Suppose:

```
OrderService → Razorpay
```

Instead:

```
OrderService → PaymentGateway
                     ↑
                  Razorpay
```

Define the abstraction:

```
interface PaymentGateway {
    void pay(double amount);
}
```

Implementation:

```
class Razorpay implements PaymentGateway {

    public void pay(double amount) {
        // payment
    }
}
```

Then:

```
class OrderService {

    private final PaymentGateway paymentGateway;

    OrderService(PaymentGateway paymentGateway) {
        this.paymentGateway = paymentGateway;
    }
}
```

---

## 🌍 Real-World Analogy

A phone charger socket doesn't need to know how the electricity grid generates electricity.

It depends on a contract/interface.

Likewise:

```
OrderService
    ↓
PaymentGateway
    ↓
Razorpay
```

The service needs the capability, not the implementation details.

---

## ❌ Bad Design

```
class OrderService {

    private Razorpay razorpay = new Razorpay();

    void placeOrder(Order order) {
        razorpay.pay(order.getAmount());
    }
}
```

Problems:

- Concrete dependency
- Construction responsibility
- Harder replacement
- Harder testing

---

## ✅ Better Design

```
class OrderService {

    private final PaymentGateway gateway;

    OrderService(PaymentGateway gateway) {
        this.gateway = gateway;
    }

    void placeOrder(Order order) {
        gateway.pay(order.getAmount());
    }
}
```

---

## 💻 Code Example

```
interface PaymentGateway {
    void pay(double amount);
}

class Razorpay implements PaymentGateway {

    @Override
    public void pay(double amount) {
        // Razorpay implementation
    }
}

class OrderService {

    private final PaymentGateway gateway;

    OrderService(PaymentGateway gateway) {
        this.gateway = gateway;
    }

    void placeOrder(Order order) {
        gateway.pay(order.getAmount());
    }
}
```

Testing can now provide a fake/mock:

```
OrderService service =
    new OrderService(new MockPaymentGateway());
```

---

## 🗺️ Diagram

```
classDiagram
    class OrderService
    class PaymentGateway {
        <<interface>>
        +pay(amount)
    }
    class Razorpay {
        +pay(amount)
    }

    OrderService --> PaymentGateway
    PaymentGateway <|.. Razorpay
```

---

## 🏢 Real-World Application

Typical backend dependencies:

```
Controller
    ↓
Service
    ↓
Repository
    ↓
Database

Service
    ↓
PaymentGateway

Service
    ↓
NotificationService
```

The abstraction boundary is useful when the implementation is replaceable or when isolation/testing matters.

---

## ⚖️ Trade-offs

### Benefits

- Lower coupling
- Easier testing
- Easier replacement
- Explicit dependencies

### Costs

- More interfaces/classes
- More indirection
- Can become over-engineered

Don't create:

```
InterfaceA
  ↓
ImplementationA
```

for every trivial class simply because "DI is good."

Use abstraction where there is a meaningful boundary or replaceable dependency.

---

## 🎯 Interview Questions

### Q1. What is dependency injection?

**Answer:** Supplying an object's dependency from outside instead of having the object create it internally.

### Q2. Which injection style was emphasized?

**Answer:** Constructor injection for required dependencies.

### Q3. DIP vs DI?

```
DIP → principle
DI  → technique
```

### Q4. Why constructor injection?

Because required dependencies become explicit and the object can be created only when those dependencies are available.

---

## 🧪 Practice Problem

Refactor:

```
class OrderService {

    private MySQLDatabase database = new MySQLDatabase();
    private Razorpay razorpay = new Razorpay();
}
```

Use appropriate abstractions and constructor injection.

---

## ⚠️ Mistakes / Gotchas

- DI is not the same thing as DIP.
- `new` is not automatically bad.
- Don't introduce abstractions without a reason.
- Constructor injection is particularly useful for required dependencies.
- The abstraction should represent a meaningful capability.

---

## 🔑 Key Takeaways

- Dependencies are normal.
- Concrete dependencies can create unnecessary coupling.
- Prefer abstractions for meaningful replaceable boundaries.
- DI supplies dependencies externally.
- Constructor injection is useful for required dependencies.
- DIP is a principle; DI is a technique.
- Don't over-engineer simple dependencies.

---

## 🧾 Key Takeaways

```
DIP
↓
Depend on abstractions

DI
↓
Supply dependency externally

Constructor DI
↓
Required dependency enters constructor

OrderService
    ↓
PaymentGateway
    ↑
Razorpay
```

---

## 🔗 Related Concepts

- DIP
- Program to an Interface
- Low Coupling
- OCP
- Dependency Injection frameworks

---

## 🚧 Pending / Related Topics

- Framework-specific DI was not covered.
- Spring dependency injection is a separate backend topic.

---

# 04.4 Immutability

🏷️ Tags: `#Immutability` `#Java` `#ObjectDesign` `#LLD`

---

## ❓ Problem

Mutable objects can change unexpectedly when multiple parts of a system hold references to the same object.

This creates hidden state changes and makes reasoning/testing harder.

---

## 📋 Prerequisites

- Java classes
- References
- Encapsulation
- `final`
- Collections

---

## 🎯 Why This Exists

An immutable object provides a strong guarantee:

> **Its state cannot be changed after construction.**

This is different from simply declaring a variable `final`.

---

## 🧠 Core Concept

```
final class Money {

    private final double amount;

    Money(double amount) {
        this.amount = amount;
    }

    public double getAmount() {
        return amount;
    }
}
```

Once:

```
Money money = new Money(500);
```

the amount cannot become `1000`.

---

## 🌍 Real-World Analogy

A printed invoice is a good mental model.

Once issued, you don't alter the same piece of paper. If something changes, you issue a new invoice.

Similarly:

```
Old Money(500)
       ↓
New Money(1000)
```

rather than modifying the existing object.

---

## ❌ Bad Design

```
class User {

    private String name;

    void setName(String name) {
        this.name = name;
    }
}
```

State can be changed after construction.

---

## ✅ Better Design

```
final class User {

    private final String name;

    User(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

No setter.

---

## 💻 Code Example

### Important: `final` does not automatically mean immutable

```
final List<String> items = new ArrayList<>();

items.add("Pizza");   // valid
items.add("Burger");  // valid

items = new ArrayList<>(); // invalid
```

`final` means:

```
reference cannot be reassigned
```

It does **not** mean:

```
object cannot mutate
```

For collections, use defensive copying when necessary:

```
class Order {

    private final List<String> items;

    Order(List<String> items) {
        this.items = new ArrayList<>(items);
    }

    public List<String> getItems() {
        return List.copyOf(items);
    }
}
```

---

## 🗺️ Diagram

```
flowchart TD
    A[Create Object] --> B[Initialize State]
    B --> C[State Cannot Change]
    C --> D[Need Different State?]
    D --> E[Create New Object]
```

---

## 🏢 Real-World Application

Immutable values are useful for concepts such as:

```
Money
Coordinates
Configuration snapshots
Value Objects
IDs
Dates/timestamps
```

The exact choice depends on whether the domain object genuinely needs mutation.

---

## ⚖️ Trade-offs

### Benefits

- Easier reasoning
- Safer sharing
- Fewer accidental mutations
- Easier testing
- Useful for concurrency

### Costs

- New objects may need to be created for changes.
- Defensive copies can have cost.
- Deep immutability can be more involved for nested mutable objects.

Do not assume every domain object should be immutable.

---

## 🎯 Interview Questions

### Q1. Is `final List<String>` immutable?

**Answer:** No.

`final` prevents reassignment of the reference, not mutation of the list.

### Q2. How do you make a class immutable?

Typical approach:

```
private state
+
initialize through constructor
+
no setters
+
prevent mutable state from escaping
+
defensive copies where needed
```

### Q3. Why use defensive copies?

To prevent external code from modifying internal mutable state.

---

## 🧪 Practice Problem

Identify why this class isn't safely immutable:

```
class User {

    private final List<String> roles;

    User(List<String> roles) {
        this.roles = roles;
    }

    List<String> getRoles() {
        return roles;
    }
}
```

Fix the design.

---

## ⚠️ Mistakes / Gotchas

- `final` ≠ immutable.
- No setter alone does not guarantee deep immutability.
- Mutable collections can leak internal state.
- Mutation itself is not automatically bad.
- Don't force immutability where controlled mutation is part of the domain model.

---

## 🔑 Key Takeaways

- Immutable objects cannot change state after creation.
- `final` prevents reference reassignment.
- `final` alone does not make an object immutable.
- Avoid exposing mutable internal state.
- Defensive copies help protect encapsulation.
- Immutability improves reasoning and safe sharing.

---

## 🧾 Key Takeaways

```
final reference
    ≠
immutable object

IMMUTABILITY
├── private state
├── initialize once
├── no setters
├── protect mutable fields
└── defensive copy when needed
```

---

## 🔗 Related Concepts

- Encapsulation
- Defensive Copy
- Value Objects
- Concurrency
- Side Effects

---

## 🚧 Pending / Related Topics

- Advanced Java immutability/concurrency was not covered.

---

# 04.5 Side Effects

🏷️ Tags: `#SideEffects` `#PureFunction` `#FunctionalProgramming` `#LLD`

---

## ❓ Problem

A method may look like it is only calculating something but can secretly modify state, write to a database, call an API, or send a notification.

Hidden side effects make code harder to reason about and test.

---

## 📋 Prerequisites

- Methods/functions
- Object state
- Database operations
- APIs

---

## 🎯 Why This Exists

A **side effect** occurs when an operation changes something outside its local computation.

Examples:

```
DB write
API call
Object mutation
Event publishing
Email
File write
Logging
```

The goal is not to eliminate all side effects.

Backend systems inherently need them.

The goal is:

> **Make side effects explicit and controlled.**

---

## 🧠 Core Concept

Pure calculation:

```
double calculateTax(double amount) {
    return amount * 0.18;
}
```

Impure behavior:

```
double calculateTax(Order order) {
    order.setTax(order.getAmount() * 0.18);
    database.save(order);

    return order.getTax();
}
```

The second method both calculates and changes external state.

---

## 🌍 Real-World Analogy

A calculator:

```
Input → Calculation → Output
```

has no need to change the world.

A bank transaction:

```
Input
 ↓
Calculation
 ↓
Account balance changes
 ↓
Transaction recorded
```

necessarily has side effects.

The design goal is to keep those effects visible and controlled.

---

## ❌ Bad Design

```
void calculatePrice(Order order) {

    order.setTotal(...);

    database.save(order);

    emailService.send(...);
}
```

One method mixes:

```
Calculation
+
Mutation
+
Persistence
+
Notification
```

---

## ✅ Better Design

Separate the concerns:

```
calculatePrice()
       ↓
pure calculation

saveOrder()
       ↓
database side effect

sendNotification()
       ↓
external side effect
```

The exact decomposition depends on the domain; separation should improve clarity rather than create unnecessary layers.

---

## 💻 Code Example

```
class PricingService {

    double calculateTax(double amount) {
        return amount * 0.18;
    }
}
```

Then application-level code handles the effect:

```
class OrderService {

    void placeOrder(Order order) {

        double tax =
            pricingService.calculateTax(order.getAmount());

        order.applyTax(tax);

        orderRepository.save(order);

        notificationService.sendConfirmation(order);
    }
}
```

---

## 🗺️ Diagram

```
flowchart LR
    A[Input] --> B[Pure Calculation]
    B --> C[Result]

    C --> D[State Mutation]
    D --> E[Database Write]
    E --> F[Notification]
```

---

## 🏢 Real-World Application

Backend operations naturally contain side effects:

```
Payment API
Database transaction
Kafka/event publishing
Cache update
Email
SMS
Push notification
File storage
```

The useful design boundary is between:

```
Business calculation
```

and:

```
External effects
```

where practical.

---

## ⚖️ Trade-offs

### Pure logic

**Pros**

- Easy testing
- Predictable
- Reusable
- Easy reasoning

### Side effects

**Pros**

- Required for real systems
- Allows persistence and integration

**Cost**

- Harder testing
- More state
- External failures
- Ordering/retry concerns

Don't attempt to eliminate all side effects from an application.

---

## 🎯 Interview Questions

### Q1. What is a side effect?

An externally observable change caused by an operation.

### Q2. Is database save a side effect?

Yes.

### Q3. Is modifying an object a side effect?

Yes, when the mutation changes state outside the function's local computation.

### Q4. Should backend systems have zero side effects?

No. Real systems need them. The goal is controlled, explicit side effects.

---

## 🧪 Practice Problem

Refactor:

```
double calculateTotal(Order order) {

    order.setTotal(
        order.getAmount() + order.getTax()
    );

    database.save(order);

    return order.getTotal();
}
```

Identify the side effects and separate the calculation from external operations.

---

## ⚠️ Mistakes / Gotchas

- "Side effect" does not mean "bad."
- Database/API operations are intentionally side-effecting.
- Logging is technically a side effect.
- Don't confuse pure functions with methods that merely return a value.
- A method can have both calculation and side effects.

---

## 🔑 Key Takeaways

- Side effects change external state or interact with external systems.
- DB writes and API calls are side effects.
- Object mutation can be a side effect.
- Pure functions are easier to reason about.
- Don't eliminate side effects; control and isolate them where useful.
- Make important effects explicit.

---

## 🧾 Key Takeaways

```
PURE
Input → Output
No observable external mutation

SIDE EFFECT
Method
 ↓
changes external state

Examples:
DB
API
Object mutation
Event
Email
File
Logging
```

---

## 🔗 Related Concepts

- Immutability
- Functional Programming
- Transactions
- Event-driven architecture
- Testing

---

## 🚧 Pending / Related Topics

- Distributed-system side effects, retries, idempotency and transactions are separate topics.

---

# 04.6 Maintainability

🏷️ Tags: `#Maintainability` `#CodeQuality` `#LLD`

---

## ❓ Problem

Code that works today may become painful to modify tomorrow.

The practical question is:

> **How painful will the next change be?**

---

## 📋 Prerequisites

- Coupling
- Cohesion
- Dependency Management
- SOLID
- Encapsulation

---

## 🎯 Why This Exists

Maintainability is about how easily developers can:

- understand code
- modify code
- debug code
- test code
- safely extend code

---

## 🧠 Core Concept

Consider:

```
class OrderService {

    void process(Order order) {
        // 200 lines
        // payment
        // tax
        // inventory
        // notification
        // database
        // discount
    }
}
```

A change to one concern can affect a large class.

A more maintainable design gives responsibilities meaningful boundaries.

```
OrderService
├── PaymentService
├── PricingService
├── InventoryService
├── NotificationService
└── OrderRepository
```

---

## 🌍 Real-World Analogy

A toolbox where every tool has its own labeled compartment is easier to maintain than one giant box containing everything.

The same idea applies to software:

```
Clear responsibility
+
Clear dependency
+
Clear boundary
=
Easier change
```

---

## ❌ Bad Design

```
class GodOrderService {

    void processPayment() {}
    void calculateTax() {}
    void updateInventory() {}
    void saveToDatabase() {}
    void sendEmail() {}
    void generateInvoice() {}
}
```

Everything is centralized.

---

## ✅ Better Design

```
OrderService
PaymentService
PricingService
InventoryService
OrderRepository
NotificationService
```

Each boundary should exist because it represents meaningful behavior, not merely because "small classes are good."

---

## 💻 Code Example

Dependency injection improves testability:

```
class OrderService {

    private final PaymentGateway gateway;

    OrderService(PaymentGateway gateway) {
        this.gateway = gateway;
    }

    void placeOrder(Order order) {
        gateway.pay(order.getAmount());
    }
}
```

Testing can provide a fake implementation without contacting a real payment provider.

---

## 🗺️ Diagram

```
flowchart TD
    A[Maintainable Design]
    A --> B[High Cohesion]
    A --> C[Low Unnecessary Coupling]
    A --> D[Clear Naming]
    A --> E[Testability]
    A --> F[Clear Boundaries]
    A --> G[Controlled Dependencies]
```

---

## 🏢 Real-World Application

Maintainability matters when:

```
Payment provider changes
Database changes
New notification channel is added
Business rule changes
Bug needs fixing
Tests need isolation
```

A well-structured design reduces the blast radius of such changes.

---

## ⚖️ Trade-offs

Maintainability does **not** mean:

```
More classes = better
More interfaces = better
More patterns = better
```

Too much abstraction can make code harder to understand.

The goal is:

> **Meaningful boundaries with the simplest design that supports expected change.**

---

## 🎯 Interview Questions

### Q1. What makes code maintainable?

A combination of high cohesion, low unnecessary coupling, clear boundaries, readable naming, testability and controlled dependencies.

### Q2. Is a small class automatically maintainable?

No.

### Q3. How does dependency injection improve maintainability?

It makes dependencies explicit and replaceable and improves test isolation.

---

## 🧪 Practice Problem

Given:

```
class OrderService {

    void placeOrder(Order order) {
        // payment
        // database
        // email
        // inventory
        // tax
    }
}
```

Identify the maintainability risks and propose meaningful boundaries.

---

## ⚠️ Mistakes / Gotchas

- Don't equate maintainability with class count.
- Don't over-abstract.
- Don't create interfaces without a meaningful reason.
- Maintainability is about future change, not merely current readability.
- High cohesion and low unnecessary coupling support maintainability.

---

## 🔑 Key Takeaways

- Maintainability asks how easy future changes will be.
- High cohesion helps.
- Low unnecessary coupling helps.
- Explicit dependencies improve testability.
- Clear boundaries reduce change impact.
- Simplicity matters.
- Over-engineering can reduce maintainability.

---

## 🧾 Key Takeaways

```
MAINTAINABILITY
↓
Easy to:
├── Understand
├── Modify
├── Debug
├── Test
└── Safely change

Supported by:
High Cohesion
Low Coupling
Clear Boundaries
Good Naming
Testability
Simple Design
```

---

## 🔗 Related Concepts

- Cohesion
- Coupling
- Dependency Management
- SOLID
- YAGNI
- KISS
- Extensibility

---

## 🚧 Pending / Related Topics

- Refactoring techniques were not covered in this section.

---

# 04.7 Extensibility

🏷️ Tags: `#Extensibility` `#OCP` `#DIP` `#LLD`

---

## ❓ Problem

Systems change.

A common example is adding another payment provider.

Today:

```
Razorpay
Stripe
```

Tomorrow:

```
PayPal
Cash
UPI
```

If every new implementation requires modifying core business logic, the design becomes harder to maintain.

---

## 📋 Prerequisites

- OCP
- DIP
- Interfaces
- Dependency Injection
- Polymorphism

---

## 🎯 Why This Exists

Extensibility asks:

> **How easily can I add new behavior without destabilizing existing behavior?**

This connects strongly with OCP:

> Extend behavior where appropriate instead of repeatedly modifying stable business logic.

---

## 🧠 Core Concept

Bad design:

```
class OrderService {

    void pay(String type, double amount) {

        if (type.equals("RAZORPAY")) {
            // Razorpay
        }
        else if (type.equals("STRIPE")) {
            // Stripe
        }
        else if (type.equals("PAYPAL")) {
            // PayPal
        }
    }
}
```

Every new provider adds another branch.

Better:

```
interface PaymentGateway {
    void pay(double amount);
}
```

Implementations:

```
class Razorpay implements PaymentGateway {
    public void pay(double amount) {}
}

class Stripe implements PaymentGateway {
    public void pay(double amount) {}
}
```

Now:

```
class OrderService {

    private final PaymentGateway gateway;

    OrderService(PaymentGateway gateway) {
        this.gateway = gateway;
    }

    void placeOrder(Order order) {
        gateway.pay(order.getAmount());
    }
}
```

Adding:

```
class PayPal implements PaymentGateway {
    public void pay(double amount) {}
}
```

doesn't require changing the core `OrderService` payment flow.

---

## 🌍 Real-World Analogy

A power socket provides a standard interface.

Different devices can use it:

```
Socket
├── Laptop charger
├── Phone charger
└── Monitor
```

The socket doesn't need to be redesigned for every new device.

The same idea can apply to software abstractions when there is genuine variation.

---

## ❌ Bad Design

```
OrderService
    │
    ├── if Razorpay
    ├── if Stripe
    ├── if PayPal
    └── if Cash
```

New behavior repeatedly modifies the existing service.

---

## ✅ Better Design

```
             PaymentGateway
                  ▲
          ┌───────┼────────┐
          │       │        │
      Razorpay  Stripe   PayPal
```

`OrderService` depends on the abstraction.

---

## 💻 Code Example

```
interface PaymentGateway {
    void pay(double amount);
}

class Razorpay implements PaymentGateway {

    @Override
    public void pay(double amount) {
        // Razorpay
    }
}

class Stripe implements PaymentGateway {

    @Override
    public void pay(double amount) {
        // Stripe
    }
}

class OrderService {

    private final PaymentGateway gateway;

    OrderService(PaymentGateway gateway) {
        this.gateway = gateway;
    }

    void placeOrder(Order order) {
        gateway.pay(order.getAmount());
    }
}
```

---

## 🗺️ Diagram

```
classDiagram
    class OrderService
    class PaymentGateway {
        <<interface>>
        +pay(amount)
    }
    class Razorpay {
        +pay(amount)
    }
    class Stripe {
        +pay(amount)
    }
    class PayPal {
        +pay(amount)
    }

    OrderService --> PaymentGateway
    PaymentGateway <|.. Razorpay
    PaymentGateway <|.. Stripe
    PaymentGateway <|.. PayPal
```

---

## 🏢 Real-World Application

Extensibility is useful where genuine variation exists:

```
Payment providers
Notification channels
Storage providers
Authentication providers
Shipping providers
Pricing strategies
```

A similar abstraction is useful in systems where implementations are expected to vary, but the exact architecture depends on the requirements.

---

## ⚖️ Trade-offs

### Extensible design

**Pros**

- Easier addition of new behavior
- Existing stable code changes less
- Better isolation of variations

### Cost

- More abstractions
- More indirection
- More classes
- Potentially harder initial understanding

### Critical rule

Do **not** create an elaborate abstraction because:

> "Maybe someday we will need another implementation."

That can violate **YAGNI**.

Use abstraction when the variation is:

- already real
- reasonably expected
- architecturally meaningful

---

## 🎯 Interview Questions

### Q1. How does polymorphism improve extensibility?

Different implementations can satisfy the same abstraction while the consumer remains unchanged.

### Q2. How does DIP help extensibility?

The high-level class depends on an abstraction rather than a concrete implementation.

### Q3. Does OCP mean "never modify existing code"?

No.

It means design stable areas so genuine extensions can be introduced without repeatedly modifying the same core logic.

### Q4. Should every class have an interface for extensibility?

No.

That would often be unnecessary abstraction.

---

## 🧪 Practice Problem

Current design:

```
class NotificationService {

    void send(String type, String message) {

        if (type.equals("EMAIL")) {
            // email
        }

        if (type.equals("SMS")) {
            // SMS
        }

        if (type.equals("PUSH")) {
            // push
        }
    }
}
```

Design an abstraction that allows a new notification channel to be added without modifying the core sending logic.

---

## ⚠️ Mistakes / Gotchas

- Extensibility ≠ unlimited abstraction.
- OCP does not mean "never change code."
- Don't create patterns for hypothetical requirements.
- A simple `if` can be perfectly acceptable when the variation is small and unlikely to grow.
- Extensibility and maintainability are related but different.

```
Maintainability
→ Easy to change existing behavior

Extensibility
→ Easy to add new behavior
```

---

## 🔑 Key Takeaways

- Extensibility is about adding new behavior safely.
- Interfaces and polymorphism can isolate variations.
- DIP supports extensibility.
- OCP is closely related.
- Don't over-engineer hypothetical extensions.
- Simpler design is better when variation is unlikely.
- Ask: **"What happens when the next implementation arrives?"**

---

## 🧾 Key Takeaways

```
EXTENSIBILITY
        ↓
Identify genuine variation
        ↓
Abstraction where justified
        ↓
Encapsulate changing behavior
        ↓
Add implementation
        ↓
Minimize changes to stable code
```

Example:

```
OrderService
     ↓
PaymentGateway
     ↑
 ┌───┼────┐
Razorpay Stripe PayPal
```

---

## 🔗 Related Concepts

- Open/Closed Principle
- Dependency Inversion Principle
- Program to an Interface
- Polymorphism
- Strategy Pattern
- YAGNI
- Maintainability

---

## 🚧 Pending / Related Topics

- Strategy Pattern
- Factory Pattern
- Advanced extensibility patterns
- Refactoring techniques

---

# Section 04 — Final Revision Map

```
04. CODE QUALITY & OBJECT DESIGN
│
├── 04.1 Types of Coupling
│   └── How strongly modules depend on each other
│
├── 04.2 Types of Cohesion
│   └── How strongly responsibilities inside a module belong together
│
├── 04.3 Dependency Management
│   └── What a class depends on + who provides it
│
├── 04.4 Immutability
│   └── Control object state after construction
│
├── 04.5 Side Effects
│   └── Control external state changes
│
├── 04.6 Maintainability
│   └── How easy existing behavior is to understand/change/test
│
└── 04.7 Extensibility
    └── How easy new behavior is to add
```

## 🧾 Section 04 Master Cheatsheet

```
┌────────────────────────────────────────────────────────────┐
│                 CODE QUALITY & OBJECT DESIGN               │
├────────────────────┬───────────────────────────────────────┤
│ Coupling           │ BETWEEN modules                      │
│                    │ Lower unnecessary coupling           │
├────────────────────┼───────────────────────────────────────┤
│ Cohesion           │ INSIDE a module                      │
│                    │ Higher meaningful cohesion            │
├────────────────────┼───────────────────────────────────────┤
│ Dependency Mgmt    │ What does this class depend on?      │
│                    │ Prefer meaningful abstractions + DI  │
├────────────────────┼───────────────────────────────────────┤
│ Immutability       │ Can state change after construction? │
│                    │ final ≠ immutable                    │
├────────────────────┼───────────────────────────────────────┤
│ Side Effects       │ Does operation change external state?│
│                    │ DB/API/mutation/event/etc.           │
├────────────────────┼───────────────────────────────────────┤
│ Maintainability    │ How painful is the next change?      │
│                    │ Cohesion + coupling + clarity        │
├────────────────────┼───────────────────────────────────────┤
│ Extensibility      │ How easy is the next implementation? │
│                    │ Abstraction where variation is real  │
└────────────────────┴───────────────────────────────────────┘
```

### The most important mental model

```
                 GOOD OBJECT DESIGN
                        │
        ┌───────────────┼────────────────┐
        ↓               ↓                ↓
   HIGH COHESION   LOW COUPLING    CLEAR DEPENDENCIES
        │               │                │
        └───────────────┼────────────────┘
                        ↓
                 MAINTAINABILITY
                        │
                        ↓
                  EXTENSIBILITY
```

### ⚠️ Final interview rule from this section

Don't blindly identify every principle in every piece of code.

Instead:

```
Read the code
    ↓
Find the actual dependency
    ↓
Find the actual responsibility
    ↓
Find the actual mutation/side effect
    ↓
Ask what happens when requirements change
    ↓
Apply only the principles supported by the evidence
```

This was the key correction from the practical exercise: **`order.setStatus("PAID")` alone does not prove that the design violates immutability**. The code must provide enough evidence before assigning a design problem.