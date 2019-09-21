# Lesson: Active Record Validations

Active Record can validate our models for us before they even touch the database. This means it's harder to end up with bad data, which can cause problems later even if our code is technically bug-free. We can use `ActiveRecord::Base` class methods like `#validates` to set things up.

## Context: Database and Data Validity

In the context of Rails, validations are special method calls that go at the top of model class definitions and prevent an object from being saved to the database if it's data doesn't meet certain requirements set by the method calls. In general, "validations" are any code that perform the job of protecting the database from invalid code.

## Active Record Validations Are Not Database Validations

Many relational databases such as SQLite have data validation features that check things like length and data type. In Rails, there validations are **not used**, because each database works a little differently, and handling everything in Active Record itself guarantees that we'll always get the same features no matter what database we're using under the hood.

## Validations Protect the Database

Invalid data is the bogeyman of web applications: it hides in your database until the worst possible moment, then jumps out and ruins everything by causing confusing errors. Instead of focusing on handling bad data, you should be focusing on handling edge cases that are truly unpredictable. That's where validations come in.

## Basic Usage

`#validates` is our Swiss Army knife for validations. It takes two arguments: the first is the name of the attribute we want to validate, and the second is a hash of options that will include the details of how to validate it.

### Basic Validation Example

```ruby
# app/models/person.rb

class Person < ActiveRecord::Base
  validates :name, presence: true
end

Person.create(name: "John Doe").valid?
# => true
Person.create(name: nil).valid?
# => false
```

In this example, the options hash is `{presence: true}`, which implements the most basic form of validation, preventing the object from being saved if its `name` attribute is empty.

## Lifecycle Timing

**Database activity triggers validation.** An Active Record model instantiated with `#new` will not be validated, because no attempt to write to the database was made. Validations won't run unless you call a method that actually hits the database, like `#save`. The only way to trigger validation without touching the database is to call the `#valid?` method. For a full list of methods that trigger validation, see [Section 4](https://guides.rubyonrails.org/active_record_callbacks.html#running-callbacks) of the Rails Guide for Active Record Callbacks.

## Validation Failure

How can you tell when a record fails validation? Pay attention to return values!

- By default, Active Record does not raise an exception when validation fails. Database operation methods (such as `#save`) will simply return `false` and decline to update the database.
- Every database method has a sister method with a `!` at the end which will raise an exception (`#create!` instead of `#create` and so on).
- And of course, you can always check manually with `#valid?`.

To find out what went wrong, you cna look at the model's `#errors` object.

- You can check all errors at once by examining `errors.messages`.
- You can check one attribute at a time by passing the name to `errors` as a key.

## Displaying Validation Errors in Views

See [Section 8](https://guides.rubyonrails.org/active_record_validations.html#displaying-validation-errors-in-views) of the Rails Guide for an example of how to use the `ActiveModel::Errors#full_messages` helper, reproduced here for convenience:

```erb
<% if @article.errors.any? %>
  <div id="error_explanation">
    <h2><%= pluralize(@article.errors.count, "error") %> prohibited this article from being saved:</h2>

    <ul>
      <% @article.errors.full_messages.each do |msg| %>
        <li><%= msg %></li>
      <% end %>
    </ul>
  </div>
<% end %>
```

This constructs more complete-looking sentences from the more terse messages available in `errors.messages`.

### Checking Error Messages

You can check all errors at once by examining `errors.messages`,

```ruby
person = Person.new
person.errors.messages
# => empty
person.valid?
# => false
person.errors.messages
# => name: can't be blank
```

Or you can check one attribute at a time by passing the name to `errors` as a key.

```ruby
person.errors[:attribute_name]
```

## Other Built-In Validators

Rails has a host of built-in helpers.

### Length

`length` is one of the most versatile. The `in` argument makes use of a [Range](http://ruby-doc.org/core-2.6.2/Range.html).

### Length Validation Example

```ruby
# app/models/person.rb

class Person < ActiveRecord::Base
  validates :name, length: {minimum: 2}
  validates :bio, length: {maximum: 500}
  validates :password, length: {in: 6..20}
  validates :registration_number, length: {is: 6}
end
```

### Uniqueness

Another common built-in validator is `uniqueness`.

### Uniqueness Validation Example

```ruby
# app/models/account.rb

class Account < ActiveRecord::Base
  validates :email, uniqueness: true
end
```

This will prevent any account from being created with the same email as another already-existing account.

### Custom Messages

This isn't a validator in its own right, but a handy convenience option for specifying your own error messages.

### Custom Message Example

```ruby
# app/models/person.rb

class Person < ActiveRecord::Base
  validates :not_a_robot, acceptance: true, message: "Humans only!"
end
```

## Custom Validators

There are three ways to implement custom validators, with examples in [Section 6](https://guides.rubyonrails.org/active_record_validations.html#performing-custom-validations) of the Rails Guide. Of the three, `#validate` is the simplest, because all you need to do is define an instance method that is invoked by `#validate`. This is probably the best way to start with most custom validations, because everything is in one place, and you cna come back later to reorganize if it starts to get more complex.

- Calling `#validate` (that's "validate" _without_ an "s") with the name of an instance method
  - Use this approach when you're not sure which to use. If you end up needing to use the same validation logic on a different model, you can easily extract the instance method into one of the ActiveModel classes and use `#validates` or `#validates_with` instead.
- Subclassing `ActiveModel::EachValidator` and invoking with an inflected key in the options hash
  - This is best for validating a single attribute on one model, especially one that you're already using built-in validators for.
- Subclassing `ActiveModel::Validator` and invoking with `#validates_with`
  - This approach is best when you want to do a whole bunch of validations on several different models. You can just call `validates_withMyValidator` on each of them.
- To recap:
  - `validate` for quick custom validations that you can extract later.
  - `EachValidator` and `validates` for validating one specific attribute.
  - `Validator` and `validates_with` for doing many validations in one pass.