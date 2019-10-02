# Pushing Code with Git

You've seen how valuable _remotes_ are for _getting_ software. Now we can take a look at the other side of the transaction: how we mirror our _local_ repository to a _remote_ repository using `git push` and `git remote`. Once your code is on a _remote_, it's backed up—which is always a good thing. Also, once you push to a remote, you can choose whether to let others `fork` or `clone` and benefit from it.

## Create a Remote Repository on GitHub

There are a few steps to follow to create a _remote_ repository on GitHub:

1. Go to: [https://github.com/new](https://github.com/new), while logged into GitHub.
2. Enter a name for your repository in the "Repository name" field. The default options are fine as-is—don't initialize the repository with a `README` or add a `.gitignore` or license. Click the green "Create repository" button.
3. After you create the _remote_ repository, you should see a "Quick setup" page. Make sure the "SSH" option is selected, then click the "Copy to clipboard" symbol next to the repo URL.

Behind the scenes, GitHub has essentially `git init`'d a blank directory.

## Connect a Local Repository to a Remote Repository

After you've created your _remote_ GitHub repository, you'll want to get your local repository uploaded to GitHub. Follow the appropriate steps below:

1. We want to create a new directory and add a file so our first step is to change into our `code` directory by typing `cd ~/code` into the terminal. (If your development directory is named something other than `~/code`, that's fine, `cd` into whatever yours is called.) Our terminal should display `code` (or whatever you decided to name your development directory), indicating that you are now inside of our development directory.

      ```bash
      ~ $ cd ~/code
      ```

2. Next, create a new directory named `my_new_directory` by entering `mkdir my_new_directory` in the terminal.

      ```bash
      code $ mkdir my_new_directory
      ```

3. We're going to move from development directory into the newly-created directory by typing `cd my_new_directory`. Our terminal should display `my_new_directory`.

      ```bash
      code $ cd my_new_directory
      my_new_directory $
      ```

4. Let's create a new file named `README.md`. Type `touch README.md` into the terminal. In the file tree, if you expand the folder `my_new_directory`, you should now see your `README.md` file. Click on it to open it in the text editor.

      ```bash
      my_new_directory $ touch README.md
      ```

5. We can directly type in content here, but we can also use our terminal skills to add content. So, in the terminal, type `echo "This is my readme file" > README.md`. If you've got the README file open, the new text will appear!

      ```bash
      my_new_directory $ echo "This is my readme file"
      ```

6. Now that we've got some basic content, we can initialize our local repository. In your terminal, type `git init`. Our terminal should show that an 'empty Git repository' has been initialized.

      ```bash
      my_new_directory $ git init
      ```

7. Type `git add README.md` to stage the new `README.md` file so it will be tracked by Git.

      ```bash
      my_new_directory $ git add README.md
      ```

8. Now, type `git commit -m "Initialize git"`. This will create the first commit for this local repository, which will allow us to push our work to the remote we created earlier.

      ```bash
      my_new_directory $ git commit -m "Initialize git"
      ```

## Set the Destination of a Repo with `git remote`

To connect your local repository to the newly created Github repository, you must add a new remote to a remote name. Adding a remote involves giving `git` a "short name" and a "repository path". You copied the repository path from GitHub a few steps above.

The repository path is a long bunch of technical words. The creators of Git thought it would be easier to type a "nickname" or a "short name" that points to that long repository path. It's common to have a "default" remote. The default remote short name is called `origin`. And so, we're going to create a new remote with a short name of `origin`.

Make sure you still have your remote Git info copied from GitHub, and type the following into the terminal:

```bash
my_new_directory $ git remote add origin <your-copied-remote-repository-URL>
```

This sets the remote so you can now _*push*_ your code.

You can use `git remote -v` (the `-v` is for "verbose") to view the remote(s).

```bash
my_new_directory $ git remote -v
# View existing remotes
# origin git@github.com:OWNER/REPOSITORY.git (fetch)
# origin git@github.com:OWNER/REPOSITORY.git (push)
```

## Send Code to the Remote Repo with `git push`

Now that we have added a remote repo, we need to send our latest work to the remote. We use this command when we want to send some code from the local repository to the associated remote repository. Git will push all the local committed work to the remote repository.

The `git push` command take two arguments. The first is the name of the remote repo. Remember, you can use `origin`—an alias or "short name" that refers to the repository name. The second is the name of the remote branch you want to send code to. In the example below, we're pushing to out remote repository's _default_ branch, `master`.

```bash
my_new_branch $ git push -u origin master
```

This will push your code up to the remote repo/branch. The first time you push code up to a newly-added remote repository, use the `-u` flag to tell Git to "save" the remote repository as the default push destination. For every subsequent push, you only need to enter `git push`.

## Conclusion

Being able to add Git remotes allows you to back up your local repository to a remote server. If you remember `git init`, git remote add origin your-remote-repository-URL`, add, and push your changes, you'll be able to get your project up to GitHub in minutes!

## Resources

[GitHub Guide on Pushing](https://help.github.com/articles/pushing-to-a-remote/)
