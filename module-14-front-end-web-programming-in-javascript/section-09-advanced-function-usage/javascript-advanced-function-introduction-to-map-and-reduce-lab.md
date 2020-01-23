# Lab: Introduction to Map and Reduce Lab (JavaScript Advanced Functions)

## What Is `map`?

As mentioned in the "character of collection processing," we need to visit each member of a collection. This is common to all collection-processing methods. In the case of `map`, we're going to produce a _new_ array after "transforming" or applying "work" to each element.

>**Naming History**
>"Map" comes from mathematics where it means:
>
>1. Taking an independent variable
>2. Plugging it into an equation
>3. Getting a result back
>
>Mathematicians would say you're **mapping** a value in the _domain_ to a value in the _range_.
>
>If this sounds vaguely familiar, you might have learned it in algebra when learning to graph on the Cartesian coordinate system.
>
>1. Take a value on the _x_ axis
>2. Plug it into a function like `y = mx + b`
>3. Get a _y_ value
>
>Hopefully you're having an "Aha!" moment from that and might be considering sending your algebra teachers a thank-you note.

## What Is `reduce`?

As mentioned in the "character of collection processing," we need to visit each member of a collection. This is common to all collection-processing methods. In the case of `reduce`, we start with an initial value that we'll call the "memo" or "aggregator." Then we do some "work" involving the element and the `memo` and that work updates the `memo`.

This is complex language and describes something we do all the time: make a running total. This updating an aggregator value and returning it at the end is the essence of `reduce`.

The `reduce` function should be given a starting point as an argument.

>**Naming History**
>This idea of "reduce" comes from lots of places, but we like to think about it coming from the realm of cooking when we make a "reduction" by applying "work" (aka heat) until what's left over is the thing we want.
