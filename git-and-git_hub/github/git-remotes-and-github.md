# Lesson: Git Remotes and GitHub

## Notes

### Creating a new repository in GitHub:

1. While logged into GitHub, click the + in the menubar and select `New repository`.
2. Enter a name for your repository in the `Repository name` field, then click the green `Create repository` button.
3. After you create the repo, you should see a "Quick setup" page. Click the "Copy to clipboard" symbol next to the repo URL to copy the URL.

### Connecting your remote repo to a local repo:

1. In you terminal, create a new directory and add a file.
2. Change into your `code` directory: `cd ~/code` (or whatever you named your development directory)
3. Create a new directory named `my_new_directory`: `mkdir my_new_directory`
4. Change into the newly created directory: `cd my_new_directory`
5. Create a new file named `README.md`: `touch README.md`
6. Add some text to the new file: `echo "This is my readme file" > README.md`
7. `git init`
8. `git add .` + `git commit -m "initialize git"` (Add and commit the new file created in step one.)
9. `git remote add origin your-remote-depository-URL` (This sets the remote so you can push and pull code.)

- "Origin" is simply the default alias assigned to your new remote repo.

### `git push`

- This command is used when we want to send some code from the local repository to the associated remote repository.
- `git push` takes two arguments: the name of the remote repo and the name of the remote branch you want to send code to
  - Run `git branch -r` to find all the branch names
- The first time you push the code, add the `-u` flag to tell Git to track the remote repository: `git push -u remote_repo remote_branch`
  - Every subsequent push can use `git push`

### `git pull`

- This command is used to pull down any changes others have made on the remote repository to our local machine.
- This can also take remote repo and remote branch arguments if need be: `git pull remote_repo remote_branch`