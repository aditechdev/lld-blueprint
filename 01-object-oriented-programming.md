
# 01 · OBJECT-ORIENTED PROGRAMMING

🏷️ Tags: <!-- shield.io badges -->

![Java](https://img.shields.io/badge/Java-17%2B-orange)
![OOP](https://img.shields.io/badge/OOP-Core-blue)
![LLD](https://img.shields.io/badge/LLD-Interview%20Ready-purple)
![Design](https://img.shields.io/badge/Design-Object%20Oriented-green)

---

# 01.1 · Class & Object

## ❓ Problem

When designing an LLD system, we need a way to represent real-world entities in code.

Consider a parking system:

```text
Parking Lot
├── Parking Spot
├── Vehicle
├── Ticket
└── Payment
```

We need multiple parking spots, vehicles, tickets, etc.

If we represent everything using independent variables and functions, the system quickly becomes difficult to organize.

We need a structure that groups:

- Data
- Behavior

around a meaningful entity.

---

## **📋 Prerequisites**

- Basic programming fundamentals
- Variables and methods
- Basic Java syntax

---

## **🎯 Why This Exists**

OOP gives us a way to model a system around **objects that have state and behavior**.

Instead of thinking only:

```
data + functions
```

we can think:

```
Object
├── State
└── Behavior
```

This becomes the foundation for almost every LLD concept that follows.

---

## **🧠 Core Concept**

### **Class**

A **class** is a blueprint/template that defines what an object contains and what it can do.

```
class ParkingSpot {

    String id;
    boolean available;

    void occupy() {
        available = false;
    }

    void release() {
        available = true;
    }
}
```

The class itself is not the actual parking spot.

It defines the structure and behavior that a parking spot object will have.

### **Object**

An **object** is an actual runtime instance created from a class.

```
ParkingSpot spot1 = new ParkingSpot();
ParkingSpot spot2 = new ParkingSpot();
```

Now we have two different objects.

```
ParkingSpot class
       │
       ├── spot1
       │
       └── spot2
```

They have independent state.

### **Reference vs Object**

In:

```
ParkingSpot spot = new ParkingSpot();
```

There are two concepts:

```
spot
 │
 │ reference
 ▼
ParkingSpot object
```

- `spot` → reference variable
- `new ParkingSpot()` → creates the actual object

---

## **🌍 Real-World Analogy**

A house blueprint is not a house.

```
Blueprint
    │
    ├── House #1
    ├── House #2
    └── House #3
```

Similarly:

```
Class
  │
  ├── Object #1
  ├── Object #2
  └── Object #3
```

The blueprint defines the structure.

Each actual house is an independent instance.

---

## **❌ Bad Design**

Representing every parking spot independently:

```
String spot1Id;
boolean spot1Available;

String spot2Id;
boolean spot2Available;

String spot3Id;
boolean spot3Available;
```

Problems:

- Difficult to maintain
- Difficult to scale
- Behavior is disconnected from data
- No meaningful domain model

---

## **✅ Better Design**

Model a parking spot as an object:

```
class ParkingSpot {

    private String id;
    private boolean available;

    void occupy() {
        available = false;
    }

    void release() {
        available = true;
    }
}
```

Now the system can create any number of spots:

```
ParkingSpot spot1 = new ParkingSpot();
ParkingSpot spot2 = new ParkingSpot();
ParkingSpot spot3 = new ParkingSpot();
```

---

## **💻 Code Example**

```
class ParkingSpot {

    private final String id;
    private boolean available;

    ParkingSpot(String id) {
        this.id = id;
        this.available = true;
    }

    void occupy() {
        available = false;
    }

    void release() {
        available = true;
    }

    boolean isAvailable() {
        return available;
    }
}
```

Usage:

```
ParkingSpot spot = new ParkingSpot("A-101");

System.out.println(spot.isAvailable()); // true

spot.occupy();

System.out.println(spot.isAvailable()); // false
```

---

## **🗺️ Diagram**

```
classDiagram
    class ParkingSpot {
        -String id
        -boolean available
        +occupy()
        +release()
        +isAvailable()
    }

    ParkingSpot --> ParkingSpot : creates instances
```

Conceptually:

```
          ParkingSpot
         (Class/Blueprint)
               │
        ┌──────┴──────┐
        ▼             ▼
     spot1          spot2
    A-101           A-102
```

---

## **🏢 Real-World Application**

Typical backend domain objects:

```
E-commerce
├── Product
├── Cart
├── Order
└── Customer

Food Delivery
├── Restaurant
├── MenuItem
├── Order
└── DeliveryPartner

Payment
├── Payment
├── PaymentMethod
└── Transaction
```

---

## **⚖️ Trade-offs**

### **Benefits**

- Models domain entities naturally
- Groups related state and behavior
- Supports multiple independent instances
- Provides foundation for encapsulation

### **Trade-off**

Not every piece of data needs to become a class.

A class should represent a meaningful concept or responsibility.

---

## **🎯 Interview Questions**

1. What is a class?
2. What is an object?
3. What is the difference between a class and an object?
4. What happens when `new` is used in Java?
5. What is the difference between a reference and an object?
6. Can multiple objects be created from one class?
7. Do two objects of the same class share instance state?

---

## **🧪 Practice Problem**

Design a `BankAccount` class.

It should have:

- account number
- balance
- deposit
- withdraw
- balance check

Do not worry about encapsulation yet. That will be introduced next.

---

## **⚠️ Mistakes / Gotchas**

### **1. Class is not an object**

```
Class → blueprint
Object → actual instance
```

### **2. Reference is not the object**

```
ParkingSpot spot = new ParkingSpot();
```

`spot` is a reference.

`new ParkingSpot()` creates the object.

### **3. Not every noun needs to become a class**

Candidate domain objects must have meaningful state, behavior, identity, or responsibility.

---

## **🔑 Key Takeaways**

```
Class = blueprint
Object = runtime instance
Reference = variable pointing to an object
```

OOP starts by modeling meaningful domain objects.

---

## **🔗 Related Concepts**

- State & Behavior
- Encapsulation
- Abstraction
- Composition
- Domain Modeling

---

## **🚧 Pending / Related Topics**

- 01.2 State & Behavior
- 01.3 Encapsulation

---

# **01.2 · State & Behavior**

## **❓ Problem**

We now know that objects represent entities.

But what exactly makes an object useful?

Consider:

```
ParkingSpot spot = new ParkingSpot("A-101");
```

The spot needs to know:

```
Is it available?
```

And it should be able to:

```
Occupy itself
Release itself
```

This leads to two fundamental OOP concepts:

```
Object
├── State
└── Behavior
```

---

## **📋 Prerequisites**

- 01.1 Class & Object

---

## **🎯 Why This Exists**

Objects are useful because they don’t just hold data.

They represent:

- what the entity currently is
- what the entity can do

This distinction becomes extremely important when deciding **where business logic belongs**.

---

## **🧠 Core Concept**

### **State**

State represents the current condition/data of an object.

For a parking spot:

```
id = A-101
available = true
```

For an order:

```
status = CONFIRMED
totalAmount = 500
```

For a bank account:

```
balance = 10000
```

### **Behavior**

Behavior represents what an object can do.

```
ParkingSpot
├── occupy()
├── release()
└── isAvailable()

Order
├── confirm()
├── cancel()
└── calculateTotal()
```

---

## **🌍 Real-World Analogy**

A bank account has:

```
State
├── Balance
├── Account number
└── Status

Behavior
├── Deposit
├── Withdraw
└── Transfer
```

You don’t normally tell a bank account:

```
balance = balance - 500
```

You ask the account to perform:

```
withdraw(500)
```

The object can then enforce its own rules.

---

## **❌ Bad Design**

```
class Booking {
    String status;
}
```

And elsewhere:

```
booking.status = "CANCELLED";
```

Now any part of the application can modify the state.

This becomes dangerous when cancellation has rules:

```
Can it be cancelled?
Has payment been refunded?
Is cancellation allowed after check-in?
Should a notification be sent?
```

---

## **✅ Better Design**

Let the object own behavior related to its state:

```
class Booking {

    private BookingStatus status;

    void cancel() {

        if (status == BookingStatus.COMPLETED) {
            throw new IllegalStateException(
                "Completed booking cannot be cancelled"
            );
        }

        status = BookingStatus.CANCELLED;
    }
}
```

Now:

```
booking.cancel();
```

is more meaningful than:

```
booking.status = CANCELLED;
```

The object controls its own state transition.

---

## **💻 Code Example**

```
class ParkingSpot {

    private boolean available = true;

    void occupy() {

        if (!available) {
            throw new IllegalStateException(
                "Parking spot already occupied"
            );
        }

        available = false;
    }

    void release() {
        available = true;
    }

    boolean isAvailable() {
        return available;
    }
}
```

The state is:

```
available
```

The behavior is:

```
occupy()
release()
isAvailable()
```

This naturally leads to **encapsulation**, which is the next concept.

---

## **🗺️ Diagram**

```
classDiagram
    class ParkingSpot {
        -boolean available
        +occupy()
        +release()
        +isAvailable()
    }

    ParkingSpot : State = available
    ParkingSpot : Behavior = occupy/release
```

---

## **🏢 Real-World Application**

Domain objects often own behavior related to their state:

```
Order
 ├── confirm()
 ├── cancel()
 └── markDelivered()

Payment
 ├── authorize()
 ├── capture()
 └── refund()

Booking
 ├── confirm()
 ├── cancel()
 └── reschedule()
```

However, not every operation belongs inside the entity.

Cross-object workflows often belong to services:

```
BookingService
    ├── Booking
    ├── PaymentService
    └── NotificationService
```

---

## **⚖️ Trade-offs**

### **Good object behavior**

Keeps business rules close to the state they protect.

### **Potential problem**

Putting every operation into entities can create large “god objects”.

Use services for workflows involving multiple independent objects.

---

## **🎯 Interview Questions**

1. What is state?
2. What is behavior?
3. Why should an object own behavior related to its state?
4. Should every business operation be placed inside an entity?
5. When should logic belong to a service instead?
6. Why is `booking.cancel()` often preferable to directly modifying `booking.status` ?

---

## **🧪 Practice Problem**

Design an `Order` class with:

```
State:
- status
- totalAmount

Behavior:
- confirm()
- cancel()
- markDelivered()
```

Define which state transitions are valid.

---

## **⚠️ Mistakes / Gotchas**

- State ≠ behavior.
- Don’t expose mutable state unnecessarily.
- Not every operation belongs inside an entity.
- Cross-object workflows may belong in services.

---

## **🔑 Key Takeaways**

```
State    → what the object currently is
Behavior → what the object can do
```

Good OO design often lets objects protect and modify their own state through meaningful behavior.

---

## **🔗 Related Concepts**

- Encapsulation
- Domain Modeling
- State Machines
- Service Layer

---

## **🚧 Pending / Related Topics**

- 01.3 Encapsulation

---

# **01.3 · Encapsulation**

## **❓ Problem**

In the previous example, `Booking` owned its state transition.

But what stops another class from directly changing the state?

```
booking.status = CANCELLED;
```

We need a mechanism to control access to internal state.

That is where encapsulation comes in.

---

## **📋 Prerequisites**

- 01.1 Class & Object
- 01.2 State & Behavior

---

## **🎯 Why This Exists**

Encapsulation protects an object’s internal state and ensures that changes happen through controlled operations.

The goal is not simply:

“Make every variable private.”

The deeper goal is:

**Protect invariants and control how state can change.**

---

## **🧠 Core Concept**

Encapsulation combines:

```
Internal State
      +
Behavior that controls that state
      +
Controlled access
```

Example:

```
class BankAccount {

    private double balance;

    public void deposit(double amount) {
        if (amount <= 0) {
            throw new IllegalArgumentException();
        }

        balance += amount;
    }
}
```

The caller cannot directly do:

```
account.balance = -100000;
```

because `balance` is private.

Instead:

```
account.deposit(5000);
```

The class controls the transition.

---

## **🌍 Real-World Analogy**

An ATM doesn’t allow you to open the bank’s database and modify your balance.

Instead, you interact through controlled operations:

```
ATM
 │
 ├── Deposit
 ├── Withdraw
 └── Balance Check
```

The bank controls what happens internally.

Similarly:

```
Object
 │
 ├── Public behavior
 │
 └── Private implementation/state
```

---

## **❌ Bad Design**

```
class BankAccount {

    public double balance;
}
```

Any caller can do:

```
account.balance = -50000;
```

Business rules can easily be bypassed.

---

## **✅ Better Design**

```
class BankAccount {

    private double balance;

    public void deposit(double amount) {

        if (amount <= 0) {
            throw new IllegalArgumentException(
                "Amount must be positive"
            );
        }

        balance += amount;
    }

    public void withdraw(double amount) {

        if (amount <= 0 || amount > balance) {
            throw new IllegalArgumentException(
                "Invalid withdrawal"
            );
        }

        balance -= amount;
    }

    public double getBalance() {
        return balance;
    }
}
```

The object protects its invariant:

```
balance >= 0
```

---

## **💻 Code Example**

Parking spot:

```
class ParkingSpot {

    private boolean available = true;

    public void occupy() {

        if (!available) {
            throw new IllegalStateException(
                "Spot already occupied"
            );
        }

        available = false;
    }

    public void release() {
        available = true;
    }

    public boolean isAvailable() {
        return available;
    }
}
```

The caller doesn’t directly manipulate `available`.

---

## **🗺️ Diagram**

```
classDiagram
    class ParkingSpot {
        -boolean available
        +occupy()
        +release()
        +isAvailable()
    }

    class Client

    Client --> ParkingSpot : controlled operations
```

---

## **🏢 Real-World Application**

Encapsulation appears everywhere:

```
Order
 └── controls valid state transitions

Payment
 └── controls payment status

Inventory
 └── controls stock changes

Account
 └── controls balance changes
```

---

## **⚖️ Trade-offs**

### **Benefits**

- Protects invariants
- Reduces accidental state corruption
- Centralizes validation
- Makes internal implementation easier to change

### **Trade-off**

Overly restrictive objects can make legitimate operations difficult.

Encapsulation should provide the **right interface**, not hide everything blindly.

---

## **🎯 Interview Questions**

1. What is encapsulation?
2. Is encapsulation simply making fields private?
3. Why should state be protected?
4. What is an invariant?
5. How does encapsulation improve maintainability?
6. What is the difference between encapsulation and abstraction?

---

## **🧪 Practice Problem**

Create:

```
class Inventory
```

with:

```
stock
addStock()
removeStock()
getStock()
```

Ensure stock can never become negative.

---

## **⚠️ Mistakes / Gotchas**

### **Encapsulation ≠****`private`**

`private` is a Java mechanism.

Encapsulation is the broader design idea of controlling state and behavior.

### **Getter for everything is not automatically good encapsulation**

This:

```
getBalance()
setBalance()
```

may simply recreate public mutable state.

Prefer meaningful operations:

```
deposit()
withdraw()
```

---

## **🔑 Key Takeaways**

```
Encapsulation
      ↓
Protect internal state
      ↓
Control state changes
      ↓
Protect invariants
```

---

## **🔗 Related Concepts**

- State & Behavior
- Abstraction
- Information Hiding
- SOLID
- Domain Modeling

---

## **🚧 Pending / Related Topics**

- 01.4 Abstraction

---

# **01.4 · Abstraction**

## **❓ Problem**

Encapsulation protects internal state.

But another problem remains.

Suppose we have:

```
Payment
├── UPI
├── Card
└── Wallet
```

Each payment mechanism has different implementation details.

The caller should not need to know all of them.

We need to define:

What can the payment system do?

without exposing:

How does each payment mechanism do it?

---

## **📋 Prerequisites**

- 01.1 Class & Object
- 01.2 State & Behavior
- 01.3 Encapsulation

---

## **🎯 Why This Exists**

Abstraction reduces unnecessary complexity for the caller.

The caller should depend on the **essential contract**, not implementation details.

---

## **🧠 Core Concept**

Abstraction means:

```
Expose what is necessary
Hide what is unnecessary
```

For payments:

```
interface PaymentProcessor {

    void pay(PaymentRequest request);
}
```

The caller knows:

```
PaymentProcessor
      ↓
     pay()
```

It doesn’t need to know how UPI or Card processing works internally.

---

## **🌍 Real-World Analogy**

When you use a UPI app, you press:

```
Pay ₹500
```

You don’t need to understand:

```
Bank routing
Authentication
Network calls
Transaction processing
Settlement
```

The system exposes a simple operation.

---

## **❌ Bad Design**

```
class PaymentService {

    void pay(String type) {

        if (type.equals("UPI")) {
            // UPI implementation
        } else if (type.equals("CARD")) {
            // Card implementation
        } else if (type.equals("WALLET")) {
            // Wallet implementation
        }
    }
}
```

The high-level service knows too many implementation details.

---

## **✅ Better Design**

Define an abstraction:

```
interface PaymentProcessor {
    void pay(PaymentRequest request);
}
```

Implementations:

```
class UpiPaymentProcessor implements PaymentProcessor {

    @Override
    public void pay(PaymentRequest request) {
        // UPI implementation
    }
}
```

```
class CardPaymentProcessor implements PaymentProcessor {

    @Override
    public void pay(PaymentRequest request) {
        // Card implementation
    }
}
```

The service depends on the abstraction:

```
class PaymentService {

    private final PaymentProcessor processor;

    PaymentService(PaymentProcessor processor) {
        this.processor = processor;
    }

    void pay(PaymentRequest request) {
        processor.pay(request);
    }
}
```

---

## **💻 Code Example**

A common concern is:

UPI and Card need different data. How can one interface work?

The interface does not mean every implementation must have identical internal data.

Use a stable business request and specialized details:

```
class PaymentRequest {

    private final double amount;
    private final PaymentDetails details;

    PaymentRequest(
        double amount,
        PaymentDetails details
    ) {
        this.amount = amount;
        this.details = details;
    }
}
```

Then:

```
interface PaymentDetails {
}
```

```
class UpiDetails implements PaymentDetails {

    private final String upiId;
}
```

```
class CardDetails implements PaymentDetails {

    private final String cardToken;
}
```

The implementation can interpret the relevant details.

Avoid a giant object containing every possible field:

```
PaymentRequest
├── upiId
├── cardNumber
├── cardCvv
├── walletId
├── bankAccount
├── ...
```

---

## **🗺️ Diagram**

```
classDiagram
    class PaymentProcessor {
        <<interface>>
        +pay(PaymentRequest)
    }

    class UpiPaymentProcessor
    class CardPaymentProcessor
    class WalletPaymentProcessor

    PaymentProcessor <|.. UpiPaymentProcessor
    PaymentProcessor <|.. CardPaymentProcessor
    PaymentProcessor <|.. WalletPaymentProcessor

    PaymentService --> PaymentProcessor
```

---

## **🏢 Real-World Application**

The same concept appears in:

```
Notification
├── Email
├── SMS
├── Push
└── WhatsApp

Storage
├── S3
├── GCS
└── Local Storage

Payment
├── UPI
├── Card
└── Wallet
```

---

## **⚖️ Trade-offs**

### **Benefits**

- Reduces coupling
- Hides implementation details
- Makes implementations replaceable
- Enables polymorphism
- Supports extensibility

### **Trade-off**

Bad abstractions create unnecessary complexity.

Do not create an interface merely because “LLD requires interfaces.”

---

## **🎯 Interview Questions**

1. What is abstraction?
2. How is abstraction different from encapsulation?
3. Is an interface the same thing as abstraction?
4. Can an abstract class provide abstraction?
5. How would you model multiple payment methods?
6. How do you handle implementation-specific payment data?
7. Why shouldn’t `PaymentService` know every payment implementation?

---

## **🧪 Practice Problem**

Design a notification abstraction:

```
Email
SMS
Push
```

The client should send a notification without knowing the implementation.

---

## **⚠️ Mistakes / Gotchas**

- Interface ≠ abstraction itself.
- Abstraction is a design concept.
- Interfaces are one mechanism for implementing abstraction.
- Don’t create giant request objects containing every possible implementation-specific field.
- Don’t expose implementation details to high-level services.

---

## **🔑 Key Takeaways**

```
Encapsulation
→ controls internal state

Abstraction
→ controls what clients need to know
```

Abstraction becomes especially powerful when combined with polymorphism.

---

## **🔗 Related Concepts**

- Interface
- Abstract Class
- Polymorphism
- Dependency Inversion
- Dependency Injection
- OCP

---

## **🚧 Pending / Related Topics**

- 01.5 Inheritance
- 01.6 Polymorphism

---

# **01.5 · Inheritance**

## **❓ Problem**

We now know how objects and abstractions work.

But sometimes two classes have a genuine hierarchical relationship.

Example:

```
Vehicle
├── Car
├── Bike
└── Truck
```

All are vehicles.

We may want to represent this relationship directly.

---

## **📋 Prerequisites**

- Class & Object
- State & Behavior
- Encapsulation
- Abstraction

---

## **🎯 Why This Exists**

Inheritance allows a class to derive from another class.

It represents an **IS-A relationship**.

```
Car IS-A Vehicle
Dog IS-A Animal
```

It is more than simply a code-reuse mechanism.

---

## **🧠 Core Concept**

Java:

```
class Vehicle {

    void start() {
        System.out.println("Vehicle starting");
    }
}
```

```
class Car extends Vehicle {

}
```

Now:

```
Car car = new Car();

car.start();
```

`Car` inherits behavior from `Vehicle`.

---

## **🌍 Real-World Analogy**

A car is a type of vehicle.

```
Vehicle
   │
   ├── Car
   ├── Bike
   └── Truck
```

But:

```
Car
   │
   └── Engine
```

is not inheritance.

A car **has an engine**.

That is composition.

---

## **❌ Bad Design**

Using inheritance for a HAS-A relationship:

```
class Engine {
}
```

```
class Car extends Engine {
}
```

This says:

```
Car IS-A Engine
```

which is conceptually wrong.

---

## **✅ Better Design**

```
class Car {

    private final Engine engine;

    Car(Engine engine) {
        this.engine = engine;
    }
}
```

Now:

```
Car HAS-A Engine
```

---

## **💻 Code Example**

```
class Vehicle {

    void start() {
        System.out.println("Vehicle starting");
    }
}
```

```
class Car extends Vehicle {

    @Override
    void start() {
        System.out.println("Car starting");
    }

    void openTrunk() {
        System.out.println("Trunk opened");
    }
}
```

Reference type matters:

```
Vehicle vehicle = new Car();

vehicle.start();
```

Works because `Vehicle` declares `start()`.

But:

```
vehicle.openTrunk();
```

does not compile because `openTrunk()` is not part of the `Vehicle` reference type.

To explicitly invoke parent implementation:

```
@Override
void start() {
    super.start();
    System.out.println("Car starting");
}
```

---

## **🗺️ Diagram**

```
classDiagram
    class Vehicle {
        +start()
    }

    class Car {
        +start()
        +openTrunk()
    }

    Vehicle <|-- Car
```

---

## **🏢 Real-World Application**

Inheritance can be useful for stable domain hierarchies:

```
Payment
├── CardPayment
├── UpiPayment
└── WalletPayment
```

But before using inheritance, ask:

Is this genuinely an IS-A relationship?

Often an interface is better when the goal is capability/contract rather than a shared class hierarchy.

---

## **⚖️ Trade-offs**

### **Benefits**

- Represents genuine hierarchies
- Supports overriding
- Reuses shared implementation
- Enables runtime polymorphism

### **Risks**

- Tight coupling between parent and child
- Fragile hierarchies
- Difficult evolution
- Can lead to class explosion
- Can violate LSP

This is why composition becomes important later.

---

## **🎯 Interview Questions**

1. What is inheritance?
2. What is an IS-A relationship?
3. Why shouldn’t inheritance be used for HAS-A?
4. What does `extends` do?
5. What is method overriding?
6. What is `super` ?
7. What is the difference between reference type and actual object?
8. Does Java support multiple inheritance of classes?

---

## **🧪 Practice Problem**

Design:

```
Vehicle
├── Car
├── Bike
└── Truck
```

Identify:

- Common behavior
- Specialized behavior
- Which behavior should be inherited
- Which relationships should instead use composition

---

## **⚠️ Mistakes / Gotchas**

### **`Vehicle v = new Car()`**

Correct.

```
Vehicle v = new Car();
```

### **`Vehicle v = Car()`**

Incorrect.

An object must be created:

```
Vehicle v = new Car();
```

### **Constructor injection doesn’t change reference type**

If:

```
void process(Animal animal) { }
```

and you pass:

```
Dog dog = new Dog();
process(dog);
```

inside the method the reference is still typed as:

```
Animal
```

---

## **🔑 Key Takeaways**

```
Inheritance → IS-A
Composition → HAS-A
```

Use inheritance when the hierarchy is genuinely stable and behaviorally substitutable.

---

## **🔗 Related Concepts**

- Polymorphism
- Composition
- LSP
- Abstract Class
- Interface

---

## **🚧 Pending / Related Topics**

- 01.6 Polymorphism

---

# **01.6 · Polymorphism**

## **❓ Problem**

Inheritance gives us a hierarchy.

But how can the same piece of code work with different implementations?

For example:

```
PaymentProcessor
├── UPI
├── Card
└── Wallet
```

We want:

```
processor.pay();
```

without writing:

```
if (type == UPI)
if (type == CARD)
if (type == WALLET)
```

---

## **📋 Prerequisites**

- Class & Object
- Inheritance
- Abstraction

---

## **🎯 Why This Exists**

Polymorphism allows one common interface/reference to work with multiple implementations.

It is one of the key mechanisms that makes abstraction useful in real LLD.

---

## **🧠 Core Concept**

Polymorphism means:

One interface/reference, many possible forms.

Runtime polymorphism is primarily achieved through method overriding.

```
interface PaymentProcessor {

    void pay();
}
```

```
class UpiPaymentProcessor implements PaymentProcessor {

    @Override
    public void pay() {
        System.out.println("UPI payment");
    }
}
```

```
class CardPaymentProcessor implements PaymentProcessor {

    @Override
    public void pay() {
        System.out.println("Card payment");
    }
}
```

Now:

```
PaymentProcessor processor =
    new UpiPaymentProcessor();

processor.pay();
```

Later:

```
processor =
    new CardPaymentProcessor();

processor.pay();
```

The client code remains the same.

---

## **🌍 Real-World Analogy**

A payment machine can accept:

```
Payment
├── UPI
├── Card
└── Wallet
```

The machine says:

```
"Process payment"
```

The actual mechanism depends on the payment type.

---

## **❌ Bad Design**

```
class PaymentService {

    void pay(String type) {

        if (type.equals("UPI")) {
            // UPI
        }

        if (type.equals("CARD")) {
            // Card
        }

        if (type.equals("WALLET")) {
            // Wallet
        }
    }
}
```

Every new payment type modifies the service.

---

## **✅ Better Design**

```
PaymentProcessor processor =
    new UpiPaymentProcessor();

processor.pay();
```

The implementation is selected elsewhere.

The consumer depends on:

```
PaymentProcessor
```

not:

```
UpiPaymentProcessor
```

---

## **💻 Code Example**

```
interface NotificationChannel {
    void send(String message);
}
```

```
class EmailNotification implements NotificationChannel {

    @Override
    public void send(String message) {
        System.out.println("Email: " + message);
    }
}
```

```
class SmsNotification implements NotificationChannel {

    @Override
    public void send(String message) {
        System.out.println("SMS: " + message);
    }
}
```

```
NotificationChannel notification =
    new EmailNotification();

notification.send("Order confirmed");
```

The same variable can reference another implementation:

```
notification = new SmsNotification();

notification.send("Order confirmed");
```

---

## **🗺️ Diagram**

```
classDiagram
    class NotificationChannel {
        <<interface>>
        +send(String message)
    }

    class EmailNotification
    class SmsNotification
    class PushNotification

    NotificationChannel <|.. EmailNotification
    NotificationChannel <|.. SmsNotification
    NotificationChannel <|.. PushNotification

    Client --> NotificationChannel
```

---

## **🏢 Real-World Application**

Polymorphism appears in:

```
PaymentProcessor
├── UPI
├── Card
└── Wallet

NotificationChannel
├── Email
├── SMS
└── Push

DiscountStrategy
├── Regular
├── Premium
└── VIP
```

This allows systems to replace behavior without changing the consumer.

---

## **⚖️ Trade-offs**

### **Benefits**

- Removes conditional branching
- Enables extensibility
- Reduces coupling
- Supports OCP
- Makes implementations replaceable

### **Trade-off**

Too many abstractions can make simple code harder to understand.

Use polymorphism when behavior genuinely varies.

---

## **🎯 Interview Questions**

1. What is polymorphism?
2. What is runtime polymorphism?
3. What is compile-time polymorphism?
4. What is method overriding?
5. What is method overloading?
6. Why is polymorphism useful in LLD?
7. What determines which overridden method executes?
8. What determines which methods are accessible through a reference?

---

## **🧪 Practice Problem**

Design a discount system:

```
DiscountStrategy
├── RegularDiscount
├── PremiumDiscount
└── VipDiscount
```

`OrderService` should not contain:

```
if (customerType == ...)
```

---

## **⚠️ Mistakes / Gotchas**

### **Reference type vs actual object**

```
PaymentProcessor processor =
    new UpiPaymentProcessor();
```

Reference type:

```
PaymentProcessor
```

Actual object:

```
UpiPaymentProcessor
```

The reference type determines what methods are accessible.

The actual object determines which overridden implementation executes.

---

## **🔑 Key Takeaways**

```
Abstraction
     +
Polymorphism
     ↓
Replaceable implementations
```

This is one of the most important combinations in LLD.

---

## **🔗 Related Concepts**

- Abstraction
- Interface
- Inheritance
- Composition
- OCP
- DIP

---

## **🚧 Pending / Related Topics**

- 01.7 Composition

---

# **01.7 · Composition**

## **❓ Problem**

Inheritance creates a hierarchy:

```
Vehicle
├── Car
├── Bike
└── Truck
```

But real systems often need to combine **independent behaviors**.

Consider an order:

```
OrderService
├── Payment
├── Delivery
├── Notification
└── Discount
```

Creating inheritance hierarchies for every combination would become unmanageable.

---

## **📋 Prerequisites**

- Class & Object
- Encapsulation
- Abstraction
- Polymorphism
- Inheritance

---

## **🎯 Why This Exists**

Composition allows an object to collaborate with other objects.

It represents a:

```
HAS-A / USES-A
```

relationship.

Example:

```
OrderService
 ├── PaymentProcessor
 ├── DeliveryStrategy
 ├── NotificationChannel
 └── DiscountStrategy
```

---

## **🧠 Core Concept**

```
class Car {

    private final Engine engine;

    Car(Engine engine) {
        this.engine = engine;
    }
}
```

The `Car` has an `Engine`.

Another example:

```
class OrderService {

    private final PaymentProcessor paymentProcessor;

    OrderService(PaymentProcessor paymentProcessor) {
        this.paymentProcessor = paymentProcessor;
    }
}
```

Composition works especially well with interfaces and polymorphism.

---

## **🌍 Real-World Analogy**

A food delivery order doesn’t **become** a payment processor.

It **uses** one.

```
Order
 │
 ├── Payment
 ├── Notification
 ├── Delivery
 └── Discount
```

These are collaborating components.

---

## **❌ Bad Design**

Trying to represent combinations through inheritance:

```
OrderWithUpiAndBikeAndEmail
OrderWithCardAndBikeAndSms
OrderWithWalletAndCarAndPush
...
```

The number of classes grows rapidly.

This is class explosion.

---

## **✅ Better Design**

Use composition:

```
class OrderService {

    private final PaymentProcessor paymentProcessor;
    private final DeliveryStrategy deliveryStrategy;
    private final NotificationChannel notificationChannel;
    private final DiscountStrategy discountStrategy;

    OrderService(
        PaymentProcessor paymentProcessor,
        DeliveryStrategy deliveryStrategy,
        NotificationChannel notificationChannel,
        DiscountStrategy discountStrategy
    ) {
        this.paymentProcessor = paymentProcessor;
        this.deliveryStrategy = deliveryStrategy;
        this.notificationChannel = notificationChannel;
        this.discountStrategy = discountStrategy;
    }
}
```

Now behaviors can vary independently.

---

## **💻 Code Example**

```
interface PaymentProcessor {
    void pay(double amount);
}
```

```
interface NotificationChannel {
    void send(String message);
}
```

```
class OrderService {

    private final PaymentProcessor paymentProcessor;
    private final NotificationChannel notificationChannel;

    OrderService(
        PaymentProcessor paymentProcessor,
        NotificationChannel notificationChannel
    ) {
        this.paymentProcessor = paymentProcessor;
        this.notificationChannel = notificationChannel;
    }

    void placeOrder(double amount) {

        paymentProcessor.pay(amount);

        notificationChannel.send(
            "Order placed"
        );
    }
}
```

The caller can compose different implementations:

```
OrderService service =
    new OrderService(
        new UpiPaymentProcessor(),
        new EmailNotification()
    );
```

Or:

```
OrderService service =
    new OrderService(
        new CardPaymentProcessor(),
        new SmsNotification()
    );
```

---

## **🗺️ Diagram**

```
classDiagram
    class OrderService {
        -PaymentProcessor paymentProcessor
        -NotificationChannel notificationChannel
    }

    class PaymentProcessor {
        <<interface>>
        +pay()
    }

    class NotificationChannel {
        <<interface>>
        +send()
    }

    class UpiPaymentProcessor
    class CardPaymentProcessor
    class EmailNotification
    class SmsNotification

    OrderService --> PaymentProcessor
    OrderService --> NotificationChannel

    PaymentProcessor <|.. UpiPaymentProcessor
    PaymentProcessor <|.. CardPaymentProcessor

    NotificationChannel <|.. EmailNotification
    NotificationChannel <|.. SmsNotification
```

---

## **🏢 Real-World Application**

Composition is everywhere in backend systems:

```
OrderService
├── PaymentGateway
├── InventoryService
├── NotificationService
└── PricingService
```

It is also common in infrastructure components:

```
NotificationService
├── NotificationChannel
├── RetryPolicy
├── EncryptionService
└── Logger
```

Each responsibility can evolve independently.

### **API Design Note**

For an API such as:

```
GET /customers/{id}/orders
```

the request generally enters through:

```
CustomerController
        ↓
Service Layer
        ↓
Repository / Domain
```

Controller-to-controller calls are generally a poor default.

The API resource and service boundaries should determine the design, not simply which entity “owns” another entity.

---

## **⚖️ Trade-offs**

### **Benefits**

- Flexible
- Loosely coupled
- Easy to replace components
- Avoids class explosion
- Supports testing with mocks/fakes

### **Trade-offs**

- More objects
- More wiring/configuration
- Can become over-engineered if used unnecessarily

---

## **🎯 Interview Questions**

1. What is composition?
2. How is composition different from inheritance?
3. Why is composition useful in LLD?
4. How does composition work with polymorphism?
5. Is constructor injection itself composition?
6. Why does composition reduce class explosion?
7. How would you design an `OrderService` with multiple independent behaviors?

---

## **🧪 Practice Problem**

Design an `OrderService` with:

```
Payment
├── UPI
├── Card
└── Wallet

Delivery
├── Bike
└── Car

Notification
├── Email
├── SMS
└── Push

Discount
├── Coupon
├── Membership
└── None
```

Use composition instead of creating a class for every combination.

---

## **⚠️ Mistakes / Gotchas**

### **Composition ≠ constructor injection**

This:

```
OrderService(PaymentProcessor processor)
```

is constructor injection.

The relationship exists because:

```
private final PaymentProcessor processor;
```

stores/collaborates with the dependency.

### **Strict UML composition is stronger**

In UML:

```
◆ Composition
```

implies stronger ownership/lifecycle semantics.

In everyday Java discussions, people often loosely call any HAS-A relationship composition. Be precise in interviews.

---

## **🔑 Key Takeaways**

```
Inheritance
→ builds hierarchies

Composition
→ builds combinations
```

For independent, changeable behaviors, composition is usually the more flexible design.

---

## **🔗 Related Concepts**

- Dependency Injection
- Polymorphism
- Interface
- Composition over Inheritance
- SOLID

---

## **🚧 Pending / Related Topics**

- 01.8 Association / Aggregation / Composition

---

# **01.8 · Association / Aggregation / Composition**

## **❓ Problem**

We know that objects can collaborate.

But not every relationship means the same thing.

Consider:

```
Customer ─── Restaurant
Company ─── Employee
Order ─── OrderItem
```

These relationships have different ownership and lifecycle semantics.

We need to model them accurately.

---

## **📋 Prerequisites**

- Class & Object
- Composition
- Object relationships

---

## **🎯 Why This Exists**

LLD interviews often require you to identify:

- who knows whom
- who owns whom
- whether objects can exist independently
- whether one object’s lifecycle depends on another

---

## **🧠 Core Concept**

There are three commonly discussed relationships:

```
Association
Aggregation
Composition
```

Think of them as increasing semantic strength:

```
Association
    ↓
Aggregation
    ↓
Composition
```

This is a conceptual progression, not a rule that every relationship must move through all three.

---

### **01.8.1 Association**

Association simply means:

Two objects are related or interact.

There is no implied ownership.

Example:

```
Customer ───── Restaurant
```

A customer can exist without a restaurant.

A restaurant can exist without a specific customer.

---

### **01.8.2 Aggregation**

Aggregation represents a whole-part relationship where the part can independently exist.

UML:

```
◇
```

Example:

```
Company ◇── Employee
```

An employee can exist even if they leave that company.

Other examples under appropriate lifecycle assumptions:

```
Playlist ◇── Song
Team ◇── Player
University ◇── Department
```

---

### **01.8.3 Composition**

Composition is a stronger whole-part relationship.

UML:

```
◆
```

The part’s lifecycle is strongly tied to the whole.

Example:

```
Order ◆── OrderItem
```

Under this model:

```
Order deleted
    ↓
OrderItems no longer exist
```

---

## **🌍 Real-World Analogy**

### **Association**

```
Customer ─── Restaurant
```

They interact.

### **Aggregation**

```
Team ◇── Player
```

A player can exist independently of a particular team.

### **Composition**

```
Order ◆── OrderItem
```

An order item exists as part of a particular order.

---

## **❌ Bad Design**

Calling every HAS-A relationship composition:

```
Company ◆── Employee
```

without considering lifecycle.

Or:

```
Customer ◆── Restaurant
```

simply because they interact.

The relationship type must come from the domain requirements.

---

## **✅ Better Design**

Ask:

```
1. Are these objects related?
        ↓
     Association

2. Is one a whole and another a part?
        ↓
     Aggregation / Composition

3. Can the part exist independently?
        ↓
     Yes → Aggregation
     No  → Composition
```

---

## **💻 Code Example**

### **Association**

```
class Customer {
}

class Restaurant {
}

class OrderService {

    void placeOrder(
        Customer customer,
        Restaurant restaurant
    ) {
        // interaction
    }
}
```

There is a relationship without ownership.

### **Aggregation**

```
class Team {

    private final List<Player> players;

    Team(List<Player> players) {
        this.players = players;
    }
}
```

Players can exist independently.

### **Composition**

```
class Order {

    private final List<OrderItem> items =
        new ArrayList<>();

    void addItem(Product product, int quantity) {
        items.add(
            new OrderItem(product, quantity)
        );
    }
}
```

Here `Order` owns the lifecycle of its `OrderItem`s under this model.

---

## **🗺️ Diagram**

```
classDiagram

    class Customer
    class Restaurant

    class Company
    class Employee

    class Order
    class OrderItem

    Customer --> Restaurant : association
    Company o-- Employee : aggregation
    Order *-- OrderItem : composition
```

Legend:

```
──> Association
◇── Aggregation
◆── Composition
```

---

## **🏢 Real-World Application**

These distinctions help during domain modeling.

Example:

```
Food Delivery

Customer ─── Restaurant
        association

Restaurant ◇── MenuItem
        aggregation
        (depending on lifecycle/domain model)

Order ◆── OrderItem
        composition
        under order-owned lifecycle
```

The exact relationship depends on requirements.

There is no universal rule that a particular real-world relationship must always be aggregation or composition.

---

## **⚖️ Trade-offs**

The main trade-off is **semantic precision**.

Overusing composition can imply ownership that doesn’t actually exist.

Overusing aggregation can fail to communicate lifecycle dependency.

Association is often enough when ownership is irrelevant.

---

## **🎯 Interview Questions**

1. What is association?
2. What is aggregation?
3. What is composition?
4. What is the difference between aggregation and composition?
5. What does the hollow diamond mean?
6. What does the filled diamond mean?
7. Is every HAS-A relationship composition?
8. Is `Company → Employee` always aggregation?
9. Why is `Order → OrderItem` often modeled as composition?

---

## **🧪 Practice Problem**

For each relationship, classify it as association, aggregation, or composition **based on explicit lifecycle assumptions**:

```
Customer — Restaurant
Company — Employee
Playlist — Song
Order — OrderItem
House — Room
```

Explain why.

---

## **⚠️ Mistakes / Gotchas**

### **Relationship type depends on requirements**

`House → Room` may be composition under one lifecycle model and a weaker relationship under another.

### **Don’t memorize examples blindly**

Interviewers care more about your reasoning:

```
Who owns it?
Can it exist independently?
Who controls its lifecycle?
```

### **Aggregation is often less important in practical Java code**

The distinction is primarily useful for modeling and communicating domain relationships.

---

## **🔑 Key Takeaways**

```
Association
→ related/interacting objects

Aggregation
→ whole-part + independent lifecycle

Composition
→ whole-part + dependent lifecycle
```

---

## **🔗 Related Concepts**

- Composition
- Domain Modeling
- UML
- Object Relationships
- Lifecycle Ownership

---

## **🚧 Pending / Related Topics**

- 01.9 Interface vs Abstract Class

---

# **01.9 · Interface vs Abstract Class**

## **❓ Problem**

We have now encountered two major ways of defining abstractions:

```
Interface
Abstract Class
```

Both can support abstraction.

The question is:

When should we choose one over the other?

---

## **📋 Prerequisites**

- Abstraction
- Inheritance
- Polymorphism
- Composition

---

## **🎯 Why This Exists**

Choosing the wrong abstraction mechanism can create unnecessary coupling.

We need to distinguish between:

```
Common capability/contract
```

and:

```
Common base family/state/implementation
```

---

## **🧠 Core Concept**

### **Interface**

An interface primarily defines a contract/capability.

```
interface PaymentProcessor {

    void pay();
}
```

Multiple unrelated classes can implement it.

```
class UpiPaymentProcessor
    implements PaymentProcessor {
}

class CardPaymentProcessor
    implements PaymentProcessor {
}
```

A Java class can implement multiple interfaces.

---

### **Abstract Class**

An abstract class represents a common base abstraction.

It can contain:

- state
- concrete methods
- abstract methods
- constructors

Example:

```
abstract class Vehicle {

    void start() {
        System.out.println("Starting");
    }

    abstract void fuelType();
}
```

Subclass:

```
class Car extends Vehicle {

    @Override
    void fuelType() {
        System.out.println("Petrol");
    }
}
```

---

## **🌍 Real-World Analogy**

### **Interface**

```
PaymentProcessor
```

Different payment systems can provide the capability:

```
UPI
Card
Wallet
```

There doesn’t need to be a shared implementation-heavy base class.

### **Abstract Class**

```
Vehicle
```

Different vehicles share meaningful common behavior:

```
start()
```

but may implement:

```
fuelType()
```

differently.

---

## **❌ Bad Design**

Using an abstract class simply because multiple classes have one common method:

```
abstract class Notification {
    abstract void send();
}
```

when the implementations don’t actually share meaningful state or implementation.

An interface may communicate the design better:

```
interface NotificationChannel {
    void send(String message);
}
```

---

## **✅ Better Design**

### **Payment**

Use an interface:

```
interface PaymentProcessor {
    void pay();
}
```

### **Vehicle family**

Use an abstract class when shared implementation/state makes sense:

```
abstract class Vehicle {

    void start() {
        System.out.println("Starting");
    }

    abstract void fuelType();
}
```

### **Notification**

Use an interface:

```
interface NotificationChannel {
    void send(String message);
}
```

---

## **💻 Code Example**

```
interface PaymentProcessor {

    void pay(double amount);
}
```

```
class UpiPaymentProcessor
    implements PaymentProcessor {

    @Override
    public void pay(double amount) {
        System.out.println("UPI: " + amount);
    }
}
```

Abstract class:

```
abstract class Vehicle {

    void start() {
        System.out.println("Starting vehicle");
    }

    abstract void fuelType();
}
```

```
class Car extends Vehicle {

    @Override
    void fuelType() {
        System.out.println("Petrol");
    }
}
```

Usage:

```
PaymentProcessor payment =
    new UpiPaymentProcessor();

Vehicle vehicle =
    new Car();
```

---

## **🗺️ Diagram**

```
classDiagram

    class PaymentProcessor {
        <<interface>>
        +pay()
    }

    class UpiPaymentProcessor
    class CardPaymentProcessor

    PaymentProcessor <|.. UpiPaymentProcessor
    PaymentProcessor <|.. CardPaymentProcessor

    class Vehicle {
        <<abstract>>
        +start()
        +fuelType()*
    }

    class Car
    class Bike

    Vehicle <|-- Car
    Vehicle <|-- Bike
```

---

## **🏢 Real-World Application**

Use interfaces commonly for:

```
PaymentProcessor
NotificationChannel
DiscountStrategy
DeliveryStrategy
Repository
PaymentGateway
```

Abstract classes can be useful when subclasses genuinely share:

```
State
Behavior
Invariant
Template algorithm
```

---

## **⚖️ Trade-offs**

| **Interface** | **Abstract Class** |
| --- | --- |
| Contract/capability | Common base abstraction |
| Multiple interfaces possible | Single class inheritance |
| Less coupling to class hierarchy | Stronger hierarchy coupling |
| Good for interchangeable implementations | Good for shared state/implementation |

Modern Java interfaces can also contain `default` and `static` methods, so avoid the outdated rule that interfaces can contain “only abstract methods.”

---

## **🎯 Interview Questions**

1. What is an interface?
2. What is an abstract class?
3. When would you use an interface?
4. When would you use an abstract class?
5. Can an interface contain implementation in modern Java?
6. Can a class implement multiple interfaces?
7. Can a class extend multiple classes?
8. Can an abstract class have constructors?
9. Can an abstract class contain concrete methods?
10. Can an abstract class implement an interface?

---

## **🧪 Practice Problem**

Choose interface or abstract class:

```
Payment Types
Notification Channels
Vehicle Family
Discount Strategies
```

Explain your reasoning rather than memorizing the answer.

---

## **⚠️ Mistakes / Gotchas**

### **Interface ≠ abstraction**

An interface is a mechanism for defining contracts.

Abstraction is the broader design concept.

### **Abstract class ≠ “just inheritance”**

It can provide:

```
Shared state
Shared behavior
Abstract behavior
Construction logic
```

### **Java inheritance syntax**

Correct:

```
Vehicle v = new Car();
```

Incorrect:

```
Vehicle v = Car();
```

---

## **🔑 Key Takeaways**

Use:

```
Interface
→ common contract/capability

Abstract Class
→ common base + shared state/behavior
```

The decision should come from the domain and design needs.

---

## **🔗 Related Concepts**

- Abstraction
- Inheritance
- Polymorphism
- Composition
- DIP

---

## **🚧 Pending / Related Topics**

- 01.10 Favor Composition Over Inheritance

---

# **01.10 · Favor Composition Over Inheritance**

## **❓ Problem**

Inheritance can model genuine hierarchies.

But using inheritance for every variation creates rigid designs.

Consider notifications:

```
Notification
├── Email
│   ├── RetryEmail
│   ├── EncryptedEmail
│   └── RetryEncryptedEmail
├── SMS
│   ├── RetrySMS
│   └── EncryptedSMS
└── Push
    └── ...
```

Independent behaviors are being encoded into the inheritance hierarchy.

This causes class explosion.

---

## **📋 Prerequisites**

- Inheritance
- Polymorphism
- Composition
- Interface vs Abstract Class

---

## **🎯 Why This Exists**

The principle says:

Prefer composition over inheritance when behavior needs to vary independently.

Inheritance builds a hierarchy.

Composition builds combinations.

---

## **🧠 Core Concept**

Suppose notification has independent concerns:

```
Channel
Retry
Encryption
Logging
```

Instead of:

```
RetryEmailNotification
EncryptedEmailNotification
RetryEncryptedEmailNotification
```

compose them:

```
NotificationService
├── NotificationChannel
├── RetryPolicy
├── EncryptionService
└── Logger
```

---

## **🌍 Real-World Analogy**

Think about ordering food.

You don’t create:

```
PremiumOrderWithUPIAndBikeAndEmail
```

You combine:

```
Order
├── Payment
├── Delivery
├── Notification
└── Discount
```

Each dimension can change independently.

---

## **❌ Bad Design**

```
PaymentNotification
├── UpiEmailNotification
├── CardEmailNotification
├── UpiSmsNotification
├── CardSmsNotification
├── UpiPushNotification
└── ...
```

Adding one new dimension multiplies classes.

---

## **✅ Better Design**

```
interface NotificationChannel {
    void send(String message);
}
```

```
class RetryPolicy {

    void execute(Runnable action) {
        // retry logic
    }
}
```

```
class EncryptionService {

    String encrypt(String message) {
        return message;
    }
}
```

```
class NotificationService {

    private final NotificationChannel channel;
    private final RetryPolicy retryPolicy;
    private final EncryptionService encryptionService;

    NotificationService(
        NotificationChannel channel,
        RetryPolicy retryPolicy,
        EncryptionService encryptionService
    ) {
        this.channel = channel;
        this.retryPolicy = retryPolicy;
        this.encryptionService = encryptionService;
    }
}
```

Now the dimensions are independent.

---

## **💻 Code Example**

Food delivery example:

```
class OrderService {

    private final PaymentProcessor paymentProcessor;
    private final DeliveryStrategy deliveryStrategy;
    private final NotificationChannel notificationChannel;
    private final DiscountStrategy discountStrategy;

    OrderService(
        PaymentProcessor paymentProcessor,
        DeliveryStrategy deliveryStrategy,
        NotificationChannel notificationChannel,
        DiscountStrategy discountStrategy
    ) {
        this.paymentProcessor = paymentProcessor;
        this.deliveryStrategy = deliveryStrategy;
        this.notificationChannel = notificationChannel;
        this.discountStrategy = discountStrategy;
    }
}
```

Possible combinations:

```
UPI + Bike + Email + Coupon
Card + Car + SMS + Membership
Wallet + Bike + Push + None
```

No new class is required for each combination.

---

## **🗺️ Diagram**

```
classDiagram
    class OrderService {
        -PaymentProcessor paymentProcessor
        -DeliveryStrategy deliveryStrategy
        -NotificationChannel notificationChannel
        -DiscountStrategy discountStrategy
    }

    class PaymentProcessor {
        <<interface>>
        +pay()
    }

    class DeliveryStrategy {
        <<interface>>
        +deliver()
    }

    class NotificationChannel {
        <<interface>>
        +send()
    }

    class DiscountStrategy {
        <<interface>>
        +calculate()
    }

    OrderService --> PaymentProcessor
    OrderService --> DeliveryStrategy
    OrderService --> NotificationChannel
    OrderService --> DiscountStrategy
```

---

## **🏢 Real-World Application**

Common examples:

```
Notification
├── Channel
├── RetryPolicy
├── Logger
└── Encryption

Order
├── PaymentStrategy
├── DeliveryStrategy
├── DiscountStrategy
└── NotificationChannel
```

This pattern is especially useful when behaviors can change independently.

---

## **⚖️ Trade-offs**

### **Composition benefits**

- Flexible
- Runtime replacement
- Lower coupling
- Avoids hierarchy explosion
- Independent evolution

### **When inheritance is still appropriate**

Inheritance is not bad.

Use it when:

```
A genuinely IS-A B
```

and the subtype can honor the parent’s behavioral contract.

---

## **🎯 Interview Questions**

1. Why prefer composition over inheritance?
2. Is inheritance bad?
3. When should inheritance be used?
4. What is class explosion?
5. How does composition prevent class explosion?
6. Give a real-world example where composition is better.
7. Does Java support multiple inheritance of classes?
8. What is the relationship between composition and polymorphism?

---

## **🧪 Practice Problem**

Design a notification system supporting:

```
Channels:
Email / SMS / Push

Features:
Retry
Encryption
Logging
```

Avoid creating a subclass for every combination.

---

## **⚠️ Mistakes / Gotchas**

### **“Java doesn’t support multiple inheritance” is not the main reason**

Java indeed doesn’t support multiple inheritance of classes.

But the deeper design problem is:

```
Independent behaviors
+
Inheritance hierarchy
=
Rigid design / class explosion
```

Composition solves the design problem by allowing independent capabilities to be combined.

---

## **🔑 Key Takeaways**

```
Inheritance
→ stable IS-A hierarchy

Composition
→ independent behaviors that need to be combined
```

The principle is not:

Never use inheritance.

It is:

Don’t use inheritance when composition provides a more flexible model.

---

## **🔗 Related Concepts**

- Composition
- Polymorphism
- Strategy Pattern
- SOLID
- OCP
- DIP

---

## **🚧 Pending / Related Topics**

- 01.11 SOLID-Friendly OOP

---

# **01.11 · SOLID-Friendly OOP**

## **❓ Problem**

We have now built the core OOP toolkit:

```
Class & Object
State & Behavior
Encapsulation
Abstraction
Inheritance
Polymorphism
Composition
Interfaces
```

But knowing individual concepts isn’t enough.

LLD interviews ask:

Can you combine these concepts to create maintainable designs?

SOLID gives us a set of design principles for doing that.

---

## **📋 Prerequisites**

- All previous 01.x topics
- Especially abstraction
- Polymorphism
- Composition
- Interfaces

---

## **🎯 Why This Exists**

OOP gives us mechanisms.

SOLID helps us reason about how those mechanisms should be used.

```
OOP mechanisms
      ↓
Good design principles
      ↓
Maintainable LLD
```

---

## **🧠 Core Concept**

SOLID:

```
S → Single Responsibility Principle
O → Open/Closed Principle
L → Liskov Substitution Principle
I → Interface Segregation Principle
D → Dependency Inversion Principle
```

---

# **S — Single Responsibility Principle**

## **❓ Problem**

A class that does too many unrelated things becomes difficult to change.

Bad:

```
class PaymentService {

    void processPayment() {}
    void validatePayment() {}
    void saveToDatabase() {}
    void sendEmail() {}
}
```

There are several independent reasons this class might change.

---

## **🧠 Core Concept**

A class should have one primary reason to change.

It does **not** mean:

A class can only have one method.

For example:

```
class UserService {

    void createUser() {}
    void updateUser() {}
}
```

These can reasonably belong together because both concern the user lifecycle.

But:

```
UserService
├── User lifecycle
├── Email sending
├── Report generation
└── Database implementation
```

mixes unrelated responsibilities.

---

## **❌ Bad Design**

```
class PaymentService {

    void processPayment() {
        validatePayment();
        calculateFee();
        savePayment();
        sendEmail();
    }

    void validatePayment() {}
    void calculateFee() {}
    void savePayment() {}
    void sendEmail() {}
}
```

---

## **✅ Better Design**

```
PaymentService
    ↓ orchestrates

PaymentValidator
PaymentRepository
FeeCalculator
NotificationService
```

Possible structure:

```
class PaymentService {

    private final PaymentValidator validator;
    private final PaymentRepository repository;
    private final FeeCalculator feeCalculator;
    private final NotificationService notificationService;

    void processPayment() {
        // orchestration
    }
}
```

`calculateFee()` should not automatically be moved to `Order`.

Ownership depends on the actual business rule.

---

## **🌍 Real-World Analogy**

A restaurant waiter:

```
Takes order
Coordinates kitchen
Delivers bill
```

doesn’t need to:

```
Cook the food
Maintain the database
Repair the POS machine
Manage payroll
```

Each concern has a suitable owner.

---

# **O — Open/Closed Principle**

## **❓ Problem**

Consider:

```
class PaymentService {

    void pay(String type) {

        if (type.equals("UPI")) {
            // ...
        } else if (type.equals("CARD")) {
            // ...
        }
    }
}
```

Adding a new payment type requires modifying existing logic.

---

## **🧠 Core Concept**

Software entities should be open for extension but closed for unnecessary modification.

Use polymorphism:

```
interface PaymentProcessor {
    void pay();
}
```

Then:

```
PaymentProcessor
├── UPI
├── Card
└── Wallet
```

`PaymentService` depends on the abstraction.

Adding a new implementation does not require adding another `if/else` branch to the service.

---

## **❌ Bad Design**

```
if (type.equals("UPI")) {
}
else if (type.equals("CARD")) {
}
else if (type.equals("WALLET")) {
}
```

---

## **✅ Better Design**

```
interface DiscountStrategy {
    double calculate(double amount);
}
```

```
class RegularDiscount
    implements DiscountStrategy {
}
```

```
class PremiumDiscount
    implements DiscountStrategy {
}
```

```
class VipDiscount
    implements DiscountStrategy {
}
```

Then:

```
class DiscountService {

    private final DiscountStrategy strategy;

    DiscountService(DiscountStrategy strategy) {
        this.strategy = strategy;
    }
}
```

---

## **🌍 Real-World Application**

The same principle applies to:

```
Payment
Notification
Discount
Delivery
Storage
Shipping
```

---

# **L — Liskov Substitution Principle**

## **❓ Problem**

Inheritance says:

```
B IS-A A
```

But is that enough?

Consider:

```
class Bird {
    void fly() {}
}
```

Then:

```
class Penguin extends Bird {
    @Override
    void fly() {
        throw new UnsupportedOperationException();
    }
}
```

Now:

```
Bird bird = new Penguin();
bird.fly();
```

The client expected a Bird that can fly.

The subtype breaks the expected behavior.

---

## **🧠 Core Concept**

A subtype should be substitutable for its parent without breaking the parent’s behavioral contract.

Mental model:

```
Inheritance says:
B is A

LSP asks:
Can B actually behave like A
wherever A is expected?
```

---

## **❌ Bad Design**

```
class Vehicle {

    void startEngine() {
    }
}

class Bicycle extends Vehicle {

    @Override
    void startEngine() {
        throw new UnsupportedOperationException();
    }
}
```

A bicycle cannot satisfy the behavioral contract of an engine-powered vehicle.

---

## **✅ Better Design**

Separate capabilities:

```
class Vehicle {
}
```

```
interface EngineVehicle {

    void startEngine();
}
```

```
class Car
    extends Vehicle
    implements EngineVehicle {
}
```

```
class Bicycle
    extends Vehicle {
}
```

Now the abstraction does not promise an engine to every vehicle.

---

## **🌍 Real-World Analogy**

A USB port should fulfill the contract expected from a USB device.

If a device claims to support an operation but always rejects it, substitutability becomes questionable.

In LLD, think in terms of **behavioral contracts**, not just class hierarchy.

---

# **I — Interface Segregation Principle**

## **❓ Problem**

A large interface can force implementations to depend on methods they don’t need.

Bad:

```
interface Worker {

    void work();
    void eat();
    void sleep();
}
```

A robot may not need:

```
eat()
sleep()
```

---

## **🧠 Core Concept**

Clients should not be forced to depend on methods they do not use.

Split large interfaces into cohesive capabilities.

---

## **❌ Bad Design**

```
interface Printer {

    void print();
    void scan();
    void fax();
}
```

A simple printer may only support printing.

---

## **✅ Better Design**

```
interface Printer {
    void print();
}
```

```
interface Scanner {
    void scan();
}
```

```
interface Fax {
    void fax();
}
```

A modern printer can implement all:

```
class ModernPrinter
    implements Printer, Scanner, Fax {
}
```

A simple printer can implement only:

```
class SimplePrinter
    implements Printer {
}
```

---

## **🌍 Real-World Application**

Good capability interfaces:

```
PaymentProcessor
NotificationChannel
Refundable
Retryable
Scannable
Printable
```

ISP does not mean:

One method per interface.

It means:

Split interfaces around cohesive client needs.

---

# **D — Dependency Inversion Principle**

## **❓ Problem**

Consider:

```
class PaymentService {

    private final RazorpayPaymentGateway gateway;

    PaymentService() {
        gateway = new RazorpayPaymentGateway();
    }
}
```

`PaymentService` is tightly coupled to Razorpay.

Changing the gateway requires modifying the high-level service.

---

## **🧠 Core Concept**

DIP states:

High-level modules should not depend directly on low-level modules. Both should depend on abstractions.

And:

Details should depend on abstractions, not the other way around.

---

## **❌ Bad Design**

```
PaymentService
      ↓
RazorpayPaymentGateway
```

The high-level policy knows the implementation detail.

---

## **✅ Better Design**

Define an abstraction:

```
interface PaymentGateway {
    void pay(double amount);
}
```

Implementation:

```
class Razorpay
    implements PaymentGateway {

    @Override
    public void pay(double amount) {
        // gateway implementation
    }
}
```

High-level service:

```
class PaymentService {

    private final PaymentGateway gateway;

    PaymentService(PaymentGateway gateway) {
        this.gateway = gateway;
    }

    void pay(double amount) {
        gateway.pay(amount);
    }
}
```

Now:

```
PaymentService
      ↓
PaymentGateway
      ↑
      │
Razorpay
```

---

## **💻 Code Example**

Complete example:

```
interface PaymentGateway {

    void pay(double amount);
}
```

```
class Razorpay
    implements PaymentGateway {

    @Override
    public void pay(double amount) {
        System.out.println(
            "Processing via Razorpay"
        );
    }
}
```

```
class Stripe
    implements PaymentGateway {

    @Override
    public void pay(double amount) {
        System.out.println(
            "Processing via Stripe"
        );
    }
}
```

```
class PaymentService {

    private final PaymentGateway gateway;

    PaymentService(PaymentGateway gateway) {
        this.gateway = gateway;
    }

    void pay(double amount) {
        gateway.pay(amount);
    }
}
```

Usage:

```
PaymentService service =
    new PaymentService(
        new Razorpay()
    );
```

The service can later use:

```
new Stripe()
```

without changing its core logic.

---

## **🗺️ Diagram**

```
classDiagram

    class PaymentService {
        -PaymentGateway gateway
        +pay()
    }

    class PaymentGateway {
        <<interface>>
        +pay()
    }

    class Razorpay
    class Stripe

    PaymentService --> PaymentGateway
    PaymentGateway <|.. Razorpay
    PaymentGateway <|.. Stripe
```

---

## **🏢 Real-World Application**

DIP is particularly useful at architectural boundaries:

```
Business Logic
      ↓
Abstraction
      ↑
Infrastructure
```

Examples:

```
OrderService
      ↓
PaymentGateway
      ↑
Razorpay / Stripe

OrderService
      ↓
NotificationChannel
      ↑
Email / SMS / Push

Application
      ↓
Repository
      ↑
MySQL / MongoDB
```

---

## **⚖️ Trade-offs**

SOLID improves maintainability but should not be applied mechanically.

### **Over-engineering**

Bad:

```
UserService
 → IUserService
 → UserServiceImpl
 → UserServiceFactory
 → UserServiceProvider
```

when there is no meaningful variation.

The goal is:

Appropriate abstraction.

Not:

Maximum number of interfaces.

---

## **🎯 Interview Questions**

### **SRP**

1. What does SRP actually mean?
2. Does SRP mean one method per class?
3. How do you identify multiple responsibilities?

### **OCP**

4. What does open for extension mean?
5. How does polymorphism help OCP?
6. Does OCP mean never modifying existing code?

### **LSP**

7. What is LSP?
8. Give a real-world violation.
9. How do you identify an LSP violation?

### **ISP**

10. What is ISP?
11. Does ISP mean one method per interface?
12. How would you split a large interface?

### **DIP**

13. What is DIP?
14. What is the difference between DIP and DI?
15. Does DIP require an interface for every dependency?

---

## **🧪 Practice Problem**

Design a food-ordering system:

```
OrderService
├── Payment
│   ├── UPI
│   ├── Card
│   └── Wallet
│
├── Delivery
│   ├── Bike
│   └── Car
│
├── Notification
│   ├── Email
│   ├── SMS
│   └── Push
│
└── Discount
    ├── Coupon
    ├── Membership
    └── None
```

Apply:

```
SRP
OCP
LSP
ISP
DIP
```

Do not create a separate class for every combination.

---

## **⚠️ Mistakes / Gotchas**

### **SRP**

Wrong:

One class = one method.

Correct:

One primary reason to change.

### **OCP**

Wrong:

Never modify existing code.

Correct:

Avoid unnecessary modification of stable core logic when adding new behavior.

### **LSP**

Wrong:

Every subclass must have identical implementation.

Correct:

Subtypes must honor the behavioral contract expected by clients.

### **ISP**

Wrong:

Every interface should have exactly one method.

Correct:

Interfaces should represent cohesive client needs.

### **DIP**

Wrong:

Every dependency must have an interface.

Correct:

High-level policy should not be unnecessarily coupled to replaceable implementation details.

### **DIP ≠ DI**

```
DIP = design principle

DI = mechanism for supplying dependencies
```

Dependency injection can help implement DIP, but they are not the same concept.

---

## **🔑 Key Takeaways**

### **SOLID in one table**

| **Principle** | **Core Idea** |
| --- | --- |
| **SRP** | One primary reason to change |
| **OCP** | Extend behavior without unnecessary modification |
| **LSP** | Subtypes honor parent behavioral contracts |
| **ISP** | Don’t force clients to depend on unused capabilities |
| **DIP** | High-level policy depends on abstractions, not details |

---

## **🔗 Related Concepts**

```
Class & Object
      ↓
State & Behavior
      ↓
Encapsulation
      ↓
Abstraction
      ↓
Polymorphism
      ↓
Composition
      ↓
Interfaces
      ↓
SOLID
      ↓
Design Patterns
      ↓
Domain Modeling
      ↓
Clean Architecture
```

The OOP section provides the foundation for the remaining LLD curriculum.

---

## **🚧 Pending / Related Topics**

The next major section is:

```
02. UML & DESIGN REPRESENTATION
```

Important concepts that build on this section:

```
02.1 UML Fundamentals
02.2 Class Diagrams
02.3 Relationships
02.4 Sequence Diagrams
02.5 Activity Diagrams
02.6 State Diagrams
02.7 Object Interaction Modeling
```

Later sections will build further on the OOP foundation:

```
03. Design Principles
04. Coupling & Cohesion
05. Creational Patterns
06. Structural Patterns
07. Behavioral Patterns
09. Domain Modeling
10. Clean Architecture
11. Dependency Injection
13. Concurrency
17. Machine Coding
18. Classic LLD Problems
19. LLD + Backend Integration
```

---

# **🧠 OOP SECTION — FINAL MENTAL MODEL**

```
                    OBJECT
                       │
              ┌────────┴────────┐
              │                 │
            STATE            BEHAVIOR
              │                 │
              └────────┬────────┘
                       ↓
                ENCAPSULATION
                       │
                       ↓
                  ABSTRACTION
                       │
          ┌────────────┴────────────┐
          ↓                         ↓
     INHERITANCE              COMPOSITION
          │                         │
          ↓                         ↓
   POLYMORPHISM             OBJECT COLLABORATION
          │                         │
          └────────────┬────────────┘
                       ↓
              INTERFACE / ABSTRACT
                    CLASS
                       │
                       ↓
          FAVOR COMPOSITION WHEN
        BEHAVIORS VARY INDEPENDENTLY
                       │
                       ↓
                    SOLID
                       │
       ┌───────┬───────┼───────┬───────┐
       ↓       ↓       ↓       ↓       ↓
      SRP     OCP     LSP     ISP     DIP
                       │
                       ↓
              MAINTAINABLE LLD
```

## **🎯 OOP Interview Checklist**

Before moving to UML, you should be able to explain and apply:

```
✅ Class vs Object
✅ Reference vs Object
✅ State vs Behavior
✅ Encapsulation
✅ Abstraction
✅ Inheritance
✅ IS-A vs HAS-A
✅ Method Overriding
✅ Runtime Polymorphism
✅ Reference Type vs Actual Object
✅ Composition
✅ Association
✅ Aggregation
✅ Composition in UML
✅ Interface
✅ Abstract Class
✅ Interface vs Abstract Class
✅ Composition over Inheritance
✅ Class Explosion
✅ SRP
✅ OCP
✅ LSP
✅ ISP
✅ DIP
✅ DIP vs DI
```

The key progression to remember is:

```
Objects
   ↓
Objects have State + Behavior
   ↓
Protect State → Encapsulation
   ↓
Hide Implementation → Abstraction
   ↓
Model IS-A → Inheritance
   ↓
Multiple Implementations → Polymorphism
   ↓
Combine Objects → Composition
   ↓
Model Relationships Precisely
   ↓
Choose Interface / Abstract Class
   ↓
Prefer Composition for Independent Behaviors
   ↓
Apply SOLID
   ↓
Design Maintainable LLD
```