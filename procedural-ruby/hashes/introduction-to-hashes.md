# Lesson: Introduction to Hashes

## Notes

- Hashes store data in an associated manner, which allows us to store complex collections of information.
- Hashes are structured with keys and values. Each key/value pair makes up one unit in the hash. The entire collection of key/value pairs, which are comma separated, is enclosed in curly braces `{}`.
  - Example: `hash = {"key" => "value", "another_key" => "another_value"}`
- Keys in hashes can be any type of data: strings, integers, or symbols. They are set equal to their associated values using the `=>` symbol, known for this use as the "hash-rocket".
- Think of the data stored in a hash as being associative. I other words, keys point to data that is related to that key.
- Unlike arrays, which store data in numbers indexes and access that data via the index numbers, hashes store data in keys and access that data by naming the key whose value we want to retrieve. If you try to add a second key that duplicates an existing key, you will overwrite the value of the existing key, instead of adding a new key/value pair.
- We can make a new hash via the literal constructor, just like arrays: `my_hash = {}` and it can include data.
- Retrieving data from a hash is similar to retrieving data from an array, but instead of giving an array the index number in brackets `[i]`, we give a hash the name of the key `[key]`.
  - Using `[]` is referred to as the "bracket method".
- We use the "bracket-equals" method to add data to a hash.
  - The general syntax for adding a new value to a hash is: `hash["new_key"] = "New Value"`
  - `"new_key"` is the literal new key we added to the hash and we assigned the `"new_key"` a value of `"New Value"`.
- A Histogram is a hash that has counts of occurrences, useful for generating charts and more.
