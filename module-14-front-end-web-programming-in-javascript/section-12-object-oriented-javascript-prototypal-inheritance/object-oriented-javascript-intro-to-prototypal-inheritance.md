# Lesson: Intro to Prototypal Inheritance (Object-Oriented JavaScript)

When you learned object-oriented JavaScript, you were exposed to the syntax that came into existence at around 2014. This syntax uses the `class` keyword and the `constructor()` method to initialize new instances of a class. We'll call this the "ES2015 standard." ES2015's syntax is similar to Ruby, Python, and Java and, to many developers learning JavaScript as a second language, feels like "the way OO should be done."

## Syntactic Sugar

However, from JavaScript's perspective, ES2015's syntax is "syntactic sugar." This is a term that developers use to communicate "we made the thing easier to type a read, but underneath it's still doing something a lot more complicated." The object-oriented model that ES2015 simplifies is the "prototypal object-oriented" modal that JavaScript _actually_ works in.

## Recognize that the Inheritance Model of JavaScript is Prototypal

>**IMPORTANT**: This is a common interview question used to weed out front-end developers. When asked what kind of inheritance model JavaScript has, boldly and proudly say, "Prototypal!"

The difference between prototypal and class-based object orientation goes all the way back to ancient philosophy; Plato and Aristotle in fact!

Plato's Theory of Forms suggests that our minds can picture a single item from a collection based on the properties the item shares with others that belong to its collection. For example, our minds can picture a tree because we know that pretty much all trees are tall, have bark and leaves, grow roots, etc. Philosophy students call this "the form of a Tree" or "Tree-ness."

This is akin to the class-based object orientation used in Ruby, Java, Python, and ES2015 standard JavaScript. Forms are classes and instances are the new embodiments of those classes with some unique, specific, real data bonded to them (via a constructor).

>**ASIDE**: Programming, for many, is an exercise in applied philosophy.

Aristotle, on the other hand, argued everything that _is_ is like something else with more specification added. Everything new is based off of a pre-existing pattern, or _prototype_.

Given this view of the world, it's no surprise that Aristotle was a huge fan of making trees of these relationships (or, "taxonomies," another computer science idea that started in philosophy). Languages that allow you to "extend what's already there" are C, Lisp, Self, and JavaScript (natively). These are also referred to as Prototypal object systems.

Ultimately, both class-based (or, "form-based") and prototype-based models are ways of describing how to create instances from a common ancestor. Neither is "better" than the other, they're just different ways of seeing objects in the world.

## Conclusion

The ES2015 standard is fast becoming _the_ standard, but it's common to see prototypal patterns in legacy code and in job interview questions.
