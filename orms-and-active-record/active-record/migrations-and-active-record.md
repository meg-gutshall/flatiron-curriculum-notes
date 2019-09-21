# Lesson: Migrations and Active Record

## Notes

### Active Record

- Active Record allows you to create a database that interacts with your class with only a few lines of code. These lines go to creating a model, which resides in the `app/models` folder, and a migration, which resides in the `db/migrate` folder.
- The model inherits from `ActiveRecord::Base` while the migration inherits from `ActiveRecord::Migration`.
- To use Active Record, you have to stick to some specific naming conventions: while the migrations are plural, the models are singular.

#### Migrations

- Class names in the migration files must match their file names.
  - Example: A class in the migration file called `20141013204115_create_candies.rb` must be named `CreateCandies`.
- For now, the numbers in the front of the file name are ignored. Later on these timestamps (in `YYYYMMDDHHMMSS` format) will become important as Rails uses them to determine which migration should be run and in what order.
  - You can create two new columns, `created_at` and `updated_at`, by using `t.timestamps`.
- As of Active Record 5.x, we can no longer inherit directly from `ActiveRecord::Migration` and must instead specify which version of Active Record/Rails the migration was written for by including it in brackets.

#### Models

- Like migrations, models also inherit, but they inherit from `ActiveRecord::Base`.