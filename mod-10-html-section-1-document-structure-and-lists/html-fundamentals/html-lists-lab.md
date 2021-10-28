# HTML Lists Lab

## What Are Unordered and Ordered HTML Lists?

Let's say, for instance, we were building a personal website and wanted to list out our favorite foods. We _could_ write this like so:

```markup
<body>
  <p>Ham and cheese</p>
  <p>Grilled cheese</p>
  <p>Nacho cheese french fries</p>
  <p>Cheese soup</p>
  <p>Cheese and crackers</p>
  <p>Sushi</p>
</body>
```

The above would create a new line on the page for each food, but doesn't really indicate that there things are related. Using the built-in `ul`, `ol`, and `li` HTML tags however, we can group related list content together. We call such a group a "list."

In HTML, we create lists using the `<ul>` tag, which stands for _unordered list_, along with the `<li>` tag for each _list item_.

To make a list, we write out the opening and closing `<ul>` tags, and inside them, we'll add `<li>` tags, each listing a single ingredient. Going back to our favorite foods example, if we wanted to convert it to a list, it would look like this:

```markup
<ul>
  <li>Ham and cheese</li>
  <li>Grilled cheese</li>
  <li>Nacho cheese french fries</li>
  <li>Cheese soup</li>
  <li>Cheese and crackers</li>
  <li>Sushi</li>
</ul>
```

Now, instead of just having each item show up on a new line, the content will also be slightly indented and a bullet will appear next to each of them.

Lists are very flexible and we can even nest lists _inside_ of lists. Say we wanted to breakdown our favorite foods by category. We may have multiple categories and one or more items in _each_:

```markup
<ul>
  <li>Sandwiches
    <ul>
      <li>Ham and Cheese</li>
      <li>Grilled Cheese</li>
    </ul>
  </li>
  <li>Snacks
    <ul>
      <li>Nacho Cheese French Fries</li>
      <li>Cheese and crackers</li>
    </ul>
  </li>
  <li>Soups
    <ul>
      <li>Cheese soup</li>
    </ul>
  </li>
  <li>Sushi
    <ul>
      <li>Spicy Salmon Rolls</li>
      <li>California Rolls</li>
    </ul>
  </li>
</ul>
```

In this example, the nested lists will now be _further_ indented and instead of a solid bullet, they will appear with hollow bullets, indicating a sublist. Adding a nested list one level deeper will make _square_ bullets appear, allowing us to easily display related and nested content in a readable format.

### What About Ordered Lists?

Unordered lists are great for organizing related content where it doesn't matter what goes first, like in our grilled cheese ingredients in situations where we _want_ items to be displayed in a specific, numbered order, we will want to use the _ordered list_ tag, which is written as `<ol>` instead of `<ul>`. Both use `<li>` tags inside, but this time, `<ol>` will display a numbered list instead of bullets. If say, we wanted to write a _ranked_ list of favorite foods, it might look like:

```markup
<h3>Top 5 Favorite Foods</h3>
<ol>
  <li>Grilled cheese</li>
  <li>Sushi</li>
  <li>Cheese and crackers</li>
  <li>Cheese soup</li>
  <li>Nacho cheese french fries</li>
</ol>
```

Nested ordered lists work the same as unordered, but instead of hollow and square bullets, each nested list will display numbers.

{% hint style="warning" %}
**Note:** In a nested list, you _must_ provide the `ol` or `ul` wrapper. Otherwise, an `li` inside another `li` will just be displayed as two items at the same level. This is because technically, you do not need to write a closing `li` tag.
{% endhint %}
