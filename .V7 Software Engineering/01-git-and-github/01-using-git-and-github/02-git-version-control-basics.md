# Lesson: Git Version Control Basics

## Identify How to Initialize a Git Repository with `git init`

Git operates on a directory level. When we have a new directory that we want to track our files in, we need to _initialize_ the directory as a Git repository. That means Git will then pay attention to what goes on in the directory and give us all the Git superpowers.

To get started, we'll create a new directory. Go to the terminal and type the following:

```bash
~ $ mkdir my-git-project
```

This command creates a new directory. Then:

```bash
~ $ cd my-git-project
```

This command moves into the newly created directory.

Now that we're in the directory where we want Git to watch for changes (adding, removing, and editing files), let's set up this directory by _initializing_ it.

```bash
my-git-project $ git init
Initialized empty Git repository in /Users/meghangutshall/my-git-project/.git/
```

The hidden `.git` directory is where Git keeps important stuff, like the commit history. If you ever `git init` in the wrong directory, you can `rm -rf .git` and return the folder to a plain-old, unprotected directory.

> Make sure you only type `git init` _within_ the directory you want `git` to track.

## Check the Status of a Repository with `git status`

Now that we have Git watching this directory, let's see what it can tell us about the directory. The command we use for this is `git status`.

```bash
my-git-project $ git status
```

Since we have not added any files yet, we'll see:

```bash
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

Let's create a `README.md` that describes the project. Make our new file by typing `touch README.md` from within the `my-git-project` directory. We won't see any output after `touch`, but we will see a new file has been created is we type `ls` (which gives a list of all the files in the directory).

```bash
my-git-project $ touch README.md
my-git-project $ ls
README.md
```

With at least one new project file, we can enable Git to start track ing changes. Type `git status`. Git will show us what our current repository looks like and what changes it sees. Git confirms that it's aware of the file `README.md`, but it's not "tracking" it... yet.

## Keep Track of File Changes with `git add`

We have to tell Git about all the files we want it to keep track of and consider as part of our project. We can do this by _adding_ the files to our `git` repository with `git add <filename or path>`. Now, all the changes in the file at the time we `added` it are "staged". If we were to change `README.md`, we'd need to re-add the file. As it happens here, this staged change is "create the file, nothing instide of it" because `touch` created an empty file.

To save a new _version_ of this new file (or, later, to "capture" changes to a file) we need to _commit_ the set of changes or "diff". We "save" the changes in out repository by making _commits_.

## Create a Commit and Apply a Commit Message with `git commit`

To make our first commit, type: `git commit -m "Initial commit"`. This tells `git` that our commit message, represented by the `-m` flag, is `"Initial commit"`.

We can see that Git has created a new version of our repo, represented by the _SHA_ `e55477d`. SHAs are the identification system that `git` uses to keep track of versions; they're long complex numbers that are unlikely to be duplicated.

## Conclusion

To make a new Git repository out of a directory—which we'll only have to do once per project—use `git init`. Whenever you make a change to a file or create a new file, you can check the status of these changes with `git status`. When you're ready to preserve changes, you can `git add` the files (or directories of files) with the `git add <filename or path>` command.

Once your changes have been added, or "staged", use `git commit -m` to commit them with an explanatory message. You can shorten the `add` + `commit` process, provided that all the files are being tracked by using `git commit -am "A message"`.

## Resources

[Git Basics](https://git-scm.com/book/en/v1/Git-Basics)
