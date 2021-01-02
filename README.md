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
