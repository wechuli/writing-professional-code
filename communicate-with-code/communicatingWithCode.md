# Readable Code

## Introduction to Code Refactoring

Refactoring can be described as follows: "To reqrite existing source code in order to improve its readability, reusability or structure without affecting its meaning or behavior"

### Benefits of Refactoring

- **Reduce complexity** - the less complex, the easier it is to understand and maintain.
- **Make code more readable** - even if the code is naturally comlex, having code that is practically self-describing goes a long way toward helping you learn how it functions
- **Improve code maintainability** - if code is easy to maintain, both the developer maintaining the code and the user benefitting from fatser turnaround of bugs fixes and features, will be happy.
- **Make code easier to test** - we can drastically increase the quality of a codebase amd make future updates more predictable when tests are easy to add.
- **Improve code design** - a good design can give a codebase enough flexibility to allow for those moments when changes or features need to be added.
- **Make code easier to extend and reuse** - a developers job is made easier whenthey can understand the code, make changes with quality and predictability. Consuming code that has been well maintained is also a lot easier.

These are all desirable traits for any code base and make it cheaper to maintain over time. All changes to software come at a cost so being able to make changes that are of high quality and to do so in an efficient manner is a critical success factor.

## Consistency of Style

Coding style matters in aproject because it removes one more thing to worry about as you try to read and understand the code. You will need to tweak your code to aim at being more consistent in terms of positioning of brackets, spacing around comments and making sure we have only one statement per line. If you use a consisten style across large code bases, it will pay dividends and remove one more cognitive load for the person trying to read the code.

## Exit Early with Guard Clauses

If you can exit early from a method, you should consider doing so. It is a good technique for handling obvious error conditions in a code path and helps the reader of your code 'park' thise paths in their head.

## Naming

We can convey a lot of information in a well-creafted variable, method or class name.
Capitalization Conventions. There are many conventions in use across companies, teams, programming languages whenit comes to the naming in their code. Two well-known conventions are PascalCasing and camelCasing. camelCasing is usually used for naming private member variables. We would use PascalCasing for public classes, methods, members.

## Refactoring Duplicate Code
Repetitive code can be moved to their own methods. Since streams use system resources, we will also make sure to release those resources with the help of the using construct.

### Reducing Code Duplication tips
 - **Locally in a class** - wrap in a private method of that class
 - **Useful for entire app** - Add as an internal method as part of a helper/utility class
 - **Useful across apps** - Add to a library or a service outside of this app
 - **Useful for this class and all descendants of it** - Add as an internal method of the base class of the inheritence chain

### Remove String Literals

String literals are a potential code smell and can often lead to coding errors. String literals can also lead to confusion. code Smell is a term of endearment in the Software Development world we give to code or code structures that indicate that something is not quite right. The example in this unit is string literals. The string literals used for arguments in this code give the impression that the developer wasn't quite finished making the code readable and self-describing. Smells often occur with the structure of a piece of software. If a good way of structuring or implementing something is defined as a pattern, a smell can lead to, or result in, anti-patterns

### Remove Redundant Variables

When reviewing code, ask yourself whether each variable is needed. Question its value by at least asking the following:]

- How often is the variable used? If is only used once, then perhaps there is no need for the variable.
- Does it add value in terms of clarification of intent? If it doesn't help explain what the code is supposed to be doing, then what calue does the name bring?

### Remove Control-flow Variables

Typically, the flow of code is controlled through application state or conditions. Control-flow variables are variables that are unnecessarily part of this control flow. Whenever you see a variable like this, see it as an opportunity to make an improvement. It is likely that we can re-structure the flow of logic in our code to remove the need for this kind of variable.

### Simplify When Possible

Simplification is a great way to improve the readability of your code and make it easier to maintain. When you inherit a project, you should look for ways to simplify and refactor code as early as possible. Removing code that isn't needed (see YAGNI below) or code that is not used (dead code) is a great simplification opportunity.

You Aren't Going to Need It


Triple slash comments show up in intellisense
