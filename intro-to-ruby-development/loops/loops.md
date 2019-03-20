# Loops

- The most basic way to build a loop is using the `loop` keyword. It simply executes a block of code between the `do` and `end` keywords.
  - The code that goes inside the `do` and `end` is considered the loop's body or block; that's the code that will execute on repeat.
  - If you get stuck in an infinite loop, use `Control+C` to break out of the loop in your terminal or just exit the session.
- Infinite loops will break our program. The `loop` keyword alone will create an infinite loop. Generally, we want to loop only a certain number of times. We can use the `break` keyword inside the body of the loop to exit or abort the loop and continue with the rest of our code.
- To build a loop that runs a set number of times, we need a counter that will conditionally break out of the loop when the counter reaches the predetermined number of iterations. Then we need to increment the counter at every iteration (or execution of the loop).
  - Two ways to increment: `counter = counter + 1` or `counter += 1`
- Another construct is `times`. There are two important distinctions to be mindful of when using `times`:
  - It has to be called on an integer
  - It executes the block a certain number of times, which is dependent on the number that it's called on
- We can also insert a counter into a `times` loop.