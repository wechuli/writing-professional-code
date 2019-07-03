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

Since many components are involved here, each with a defined relationship to other components, we need to determine how best to verify that everything works as expected and that this quality is maintained. For example, we said `My Code` represents the code that is under the direct responsiblity of the developer. He or she may be writing this code from scratch or mayhave inherited code or a project that must be maintained. It contains functionality- classes, methods, properties, events. The developer must be able to verify that the code does what is says it would do and behaves in a predictable manner even under error conditions.

![](testtypes.PNG)

As can be seen, the boundary between each part of our software solution is validated using different test types to verify everything in working order.

A primary tool in the developer's toolbox is to make sure code quality is verified and maintained is the Unit Test.

The preseding table does not cover all types of testing that have evolved over the years. Come other testing types include:

- **Performance Tests** - tests designed specifically to help us measure the throughput of a part of our system.
- **Stress Tests** - tests designed to observer what happens to our software under a heavy load or stress.
- **Beta Tests** - this is typically the name given to a program or period of time when a select subset of users are given an opportunity to try the software application, or service and give feedback before the final release is completed and delivered.
- **Fuzzy Tests** - testing the behavior of a software system or program, by inputting large amounts of random data and watching for crashes, unexpected behavior and unexpected resource usdage, such as memory leaks.
- **A/B testing** - Users are split into (at least) two groups and interact with similar, but different, versions of your software. The goal is to measure the impact the subtle differences in behavior, design and User Experience (UX) in each version have on the satisfaction of the customer.

## Anatomy of a Test

One of the core characteristics that all tests share is that their main purpose is to test something, that is, to verify that something works or behaves as expected or can be measured when behaving in a certain way. Tests also share characteristics that make them tests. These are listed as follows:

### System Under Test(SUT)

As it's name suggests, this term refers to whatever we are testing. For example, in a Unit Test, it refers to functionality, or a unit of functionality we are testing. In a System Test, it refers to the entire system.

### An Expected Outcome

Except for Fuzzy Tests and, perhaps, Performance and Stress tests, we have a particular outcome in mind when we test. It is usually quite concrete, seen as a fact in most cases. For example, if we wanted to test a mathematical addition function, one test would state the expected outcome of the method Add() on two numbers is a result that is the sum of those numbers. In other cases the outcome is an hypothesis or theory instead.

### A Setup Step

This characteristics refers to whatever it takes to have the code we are testing ready for the test. In an Integration Test, it might mean initializing dependencies. It could mean having test data ready. If the test is very basic, there might not be any setup involved.

### An Action Setup

This is where exercising the SUT takes place. In a Unit Test, it typically means invoking a single mthod on the SUT. Int other types it involves more interaction. During this phase of a test, an outcome or result is captured, to be used in the next phase.

### A verification Step

In this step, the actual result of the action we took on the SUT is compared to the expected result. We say a test has succeeded, or passed, if actual = expected. In more complex tests, the verification can be more complex and involve checking a larger data set.

### Repeatable

Tests have limited value to us if we can't repeat them easily. The number of times we run a test should not alter the outcome of the test unless we have altered the SUT, the setup or some other environmental factor.

### A Tear Down Step

This is the opposite of the setup step and the goal is to leave the test infrastructure and the SUT in a state that allows tests to be repeatable.

## Summary

Software Testing encapsulates a broad spectrum of techniques to verify that the code we write does what it says, and continues to do so over time. In some companies and projects, the bulk of testing is left to a set of testers who test manually and also automate tests. There are many reasons why this is done. Sometimes a team is created with the goal of having people dedicated to that aspect of software development. In critical systems such as Financial Services, where money is at stake, testing is done by another part of a team, or even from another group as a form of Separation of Responsibilities or Segregation of Duties. This is done to prevent fraud and reduce errors caused by the same people building the code and testing it.