# Lab: `reduce` Lab (Iterators Drill)

In the world of programming, we often work with lists. Sometimes we want to transform elements in that list to another value, but other times we want to _aggregate_ a result. In other words, we want to _reduce_ a list to a single value.

## How the `reduce` Method Works

To illustrate how `reduce()` works, we'll make up some store data. We're interested in getting a total price of all products in our basket. The store data looks like this:

```js
const products = [
  { name: 'Shampoo', price: 4.99 },
  { name: 'Donuts', price: 7.99 },
  { name: 'Cookies', price: 6.49 },
  { name: 'Bath Gel', price: 13.99 }
];
```

We're going to reduce the array of products to a _single value_—in this case, the total price of all products in the basket. Let's create a function that has an initial value, then iterates through the given products and adds their price to the total price. When the loop has finished, we return our `totalPrice` result:

```js
function getTotalAMountForProducts(products) {
  let totalPrice = 0;

  products.forEach(product => {
    totalPrice += product.price;
  });

  return totalPrice;
};

console.log(getTotalAMountForProducts(products));
//=> 33.46
```

This is a very basic way to manually add together the prices of the products we want to buy.

To abstract this further, let's count the number of coupons we have lying around the house:

```js
const couponLocations = [
  { room: 'Living room', amount: 5 },
  { room: 'Kitchen', amount: 2 },
  { room: 'Bathroom', amount: 1 },
  { room: 'Master bedroom', amount: 7 }
];

function couponCounter(totalAmount, location) {
  return totalAmount + location.amount;
};

console.log(reduce(couponLocations, couponCounter, 0));
//=> 15
```

What if we already have three coupons in hand? We can easily account for that by adjusting the initial value:

```js
console.log(reduce(couponLocations, couponCounter, 3));
//=> 18
```

## Demonstrate `reduce()`

With JavaScript's `reduce()` method, we don't need to write out all that code. The `reduce()` method is when we want to get something useful out of each element in the collection and gather that information into a final summary object or value. Let's take the native implementation with our previous example for a spin:

```js
console.log(couponLocations.reduce(couponCounter, 0));
//=> 15
```

Another simple numerical example:

```js
let doubleAndSummed = [1, 2, 3].reduce( (total, element) => element * 2 + total, 0 );
console.log(doubleAndSummed);
//=> 12
```

Here, for each element, JavaScript passes it and the running total (initialized to `0`, in the second argument to `reduce()`) into the function. The function multiplies the element by `2` and adds that to the current total.

That sum (`2 * element + total`) is the return value of the function and becomes the new `total` for the next iteration. When there's nothing left to iterate, the total is returned.

The initialization value can be left out, but it might lead to a real suprise. If _no_ initial value is supplied, the first element is used _without having been used in the function_:

```js
let doubleAndSummed = [1, 2, 3].reduce( (total, element) => element * 2 + total );
console.log(doubleAndSummed);
//=> 11
```

The initialization value can be changed:

```js
let doubleAndSummedFromTen = [1, 2, 3].reduce( (total, element) => element * 2 + total, 10 );
console.log(doubleAndSummed);
//=> 22
```

For more powerful uses, we could use:

```js
let hogwarts_houses = {
  "Slytherin": [],
  "Gryffindor": [],
  "Hufflepuff": [],
  "Ravenclaw": []
};

incoming_students.reduce( (houses, student) => houses[sorting_hat.assign(student)].push(student), hogwarts_houses);
```

Here we iterate over a collection of students and assign each one to a pre-existing accumulator object. We ask the object to look up an array keyed by the name of the houses. We then `push()` the student into that array. Later in the code:

```js
hogwarts_houses["Gryffindor"];
//=> [hermioneGranger, ronWeasley, harryPotter]
```

## Conclusion

With `reduce()`, like many other enumerators in the JavaScript library, we are able to quickly get a minimized list or a total sum from a set of values, including values that we might have filtered out of a list. With this, we can greatly cut down the amount of time spent recreating common functionality, or building out helper methods for commonly used functionality from scratch.

### Resources

- [Array.prototype.reduce() (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)
