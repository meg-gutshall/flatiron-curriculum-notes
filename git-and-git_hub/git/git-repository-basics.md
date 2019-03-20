# Git Repository Basics

- Git operates on a per-directory setup.
- To make a new directory, open the terminal and type `mkdir my-git-project`. Then to move to the new directory, type `cd my-git-project`.
- To initialize `git`, type `git init` into the terminal.
  - This step will create a new repository within the hidden `.git` folder located in `my-git-project`. The `.git` folder is what `git` uses to keep track of our log of changes.
- We have to tell `git` which files we want it to keep track of and consider part of our project.
  - We can do this by using `git add <filename or path>`.
- **To capture changes in a directory, type `git add .`, where `.` refers to the entire current directory.**
- To make the first commit, type `git commit -m "Initial commit"`.
  - `-m` signals that the following is part of the commit message.
- **A faster way to capture all outstanding changes for files that are already being tracked in a commit is to use `git commit -am "Our commit message"`, where the `a` refers to adding 'all changes' and `m` assigns a commit message of `"Our commit message"`.**