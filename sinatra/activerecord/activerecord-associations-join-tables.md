# Lesson: ActiveRecord Associations: Join Tables

## Notes

- Let's look at an e-commerce site. If you think about the models, there would be a `User` class and an `Item` class, which would contain all the items a user could buy. Since a user can have many items and an item can belong to many users, we're basically dealing with a many-to-many relationship.
- This is where join tables come into play with the `has_many :through` association, which is used for object associations where more than one object can own many objects of the same class. A join table is a table that connects records that are related, but in different tables themselves.
  - In our online store example, this table would contain a `user_id` and `item_id`. Each row in this table would contain a user's ID and an item's ID. We call this join table `user_items` because the name makes it clear that we are linking the `users` and the `items` tables.

**Migrations**
First, we need to create three migrations: one for the users table, one for the items table, and the join table, `user_items`.

**Models**
Next, we need to define the appropriate relationships in our three models.

## Code Examples

### Join Tables Migrations

```ruby
class CreateUsers < ActiveRecord::Migration
  def change
    create_table :users do |t|
      t.string :name
      t.timestamps null: false
    end
  end
end

class CreateItems < ActiveRecord::Migration
  def change
    create_table :items do |t|
      t.string :name
      t.integer :price
      t.timestamps null: false
    end
  end
end

class CreateUserItems < ActiveRecord::Migration
  def change
    create_table :user_items do |t|
      t.integer :user_id
      t.integer :item_id
      t.timestamps null: false
    end
  end
end
```

### Join Tables Models

```ruby
class User < ActiveRecord::Base
  has_many :user_items
  has_many :items, through: :user_items
end

class Items < ActiveRecord::Base
  has_many :user_items
  has_many :users, through: :user_items
end

class UserItems < ActiveRecord::Base
  belongs_to :user
  belongs_to :item
end
```