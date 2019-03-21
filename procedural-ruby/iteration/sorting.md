# Lesson: Sorting

## Notes

- To compare strings and sort them alphabetically, use the `>` ("greater than") and `<` ("less than") comparison operators.
  - Letters later in the alphabet are considered greater than letters earlier in the alphabet.
- The `.sort` method yields to a block with two elements. That block is the comparator, so it should compare the two elements and return 0 if they are the same, -1 if the first is less than the second, and 1 if the first is greater than the second.
- The `.sort` method passes elements two at a time into the block, and compares those two elements inside the block with out `if` and `elsif` logic.
  - [Sort Method Example](:note:37e70445-a60d-48f3-8c18-a95ff8de5c3a)
  - If `a` and `b` are equal, the block will return `0`, and `.sort` will leave them in their current places.
  - If `a` is less than `b` and belongs before it, the block will return `-1` and `.sort` will once again leave them in their current places (because `a` is already before `b`).
  - If `a` is greater then `b` and belongs after it, the block will return `1` and `.sort` will switch the locations of `a` and `b`.
- The `.sort` method uses the "spaceship operator" (`<=>`), or combined comparison operator.
  - Instead of utilizing `if` and `elsif`, we can simply call `.sort` with the following code: [Sort Method Examples](:note:37e70445-a60d-48f3-8c18-a95ff8de5c3a)
- Simply calling `.sort` on an array will return the sorted array.
  - By default, the `.sort` method is case sensitive. It will prioritize strings that are capitalized.

## Code Examples

```ruby
array = [7, 3, 1, 2, 6, 5]

array.sort do |a, b|
  if a == b
    0
  elsif a < b
    -1
  elsif a > b
    1
  end
end
```

## Sort Method Using the Spaceship Operator

```ruby
array = [7, 3, 1, 2, 6, 5]

array.sort do |a, b|
  a <=> b
end
```