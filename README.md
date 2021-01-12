# Growing Object-Oriented Software, Guided by Tests (WIP)

Reading Notes for [Growing Object-Oriented Software, Guided by Tests (Pryce)](http://www.growing-object-oriented-software.com/)

# Chapter 1 - What Is the Point of Test-Driven Development?

### Software Development as a Learning Process

Most software projects are attempting something that nobody (or at least in the organization) has done before. In most cases, there will be surprises and uncertainties. Everyone involved in the project has to learn as it progresses. They need a process to help them cope with uncertainty as their experience grows — *to anticipate unanticipated changes.*

### Feedback is the Fundamental Tool

Use empirical feedback to learn about the system and its use, and then apply that learning back to the system. Deploy completed work to check assumptions against reality and ultimately the progress. Organize projects as a system of nested loops. Inner loops are concerned with the implementation details, whereas the outer loops are concerned with the team and the organization. Learnings from each iteration and then applied back to the system.

```
Incremental Development: Builds a system feature-by-feature. Each feature is implemented as an end-to-end "slice" through all the relevent parts of the system. The system is always integrated and ready for deployment.

Iterative Development: The implementations are features are progressively refined based on feedback.
```

### Practices That Support Change

Code need to be accessible in order to be testable. Tests often drives it towards being cleaner and more modular.

- Write automated tests to catch regression errors and to verify new changes
- Write code that's easy to understand and change. Test-Driven Development (TDD) turns testing into a design activity. 

### Test-Driven Development in a Nutshell

TDD provides feedback on the quality of *implementation* ("Does it work?") and design ("Is it well structured?").
```
Write a failing unit test → → → Make the test pass
        ↑                               ↓
        ↑                               ↓
        ↑                               ↓
        ↑                               ↓
        ↑ ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← 
```

### The Bigger Picture

- Start by writing an acceptance test. It exercises the functionality we want to build, and it tracks the progress.
- Underneath the acceptance test, we follow the unit level test/implement/refactor cycle to develop the feature.

```
Write a failing acceptance test → → →  Write a failing unit test → → → Make the test pass
             ↓                                    ↑                           ↓      ↓
             ↓                                    ↑                           ↓      ↓
             ↓                                    ↑                           ↓      ↓
             ↓                                    ↑                           ↓      ↓
             ↓                                    ↑ ← ← ← ← ← ← ← ← ← ← ← ← ← ←      ↓
             ↓                                                                       ↓
             ↓                                                                       ↓
             ↓                                                                       ↓
             ↓                                                                       ↓
             ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ←
```

### Testing End-To-End

- Acceptance tests exercises the system end-to-end without directly calling its internal code.
- An end-to-end test interacts with the system only from the outside: through the UI, by sending messages as if from third-party systems, by invoking its web services, by parsing reports, and so on.
- It's preferred to have the end-to-end tests exercise both the system and the process by which it's built and deployed.

### Levels of Testing

- Acceptance: Does the whole system work?
- Integration: Does our code work against code we can't change?
- Unit: Do our objects do the right thing, are they convenient to work with?

### External and Internal Quality
- External: How well the system meets the requirements of its customers and users. (Functional, available, reliable)
- Internal: How well the system meets the needs of its developers and administrators. (Easy to understand and easy to change)
- End-to-end tests tell us about how well the team understand the domain
- Unit tests tell us that we haven't broken any classes
- Integration tests falls in between
- Tests would be difficult to write when code is poorly structured. It's a sign to consider refactoring the code. (Listen to the tests)
- Coupling: module A is said to be deeply coupled to module B if changes in module B force a lot of changes in module A
- Cohesion: module A is said to be cohesive when its responsibilities form a meaningful/coherent unit.

# Chapter 2 - Test-Driven Development with Objects

### A Web of Objects

```
The big idea is 'messaging' [...] The key in making great and growable systems is much more to design how its modules communicate rather than what their internal properties and behaviours should be. (Alan Kay)
```

### Values and Objects

Values
- model unchanging quantities or measurements
- immutable and have no individual identity
- - two value instances are effectively the same if they have the same state

Objects
- have an identity, might change state over time, and model computational processes
- mutable state to model their behaviour over time
- two objects of the same type have separate entities even if they have exactly the same state

### Follow the Messages

- A communication pattern is a set of rules that govern how a group of objects talk to each other: the roles they play, what messages they can send and when, and so on.
- Domain model lies within the communication patterns, because they are what gives meaning to the universe of possible relationships between the objects.
- Think of objects in terms of roles, responsibilities, and collaborators; An object is an implementation of one or more roles; a role is a set of related responsibilities; and a responsibility is an obligation to perform a task or know information; A collaboration is an interaction of objects and roles.

### Tell, Don't Ask

- Calling object should describe what it wants in terms of the role that its neighbor plays, and let the called object decide how to make that happen. This is also known as "Tell, Don't Ask" or formally, the *Law of Demeter*. 
- Avoid train-wreck code: `object.getA().getB().getC();`

### But Sometimes Ask

- We *ask* when getting information from values and collections.

### Unit-Testing the Collaborating Objects

- Substitute target object's neighbours with mock objects
- Expectations specify how the target object communicates with its neighbours
- Interface Discovery: tease out the supporting roles our object needs and fill in real implementations as we develop the rest of the system

### Support for TDD with Mock Objects

Mockery: the object that holds the context of a test, creates mock objects, and manages expectations and stubbing for the test.

# Chapter 4 - Kick-Starting the Test-Driven Cycle

### First, Test a Walking Skeleton

- A "walking skeleton" is an implementation of the thinnest possible slice of real functionality that we can automatically build, deploy, and test end-to-end.

### Deciding the Shape of the Walking Skeleton

The point of the "walking skeleton" is to use the writing of the first test to draw out the context of the project, to help the team map out the landscape of their solution - the essential decisions that they must take before they can write any code.

### Build Sources of Feedback

```
Understand the Problem → → Broad-Brush Design (Architecture) → → Automate (Build, Deployment, End-to-end, Tests) → → End-to-end Cycle
          ↓                               ↓                                   ↓                                             ↓
          ↓                               ↓                                   ↓                                             ↓
          ↓                               ↓                                   ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ←
          ↓                               ↓                                                                                 ↓
          ↓                               ↓                                                                                 ↓
          ↓                               ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ←
          ↓                                                                                                                 ↓
          ↓                                                                                                                 ↓
          ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ←
```

### Expose Uncertainty Early

Building out the "walking skeleton" flushes out issues early in the project when there's still time, budget, and goodwill to address them.

# Chapter 5 - Maintaining the Test-Driven Cycle

### Start Each Feature with an Acceptance Test

- Write the acceptance test using only terminology from the application's domain, not from the underlying technologies. This helps to understand what the system should do, without tying us to any of our initial assumptions about the implementation or complicating the test with technological details
- Acceptance tests both test the integration of unit-tested objects and push the project forwards

### Separate Tests That Measure Progress from Those That Catch Regressions

- Organize test suites to reflect the different roles that the tests fullfill.
- Unit and integration tests should run quickly and should run fast
- Acceptance tests for completed features. catch regressions, and should always pass, although they might take longer to run.
- If requirements change, move any affected acceptance tests out of the regression suite back into the in-progress suite.

### Start Testing with the Simplest Success Case

- Start by testing the simplest success cases first. Degenerate cases usually don't provide enough feedback about the validity of the early phases of a project.
- While working through the simple success cases, keep a note of the failure cases, refactorings and other technical tasks that need to be addressed.
- A feature is considered completed and robust once the failure cases are also checked off.

### Write The Test That You'd Want to Read

- Aim to write tests that are easy to understand and express the expectations on how the system should behave

### Watch The Test Fail

- Always watch the test fail before writing the code to make it pass, and check the diagnostic message.
- Ensure the tests fail as expected and the diagnostics clearly indicate why they failed

```
Write a failing test → → Make the diagnostics clear → → Make the test pass → → refactor → → repeat
```

### Develop from the Inputs to the Outputs

- We work our way through the system: from the objects that receive external events, through the intermediate layers, to the central domain model, and then on to other boundary objects that generate an externally visible response.

### Unit-Test Behaviour, Not Methods

- Focus on the features that the object unde test should provide, eac of which may require collaboration with its neighbours and calling more than one of its method.
- Need to know how to use the class to achieve a goal, not how to exercise all the paths through its code.

### Listen to the Tests

- When we find a feature that's difficult to test, we don't just ask ourselves how to test it, but also why is it difficult to test. It's a sign that the design needs improving when it's hard to test.
- Keep up the quality of the system by refactoring when we see a weakness in the design.

```
         ↑ → → → → → → → → → → → → → → → → → → → → → → →
         ↑                                             ↓
Write a failing unit test → → Make the test pass → → Refactor
         ↑                                             ↓
         ↑                                             ↓
         ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ← ←
```

### Tuning the Cycle

- Depending on the project context, balance between exhaustively testing execution paths and testing integrations depending.

# Chapter 6 - Object-Oriented Style

> Always design a thing by considering it in its next larger context - a chair in a room, a room in a house, a house in an environment, an environment in a city plan. -- Eliel Saarinen

### Designing for Maintainability

**Separate of Concerns**: If all the relevant changes are in one area of code, we don't have to hunt around the system to get the job done.

**Higher level of abstraction**: Can get more done if we program by combining components of useful functionality rather than manipulating variables and control flow.

**Ports and Adapters architecture**: the code for the business domain is isolated from its dependencies on technical infrastructure, such as databases and user interfaces.

**Encapsulation**: ensures the behaviour of an object can only be affected through its API.

**Information Hiding**: implementation details concealed behind the abstraction of its API.

**Standard practices to main encapsulation:**
- define immutable value types
- avoid global variables and singleton
- copy collections and mutable values when passing them between objects

### Internal vs. Peers

If we expose too much of an object's internals through its API, its clients/peers will end up doing some of its work. This leads to coupled objects and changes made in one will rippple across to others.

### No And's, Or's, or But's

Object should conform to the single responsibility principle. The responsibility of an object should be described without using any conjunctions ("and", "or").

The principle applies to new abstraction from combined objects as well (when composite simpler than the sum of its parts).

### Object Peer Stereotypes

Three types of relationships among objects loosely categorized:

**Dependencies:** when an object cannot function without some other services. Like a graphics package that depends on a screen or canvas to draw on.

**Notifications** when an object notifies ("fire and forget") interested peers whenever it changes state or perform a significant action. The object neither knows nor cares which peers are listening. Like a button control notifying registered listeners, but it does not know what those listeners will do, neither do the listeners know how the event is dispatched to them.

**Adjustments:** when an object's behaviour is adjusted by its peers to the wider needs of the system. Like a policy object that controls access to another object.

Tip: "New or new not. There is no try". We try to make sure to always create a valid object.

### Composite Simpler Than Sum of its Parts

When composing objects into a new type, we want the new type to exhibit simpler behaviour than all of its components parts considered together. Components parts are hidden and the composed object exposes a simpler abstraction/interface.

```
// from
moneyEditor.getAmountField().setText(String.valueOf(money.amount()));
moneyEditor.getCurrencyField().setText(money.currencyCode());

// initial attempt as per 'Tell, Don't Ask', but object's structure is still exposed (amountField and currencyField)
moneyEditor.setAmountField(money.amount());
moneyEditor.setCurrencyField(money.currencyCode());

// finally
moneyEditor.setValue(money);
```

The rule helps us decide whether an object hides enough information, and it contributes to raising the level of abstraction.

### Context Independence

The context independence rule helps us decide whether an object hides too much or hides the wrong information.

An object is said to be *context-independent* if it has not built-in knowledge about the system in which it executes.

Context independence guides us towards coherent objects that can be applied in different contexts, and towards the systems that we can change by reconfiguring how their objects composed.

# Chapter 7 - Achieving Object-Oriented Design

**Three Aspects of TDD**
1. Starting with a test means we have to describe *what* we want to achieve before we consider *how*.
2. Limit the scope of the test to ensure the object under test has a clear separation of concerns.
3. Dependencies need to be known when writing unit tests for an object. This reinforces *context indepdendence* as object with implicit dependencies would be painful to setup and would make a point of clearing it up.


### Communication over Classification

>An interface describes whether two components will fit together, while a protocol descries whether they will work together.

TDD with mock objects as a techniue to make communications between objects visible.

### Value Types

*Values* are immutable and have no meaningful identity; *Objects* have state, so they have identity and relationships with each other. It's encouraged to define types to represent value concepts in the domain.

Three Techniques for introducing value types:
  
1. **Breaking out:** break out object when it has too many responsibilities, and it's too hard to test.
2. **Budding off:** introduce a placeholder type when there's a new domain concept in the code. It starts off as a class that wraps around a single field, and details will be filled in as the code grows.
3. **Bundling up:** group values that are oftenly used together into a single construct.

### Identify Relationships with Interfaces

Interfaces should be kept as arrow as possible. The fewer methods there are on an interface, the more obvious is its role in the callign object.

### Refactor Interfaces Too

Merge interfaces with similar responsibilities. Split interface if it turns out to represent different concepts.

### Building Up to Higher-Level Programming

Organize the code into two layers: an *implementation layer*, which is the graph of objects, its behaviour is the combined result of how its objects respond to events; and, a *declarative layer* which builds up the object in the implementation layer, using small "sugar" methods and syntax to describe *what* the code will do, while the implementation layer describes how the code does it - Declarative layer is, in effect, a small *domain-specific* language.

# Tips

**Composite Simpler Than the Sum of Its Parts**

The API of a composite object should not be more complicated than that of any of its components.

**One Domain Vocabulary**

A class that uses terms from multiple domains might be violiating *context independence* (p55), unless it's part of a bridging layer.

**The Tests Say...**

Break up an object if it comes t oo large to test easily, or if its test failures become difficult to interpret. Then unit-test the new parts separately.

When writing a test, we ask ourselves, "if this worked, who would know?" If the right answer to that question is not in the target object, it's probably time to introduce a new collaborator.

When the test for an object becomes too complicated to setup - when there are too many moving parts to get the code into the relevant state - consider bundling up some of the collaborating objects.