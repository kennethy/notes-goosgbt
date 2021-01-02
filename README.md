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
