## Pitfalls of Manual Testing

Manual verification of code is a hit-and-miss. How well your changes are validated depends entirely on how well you manually test and the effort you put in. The following is a list of other weaknesses with the manual testing approach.

- We often omit testing of exceptions or complex code paths and instead stick to testing the "happy path"
- The time it takes to test varies based on who is testing the app
- While you can write a test script and hire some people to run through the test cases, the script document can become stale quickly
- Manual testing is difficult to drive consistently across a team or project. The approach lacks rigor and is prone to interpretation. This can lead to a wide variance in the quality of testing we perform.

To write professional code, we need to view the systematic testing of our changes as a way to guarantee a level of quality and confidence in our work that will ultimately help us move forward, fatser. An for that, we need to look at test automation.


## An Introduction to Software Testing

Testing is a procedure intended to establish and maintain the quality, performance or reliability of a piece of software or a solution, before being taken into widespread use and before shipping updates into widespread use.

## Types of Testing

The type of testing we perform is defined by what we are trying to test. The following is a simplified representation of a software system

![](software.PNG)

This diagram illustrates a typical set of components and relationships in any software system.
- **My code** - the code that is under direct responsibility of the developer
- **Software Components** - represents libraries, components, services the developer uses to implement functionality. `My Code` depends on these components.
- **Software Solution** - represents the package/production that ships. This is what human and software (service) consumers see and interact with. The developer's code is, at the very least, a subset of the solution being shipped.