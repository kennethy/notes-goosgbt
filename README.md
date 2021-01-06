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

