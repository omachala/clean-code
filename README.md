# Clean Code by Robert C. Martin 
"A Handbook of Agile Software Craftsmanship"

This is a list of my notes from that book for a quick reference in the future. My notes below focus mainly on two areas - functions and testing. Enjoy 🚀

## Functions

### Small
- The first rule of functions is that they should be small. The second rule of functions is that they should be smaller than that.
- This also implies that functions should not be large enough to hold nested structures. Therefore, the indent level of a function should not be greater than one or two. This, of course, makes the functions easier to read and understand.

### Do One Thing
- Functions should do one thing. They should do it well. The should do it only.

### One Level Of Abstraction per Function
- In order to make sure our functions are doing “one thing,” we need to make sure that the statements within our function are all at the same level of abstraction.

### Reading Code from Top to Bottom: The Stepdown Rule
- We want the code to read like a top-down narrative.5 We want every function to be followed by those at the next level of abstraction so that we can read the program, descending one level of abstraction at a time as we read down the list of functions. I call this The Step-down Rule.

### Switch Statements
- It’s hard to make a small switch statement.6 Even a switch statement with only two cases is larger than I’d like a single block or function to be. It’s also hard to make a switch statement that does one thing. By their nature, switch statements always do N things.

### Use Descriptive Names
- Ward’s principle: “You know you are working on clean code when each routine turns out to be pretty much what you expected.” Half the battle to achieving that principle is choosing good names for small functions that do one thing. The smaller and more focused a function is, the easier it is to choose a descriptive name.
- Don’t be afraid to make a name long. A long descriptive name is better than a short enigmatic name. A long descriptive name is better than a long descriptive comment. Use a naming convention that allows multiple words to be easily read in the function names, and then make use of those multiple words to give the function a name that says what it does.
- Don’t be afraid to spend time choosing a name. Indeed, you should try several different names and read the code with each in place.
- Be consistent in your names. Use the same phrases, nouns, and verbs in the function names you choose for your modules.

### Function Arguments
- The ideal number of arguments for a function is zero (niladic). Next comes one (monadic), followed closely by two (dyadic). Three arguments (triadic) should be avoided where possible. More than three (polyadic) requires very special justification—and then shouldn’t be used anyway.
- Arguments are even harder from a testing point of view. Imagine the difficulty of writing all the test cases to ensure that all the various combinations of arguments work properly. If there are no arguments, this is trivial. If there’s one argument, it’s not too hard. With two arguments the problem gets a bit more challenging. With more than two arguments, testing every combination of appropriate values can be daunting.
- Output arguments are harder to understand than input arguments. When we read a function, we are used to the idea of information going in to the function through arguments and out through the return value. We don’t usually expect information to be going out through the arguments. So output arguments often cause us to do a double-take.

### Flag Arguments
- Flag arguments are ugly. Passing a boolean into a function is a truly terrible practice. It immediately complicates the signature of the method, loudly proclaiming that this function does more than one thing. It does one thing if the flag is true and another if the flag is false!

### Argument Objects
- When a function seems to need more than two or three arguments, it is likely that some of those arguments ought to be wrapped into an object of their own.
- When groups of variables are passed together, they are likely part of a concept that deserves a name of its own.

### Argument List
- Sometimes we want to pass a variable number of arguments into a function.
- If the variable arguments are all treated identically, as they are in the example above, then they are equivalent to a single argument.
- So all the same rules apply. Functions that take variable arguments can be monads, dyads, or even triads. But it would be a mistake to give them more arguments than that.
    void monad(Integer... args);     void dyad(String name, Integer... args);     void triad(String name, int count, Integer... args);

### No Side Effects
- Side effects are lies. Your function promises to do one thing, but it also does other hidden things.

### Prefer Exceptions to Returning Error Codes
- Returning error codes from command functions is a subtle violation of command query separation. It promotes commands being used as expressions in the predicates of if statements.
- If you use exceptions instead of returned error codes, then the error processing code can be separated from the happy path code and can be simplified.

### Extract Try/Catch Blocks
- Try/catch blocks are ugly in their own right. They confuse the structure of the code and mix error processing with normal processing. So it is better to extract the bodies of the try and catch blocks out into functions of their own.

### Error Handling Is One Thing
- Functions should do one thing. Error handing is one thing. Thus, a function that handles errors should do nothing else. This implies (as in the example above) that if the keyword try exists in a function, it should be the very first word in the function and that there should be nothing after the catch/finally blocks.

### Write Your Try-Catch-Finally Statement First
- In a way, try blocks are like transactions. Your catch has to leave your program in a consistent state, no matter what happens in the try. For this reason it is good practice to start with a try-catch-finally statement when you are writing code that could throw exceptions. This helps you define what the user of that code should expect, no matter what goes wrong with the code that is executed in the try.

### Don’t repeat yourself (DRY)
- It’s not easy to spot this duplication because the four instances are intermixed with other code and aren’t uniformly duplicated. Still, the duplication is a problem because it bloats the code and will require four-fold modification should the algorithm ever have to change. It is also a four-fold opportunity for an error of omission.

### Structured Programming
- Some software engineers follow Edsger Dijkstra’s rules of structured programming. Dijkstra said that every function, and every block within a function, should have one entry and one exit. Following these rules means that there should only be one return statement in a function, no break or continue statements in a loop.
- But it is only in larger functions that such rules provide significant benefit.

### Provide Context with Exceptions
- Create custom Exceptions
- Each exception that you throw should provide enough context to determine the source and location of an error. In Java, you can get a stack trace from any exception; however, a stack trace can’t tell you the intent of the operation that failed.
- Create informative error messages and pass them along with your exceptions. Mention the operation that failed and the type of failure. If you are logging in your application, pass along enough information to be able to log the error in your catch.

### Define the Normal Flow
- Separation between your business logic and your error handling.

### Don’t return NULL
- When we return null, we are essentially creating work for ourselves and foisting problems upon our callers. All it takes is one missing null check to send an application spinning out of control.

### Don’t pass NULL
- Returning null from methods is bad, but passing null into methods is worse. Unless you are working with an API which expects you to pass null, you should avoid passing null in your code whenever possible.

## Testing

### TDD
- **First Law** You may not write production code until you have written a failing unit test.
- **Second Law** You may not write more of a unit test than is sufficient to fail, and not compiling is failing.
- **Third Law** You may not write more production code than is sufficient to pass the currently failing test.

### Keeping Tests Clean
- The moral of the story is simple: Test code is just as important as production code. It is not a second-class citizen. It requires thought, design, and care. It must be kept as clean as production code.
- What makes a clean test? Three things. Readability, readability, and readability. Readability is perhaps even more important in unit tests than it is in production code. What makes tests readable? The same thing that makes all code readable: clarity, simplicity, and density of expression. In a test you want to say a lot with as few expressions as possible.

### Minimise number of Assert per Test
- I think the single assert rule is a good guideline.
- At least single concept per Test

### Use coverage tools
- Coverage tools reports gaps in your testing strategy. They make it easy to find modules, classes, and functions that are insufficiently tested.

### Don’t Skip Trivial Tests
- They are easy to write and their documentary value is higher than the cost to produce them.

### Test Boundary Conditions
- Take special care to test boundary conditions. We often get the middle of an algorithm right but misjudge the boundaries.

### Exhaustively Test Near Bugs
- Bugs tend to congregate. When you find a bug in a function, it is wise to do an exhaustive test of that function. You’ll probably find that the bug was not alone.

### Tests Should Be Fast
- A slow test is a test that won’t get run. When things get tight, it’s the slow tests that will be dropped from the suite. So do what you must to keep your tests fast.

## F.I.R.S.T.
Clean tests follow five other rules that form the above acronym:

### Fast
- Tests should be fast. They should run quickly. When tests run slow, you won’t want to run them frequently. If you don’t run them frequently, you won’t find problems early enough to fix them easily. You won’t feel as free to clean up the code. Eventually the code will begin to rot.

### Independent
- Tests should not depend on each other. One test should not set up the conditions for the next test. You should be able to run each test independently and run the tests in any order you like. When tests depend on each other, then the first one to fail causes a cascade of downstream failures, making diagnosis difficult and hiding downstream defects.

### Repeatable
- Tests should be repeatable in any environment. You should be able to run the tests in the production environment, in the QA environment, and on your laptop while riding home on the train without a network. If your tests aren’t repeatable in any environment, then you’ll always have an excuse for why they fail. You’ll also find yourself unable to run the tests when the environment isn’t available.

### Self-Validating
- The tests should have a boolean output. Either they pass or fail. You should not have to read through a log file to tell whether the tests pass. You should not have to manually compare two different text files to see whether the tests pass. If the tests aren’t self-validating, then failure can become subjective and running the tests can require a long manual evaluation.

### Timely
- The tests need to be written in a timely fashion. Unit tests should be written just before the production code that makes them pass. If you write tests after the production code, then you may find the production code to be hard to test. You may decide that some production code is too hard to test. You may not design the production code to be testable.

