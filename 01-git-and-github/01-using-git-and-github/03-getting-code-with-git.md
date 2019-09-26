# Lesson: Getting Code with Git

Git not only lets you track files in a local repo on your machine, you can "share" your repo on the Internet so that others can use your code.

## Copy a Repository to Your Local Machine with `git clone`

We use `git clone` to copy someone else's repo from the Internet to our _local_ machine. We are not getting _their_ repo from _their_ local machine. Instead, they have already "mirrored" their _local_ repository into the Internet. In Git-speak we'd say they would have created a _remote repository_: a copy of their local repository, but on the Internet. We'll be cloning that _remote repository_.

Here's the steps to clone a remote repository:

1. Navigate to the repository in GitHub.
2. Click the green "Clone or download" button on the right.
3. Make sure you select `Use SSH` as your URL type.
4. Click the "Copy to clipboard" button. This will copy the URL for us to use when we clone.
5. In the terminal, run the `git clone` command. It takes the URL we just copied as an argument, like so:

```bash
$ git clone your-copied-github-url
```

This will create a _local_ copy of the GitHub repository on our own machine.

## List Remotes with `git remote`

If you use the `ls` command, you'll see Git created a directory for your copied repo. Use `cd` to enter into that directory.

Type `git remote` to see the names of each remote repository (or, "remote") available. Since you cloned your repository, you should see a remote named called `origin`. The remote name `origin` is the default name Git gives to the remote you cloned from:

```bash
$ git remote
origin
```

Let's prove that the `origin` name has some relationship to the address GitHub gave us.

```bash
$ git remote show origin
* remote origin
  Fetch URL: [copied-github-url]
```

The "remote address" assigned to the "remote name" `origin` is the same thing you copied from the GitHub web interface. This confirms that the _remote repository_ you _cloned_ automatically set up a _remote name_ called `origin`.

## Duplicate Other Organizations' Repositories into Your Own via GitHub with the "Fork" Button

Forking a GitHub repository is just a way to create a personal, online duplicate of it. When you fork a repository, GitHub creates a duplicate of that repository under your control.

If my GitHub username were `octocat` and I "forked" `facebook/react`, GitHub would copy the remote repository `facebook/react` and create it under my name as `octocat/react`. It's making a copy of one _remote repository_ to a new _remote repository_.

The "Fork" button is located in the upper right corner of every GitHub repository page.

**Be sure not to confuse the terms "fork" and "clone".** To get a local copy: **clone**; to make an online copy of a repository to your personal organization so that you have the ability to update its `master` branch, **fork**.
