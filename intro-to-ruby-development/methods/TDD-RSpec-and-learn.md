# Lesson: TDD, RSpec, and Learn

## Notes

- Tests verify that the code you write behaves and produces the desired result.
- TDD (or test-driven development) is considered the most reliable methodology for writing quality code.
  - The basic idea behind TDD is that you should think about what you want your program to do and how you want your code to behave before you start coding.
- Writing a test:
  - First, write the test for a specific function of your code
    - Identify the desired behavior of the program you’re going to write
- Then, write the code to make the test pass
  - Use the [RSpec Testing Framework](http://rspec.info/), a ruby library designed to allow programmers to describe the behavior and outcomes of their programs in a very natural language
- About the RSpec Testing Framework:
  - Tests are located within the `spec` directory, whereas are programs are generally in the root of the lab directory or in files in directories like `lib` or `app`.
  - A test is always going to be about setting up a state with a known result and comparing that known result or expectation to the behavior of your program, thus ensuring that your program behaves as you expected.
- Types of errors:
  - `NoMethodError`: when a method is undefined
  - `ArgumentError`: when a method isn’t set up to except an argument or there’s a mismatched expectation for the result

## Code Examples: Understanding the Tests in the `spec` Directory

### Understanding and Writing Tests

```ruby
# In this lab, our test is in the file:
spec/current_age_for_birth_year_spec.rb

# and our actual program and solution are in the file:
current_age_for_birth_year.rb

# Our example test:
require_relative '../current_age_for_birth_year.rb'

describe "current_age_for_birth_year method" do
  it "returns the age of a person based on their year of birth" do
    age_of_person = current_age_for_birth_year(1990)

    expect(age_of_person).to eq(28)
  end
end

# The first line of the test loads the program and connects it to our test.
require_relative '../current_age_for_birth_year.rb'

# The second line uses the describe method in RSpec
describe "current_age_for_birth_year method" do
# The RSpec describe method and Ruby do keyword are required but the code in between is
# arbitrary and meant for the programmer to describe what is being tested.

# The third line uses the RSpec it method
it "returns the age of a person based on their year of birth" do
# Again, the RSpec it method and Ruby do keyword are required. Everything else is solely
# for the programmer's purposes.

# The next three lines (between it and end) are the most important part of the test.

# Call the method that's being tested, pass it a known argument, and assign a return
# variable to the method.
age_of_person = current_age_for_birth_year(1990)

# The next line asks what response we are expecting
expect(age_of_person).to eq(28)

# Then the methods are closed with the Ruby end keyword
```

### Understanding Test Output

```ruby
# Run the test! If there's a failure, a summary will display of what we are testing and
# why it failed. The feedback corresponds directly to the strings provided to methods
# describe and it and are there to provide context.

# Example:
  1) current_age_for_birth_year method returns the age of a person based on the year of birth
  Failure/Error: age_of_person = current_age_for_birth_year(1984)
  NoMethodError:
    undefined method `current_age_for_birth_year' for #<RSpec::ExampleGroups::CurrentAgeForBirthYearMethod:0x007fbb8b0607b8>
  # ./spec/current_age_for_birth_year_spec.rb:5:in `block (2 levels) in <top (required)>'

# The first line describes why our test failed
# The second line describes what part of the code is broken
```