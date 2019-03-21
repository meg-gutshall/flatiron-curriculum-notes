# Lesson: RegEx Basics

## Notes

- RegEx stands for regular expressions.
- A good tool for RegEx is [Rubular: a Ruby regular expression editor and tester](http://rubular.com/)
- In Ruby, regular expressions are generally written between forward slashes: `/your regex/`. This is the 'literal' alternative to creating a regular expression object using the following syntax: `Regexp.new('your regex')`.
- Simple text matching
  - Writing a series of letters or numbers in your regular expression will result in a search for exact matches of this pattern anywhere in the string.
- Metacharacters
  - Metacharacters allow you to use a pre-defined shorthand to match specific characters.
- Only specific characters
  - If we want to look for only one single character, enclose the characters in brackets (`[]`).
- Ranges
  - Shorten a search for a single character by using a hyphen (`-`) to express a range.
- Repetitions
  - Add curly braces (`{}`) with a number enclosed to the end of a set of brackets to indicate that the pattern or character directly preceding the curly braces must repeat that number of times.

**It is often best practice to write as specific regular expressions as possible to ensure that we don't get false positives when matching against real world text.**