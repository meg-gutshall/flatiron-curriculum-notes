# Lesson: Ruby Methods with Regex

## Notes & Code Examples

### Ruby Regex Methods

#### `scan`

The `scan` method returns an array of all items in your string that match a given regular expression.

```ruby
"The rain in Spain lies mainly in the plain.".scan(/\w+ain/)
=> ["rain", "Spain", "main", "plain"]
```

#### `match`

The `match` method returns the first item in your string that matches a given regular expression as a `MatchData` object.

```ruby
"The rain in Spain lies mainly in the plain.".match(/\w+ain/)
=> <MatchData "rain">

"The rain in Spain lies mainly in the plain.".match(/France/)
=> nil
```

#### `grep`

`grep` is an enumerable method for pattern searching in arrays and hashes. Similar to `scan`, `grep` will return an array of matching items from an array.

```ruby
names = ["Jeri Faria", "Althea Voth", "Audry Donoho", "Scotty Chaves", "Lance Barrio", "Zachary Newhall", "Stefany Janey", "Tressie Kinsel", "Raven Grimsley", "Marketta Gaylor", "Leota Crowe", "Mazie Norman", "Damien Loffredo"]

# Get items from array where first name has five letters:
names.grep(/^\w{5}\s/)
=> ["Audry Donoho", "Lance Barrio", "Raven Grimsley", "Leota Crowe", "Mazie Norman"]
```

### Capture Groups

Using parentheses in our Regex allows us to create groups that we can refer to in our `scan`/`match`/`grep` methods as indexes in an array.

```ruby
numbers = "202-555-0192 202-555-0147 202-555-0131 202-555-0116 202-555-0192 202-555-0197"

number_breakdown = numbers.scan(/(\d+)-(\d+)-(\d+)/)
=> [["202", "555", "0192"], ["202", "555", "0147"], ["202", "555", "0131"], ["202", "555", "0116"], ["202", "555", "0192"], ["202", "555", "0197"]]

number_breakdown[0]
=> ["202", "555", "0192"]

number_breakdown[0][1]
=> "555"
```