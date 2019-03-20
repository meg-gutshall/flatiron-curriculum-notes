# Lesson: Display Tic Tac Toe Board Example

## Notes

Because our program is going to have to display the board repeatedly, we should encapsulate the procedure of printing a board within a method so that we can simply call it whenever we need to print the board.

We're going to start with a simplified version of the `display_board` method. Instead of actually displaying the state of a Tic Tac Toe board, we're going to only print out an empty, hard-coded, board. Sure, this method wouldn't work in a real game, but if we can't print a predefined, hard-coded, simplest board, we're probably not going to be able to print a real board.
>Building a simplified first version of a method is a common practice in programming (these methods are sometimes referred to as 'stubs'). By not trying to solve the entire problem at once, we can first focus on correctly structuring our code, laying out some basics for us to build upon. It allows us to get something working as quickly as possible and then improve the code. This process is called iterating on your code and it's just like editing an essay. It's the natural process of small incremental improvements.