# Lesson: Git Collaboration

## Notes

- A key to collaborating with Git is to keep discrete and individual lines of work isolated from each other.
  - We can do this using branches.
- Whenever you are working on commits in Git, you are adding them on a timeline of code called a branch.
  - The default main branch at the start of any repository is called master.
  - `git status` will always tell you what branch you are on.
  - Don't put broken code in master so you can always deploy master.
- To add a new branch, type `git branch <branch name>`.
- To see a list of branches, type `git branch -a`.
  - An `*` will be in front of the working branch where current commits would be applied.
- To move between branches, type `git checkout <branch name>`.
  - You can create and checkout a new branch in one command using: `git checkout -b new-branch-name`.
- The master branch only keeps the code from the most recent commit relative to the master timeline or branch.
- Once the code in the new branch is ready to be added to the master branch, we'll use the `git merge` command.
  - It's important to be currently working on your target branch, the branch you want to move into, when you do a `git merge`.
- When you run `git merge`, `git` will ask you to create a commit to reflect that you've done a merge. By default `git` will look for a default, console-based editor but instead we're going to direct it to use the Atom editor by typing `git config core.editor "atom--wait"`.
  - This will automatically launch Atom with an open `MERGE_MSG` tab. Describe the merge, then save and close the file.
- Whenever you want to update a local copy with all the branches that might have been added to the GitHub remote, you can type `git fetch -a`
  - The last three lines of output from this command are very important:
    - The first line is informing us which remote out `git fetch` updated from. When we `fetch` with git, we are asking to copy all changes on the remote to our local git repository, but not actually integrate any.
    - The next line tells us if and where a new commit was found.
- After you fetch, you have access to the remote code but you still have to merge it.
  - To do this, from within your local master branch, type `git merge origin/master`, referring to the branch's full path, `remote/branch`, or `origin/master`.
- The last line of a `git fetch` will display any new branches created.
  - We can access this with `git checkout`, which will trigger Git to make a local branch to track that remote and switch to that branch.
- Generally, if you are in `master` you want to immediately `fetch` and `merge` any changes to the remote master.
  - Do this more simply by typing `git pull`.