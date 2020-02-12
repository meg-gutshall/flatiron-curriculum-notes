# Lab: Introduction to Context Lab (JavaScript Advanced Functions)

We're now ready to face one of the (infamously) most-challenging parts of JavaScript: working with execution context. We'll start off with defining five key terms and then dive deeper.

## Definitions

1. Execution Context: When JavaScript functions run, they have an associated JavaScript object that goes along with them which they can access by the keyword `this`.
2. `this`: Inside a function, `this` is the object that represents the function's execution context.
3. `call`: This is a method _on a function_ that calls the function, just like `()`. You provide a new execution context as the first argument, traditionally called `thisArg`, and the arguments you want to send to the function after the `thisArg`. An invocation of `call` looks like: `Calculator.sum.call(multilingualMessages, 1, 2)`.
4. `apply`: This is a method _on a function_ that calls the function, just like `()`. You provide a new execution context as the first argument, traditionally called `thisArg`, and the arguments you want to send to the function **_as an array_** after the `thisArg`. An invocation of `apply()` looks like: `Calculator.sum.apply(multilingualMessages, [1, 2])`.
5. `bind`: This method returns _a copy_  of the function but with the execution context "set" to the argument that's passed to `bind`. It looks like this: `sayHello.bind(greenFrog)("Hello"); //=> "Mr. GreenFrog says 'Hello' to you all."`

## What Is a "Record"?

Back in the old days (the 1960s and earlier) computers didn't have memory. Records were stored on small paper cards called punch cards. They looked like this:

![A Used Punch Card for Programming](/public/images/front-end-web-programming-in-javascript/used-punch-card.jpg)

These cards, or "records," often had information on them in "fields." In the `first_name` field, you'd find a first, etc... So when a business needed to figure out how much to pay each person for a week's work, something like the following would happen:

- Load up all the employees' cards into a tray
- Feed the tray of cards into the computer
- The computer would read each card and calculate the hours worked for the week per card
- The computer would emit a new card with all the old data, but this card would have a new field added called something like `wagesPaidInWeek33OfYear: 550`
- The computer would also print out a table of the employee name and the amount owed

Then, the emitted pay ledger could be taken to the payroll department and the appropriate person could write out paychecks to the employees.

Ultimately, the punch card was an intermediate step between paper records and digital records. But it was during the punch card era the computing really got big, so a _lot_ of our ways of thinking about programming started by thinking about "records."

## What Is "Record-oriented Programming"?

[Record-oriented programming](https://en.wikipedia.org/wiki/Record_(computer_science)) is a style of programming based on finding records and processing them so that they're updated (like `map`) or so that their information is aggregated (like `reduce`). "Record-oriented" isn't a buzzword that we hear used very much. Ask any programmer who's worked in large-scale billing (phone companies, insurers, etc.) or at a university (50,000 grade point averages), and you can bet they'll understand what the term means.

The amazing thing is that in the 21st century, this style of programming is back in vogue! We're not using punch cards, but the ability to spin up hundreds of little computers in a cloud, hand each of them a bundle of records, and get processed answers back is _cutting-edge_!

In fact, a program to do `map` and `reduce` operations at scale on a cloud was standardized in the 2000s. Guess what it was called? [`mapReduce`](https://en.wikipedia.org/wiki/MapReduce) It was pioneered and advanced as part of the secret sauce that made a small company from Mountain View, CA called Google become the giant it is today. Today, you can use it under the name of [Apache Hadoop](https://en.wikipedia.org/wiki/Apache_Hadoop).

The Go programming language is built around building and processing records at scale. Record-oriented programming is not likely to go away anytime soon.

## Conclusion

We can use the innovation of execution context to DRY up repetition in our code.

### Resources

- [Record/Record-oriented Programming (Wikipedia)](https://en.wikipedia.org/wiki/Record_(computer_science))
- [JavaScript Error Class (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)
- [JavaScript Date Class (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)
