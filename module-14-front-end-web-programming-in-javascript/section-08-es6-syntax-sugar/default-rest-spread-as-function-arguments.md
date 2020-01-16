# Lesson: Default/Rest/Spread as Function Arguments

Unlike most modern programming languages like Ruby or Python, JavaScript didn't have a way to pass a default parameter into a function. However, with the introduction of ES2016, that is no longer the case. It also introduced two other helpful parameters, the `rest` parameter and the `spread` operator.

## JavaScript's Default Function Argument as a Parameter in a Function

Let's say you work for an e-commerce site and you're prepping for your post-holiday sales. You're working on some code for your website and you need to set a discount of 25% across the board for everything that you sell on the website.

We have a function that takes in an `itemPrice` as a price in dollars and a `discount` as a percentage, and returns the total amount due:

```js
function discountedPrice(itemPrice) {
  return itemPrice - (itemPrice * 0.25);
};
```

But it seems unwise to hard-code the discount of `0.25`. Management's whims on  discount rates change almost daily, as the corporate sales offices' machine learning algorithms recommend new discount rates. Because of this, we want to encode the discount rate as a _parameter_ of the function:

```js
function discountedPrice(itemPrice, discount) {
  return itemPrice - (itemPrice * discount);
};
```

So calls to `discountedPrice` will look like:

```js
function discountedPrice(itemPrice, discount) {
  return itemPrice - (itemPrice * discount);
};

discountedPrice(100, 0.25); //=> 75.00
```

But it _also_ seems a bit of a burden to **have** to pass the discount amount on every call. We'd like `discount` to _default_ to `0.25`. It'll be 25% off _unless_ we choose to pass a new discount percentage into `discountedPrice`.

When writing functions that have _parameters_ that take default values, it's best practice to put them at the **end** of the parameter list:

```js
function discountedPrice(itemPrice, discount = 0.25) {
  return itemPrice - (itemPrice * discount);
};

discountedPrice(100); //=> 75.00
discountedPrice(100, 0.5) //=> 50.00
```

What would happen if we added `tax` to `discountedPrice` so that we could add a tax percentage to be added to the sales price? We'll honor best practices and put `tax` before `discount`.

```js
function discountedAndTaxedPrice(itemPrice, tax, discount = 0.25) {
  let subtotal = itemPrice - (itemPrice * discount);
  return subtotal * (1 + tax);
};

discountedAndTaxedPrice(100, 0.15); //=> 86.25
```

## Use JavaScript's `rest` Parameter as a Parameter in a Function

You might have heard a little bit about JavaScript's magical "three dots." These three dots allow you to do two very different things—the `rest` parameter and the `spread` operator. The `rest` parameter allows you to collect the rest of your remaining parameters that you are passing into your function into an array, while the `spread` operator allows you to pass elements of an array into a function as an argument.

Sometimes we might not know exactly how many arguments we want to pass into a function, but we know that we only want to do something with the first two arguments. In JavaScript, it's possible to pass any number of arguments into a function. But what happens if we want to capture the rest of the arguments that are left over? The `rest` parameter allows us to take the rest of the arguments that we pass into the function and gather them into an array. Here's how it works:

```js
function muppetLab(a, b, ...muppets) {
  console.log(a, ' ', b); //=> Dr. Bunson Beaker

  console.log(muppets); //=> ["Miss Piggy", "Kermit", "Animal"]
  console.log(muppets[0]); //=> Miss Piggy
  console.log(muppets.length); //=> 3
};

muppet_lab("Dr. Bunson", "Beaker", "Miss Piggy", "Kermit", "Animal");
```

Since the `rest` parameter gathers the rest of the parameters given to a function, it should always come at the end of a list of parameters.

## Use JavaScript's `spread` Operator as a Parameter in a Function

With the `rest` operator, JavaScript allowed us to put the remaining arguments in an array. The `spread` operator allows us to pass elements of an array into a function as an argument:

```js
function add(a, b, c) {
  return a + b + c;
};

const arr = [1, 2, 3];

add(...arr); //=> 6
```

## Conclusion

Since the syntax here is similar, how do we know when JavaScript is using the `spread` operator and when it's using the `rest` parameter? It's all about context. If the three dots occur when you are calling the function, then it's the `spread` operator. If they happen when you're defining the function, it's the `rest` parameter. Don't forget to use default parameters when you have an argument that you are going to be defining on a regular basis to increase your code efficiency!

### Resources

- [Default Parameters (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)
- [Rest Parameters (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)
- [Spread Operators(MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
