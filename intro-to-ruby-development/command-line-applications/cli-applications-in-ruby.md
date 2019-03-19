# CLI Applications in Ruby

## CLI File Structure

- `bin/`: Within the `bin/` directory we generally put code that relates to running our actual program.
- `config`: We generally put all the code required to initialize the environment within `config/`. We might see that in a `config/environment.rb` file or even an entire `config/environments/`` directory. The config file or directory is responsible for things like file requirements (i.e. making sure your different files have access to one another), establishing connections to your database (if you have one) and ensuring that your test suite has access to the files that contain the code it is testing.
- `lib/` (`app/`): The `lib/` or Library directory in most Ruby programs and the `app/` directory in Rails projects or complex Ruby programs, is where the majority of our code lives. Within this directory are all the files that define what our program can do. All of the methods and classes our program needs are defined within the files in this directory.
- `spec/` (`test/`): All of our tests go into the `test/` or `spec/` directory.

## Running CLI Applications

- First, your program needs a `bin` directory. "Bin" is short for "binary" and is just another way to refer to executable files. Accordingly, your executable files belong in this directory.
- Executable files are any files that contain instructions in a form that a computer's operating system or application can understand and follow. Any executable files we place in our bin directory need to begin with the following line: `#!/usr/bin/env ruby` (called the “shebang line”)
- By adding `require_relative '../lib/program'` on the following line, we are telling Ruby to load a file from a relative path to the current file.
- You never need to give the `.rb` extension to a path for `require_relative`. Ruby assumes you mean a `.rb` file.
- Using the above setup, you can run your program by typing `ruby bin/< your file name >` into the command line.