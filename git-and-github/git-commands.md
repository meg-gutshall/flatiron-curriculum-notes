# Lesson: `git` Commands

## Notes

- `cd my-git-project` moves the terminal to the new directory
- `git add <filename or path>` adds that file to the list to files being tracked in the directory
- `git add .` captures all changes in the directory
- `git branch <branch name>` adds a new branch of code instead of using `master`
- `git checkout <branch name>` lets you move between branches
- `git checkout -b new-branch-name` lets you create a new branch and move to it in one command
- `git clone` clones a repository, taking a URL as its argument
- `git commit` sends changes to the staging area
  - add `-m` to flag a message in your commit (the message should be in quotations)
- `git init` initializes a new directory
- `git merge` adds changes from your branches into the `master` branch
  - You must be in the `master` branch when using this command.
- `git pull` pulls changes from the remote repository to your local repository
- `git push` sends code changes from your local repository to the remote repository
  - takes two arguments: remote repository name and remote branch name
  - use `-u` when pushing for the first time to tell Git to track changes
- `git status` will give us info about the directory
- `ls` lists all of the files in the current directory
- `mkdir my-git-project` makes a new directory
- `touch` creates a new file
