# Lesson: Securing Passwords in Sinatra

## Notes

- Since many users keep the same login credentials across multiple platforms, we never want to store our users' passwords in plain text in our database. Instead, we'll run the passwords through a hashtag algorithm.
  - A hashtag algorithm manipulates data in such a way that it cannot be unmanipulated.
  - In addition to hashing the password, we'll also add a "salt", which is a random string of characters that gets added into a hash. That way, if two of our users have the same password, they will end up with different hashes in our database.
- We'll use an open-source gem, `bcrypt`, to implement this strategy.

### Password Encryption with BCrypt

- BCrypt will store a salted, hashed version of our users' passwords in our database in a column called `password_digest`.
- Essentially, once a password is salted and hashed, there is no way for anyone to decode it. This method requires that hackers use a "brute force" approach to gain access to someone's account-still possible, but more difficult.

**ActiveRecord's `has_secure_password`**

- Let's update our `User` model so that it includes `has_secure_password`. This ActiveRecord macro gives us access to a few new methods.
  - In this case, the macro `has_secure_password` works in conjunction with the `bcrypt` gem and allows us to store the users' passwords securely in the database, instead of using just plain text.
- Even though our database has a column called `password_digest`, we still access the attribute of `password`.

### Login Process with BCrypt

- In `post '/login'`, we need to authenticate the user based on the information they submitted in the login form. We need to check two conditions: does the submitted username exist and if so, does the submitted password match up with the value in `password_digest`.
- First, we find the user with the following code: `user = User.find_by(username: params[:username])`. Then, we create an if/else statement based on if we found a username in our database that matches what was submitted in the login form.
  - If not, the user is redirect to the `/failure` view page. If so, we now need to check that the submitted password matches the value stored in `password_digest` for that particular user.
- We validate password match by using a method called `authenticate` on our `User` model.
  - The `authenticate` method is made available by our `has_secure_password` macro.
- **IMPORTANT: At no point do we see an unencrypted version of the user's password.**