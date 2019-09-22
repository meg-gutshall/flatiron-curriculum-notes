# Lesson: Setting Up A New Site

## Notes

### Setting Up Your GitHub Repository

- Start by creating some initial folders and files before creating a remote git repository online.
  - Create a project folder and add a `README.md` file to that folder. Add some content to the `README.md` file. Here's [a template to make a good `README.md`](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2).
  - Then create a `.gitignore` file, which is _essential_ in preventing private and/or sensitive files from being shared publicly when your repository is online. Here's [a list of common `.gitignore` configurations to populate this file](https://gist.github.com/octocat/9257657).
- Now that we've got some files in our project, let's initialize a new git repository locally, then create a remote repo and connect them.
  - To initialize a new git repository locally, in our project folder type `git init`.
  - If you type `git status` in your terminal, you should see the files we just created listed as "Untracked files". Since these files are untracked, any changes made to them won't be recognized by our git repository yet.
  - To try the files we've created and changed, type `git add .`. Then, we want to commit these changes to our git repo by typing `git commit -m "Initial commit"`.
  - If you type `git status` now, you'll see that our files are no longer listed, and that there is "nothing to commit, working tree clean", meaning there are no new changes since the last commit.
- We've got our local work ready to go, so now we need to set up a new remote repository to store this in.
  - Open a new browser tab and go to [github.com](https://github.com/), making sure you are signed in.
  - In the upper right-hand corner of the page, click the `+` button and choose _**New repository**_.
  - You'll be brought to the _**Create a new repository**_ page. We can go ahead and name this repository the same name we gave our folder, so in the _Repository name_ field, enter the project folder's name. Then, we'll add a brief description of what this repository is for in the _Description_ field.
  - We can leave this repository set to _Public_. We also already have a README.md file, so we do not need to initialize this repository with one. Click _**Create repository**_ to continue.
  - GitHub provides commands in the _**Quick setup**_ page for starting from scratch, pushing an existing local repository, or importing code from another repository. In our case, we need commands for "pushing an existing repository". The URL provided will be unique to your GitHub username and repo, so copy the first command that starts with `git remote add origin https://github.com/...`. Paste the copied command into your terminal and press return.
  - To push up your local work to this new remote repository, we'll use the second command GitHub provides: `git push -u origin master`. This tells our git repository to push up to our remote repository, `origin`, using our local repository's `master` branch. The `-u` is necessary the first time we do this, as it also tells git to set up tracking between our local and remote `master` branches.
- Always push up any work you want to keep and access again!

### Adding Branches

- When you type `git branch` from the terminal while inside your repository folder, this command will show you all the existing branches that are stored locally on your computer. As a general best practice, the `master` branch should always be kept in a fully functional state; any new features or additions made on a repo should be done on a separate branch, allowing one or more developers to work on isolated parts of a project without interfering with the `master` version until the branch code is fully ready.
- To create a new branch, type `git checkout -b branch-name`. Your terminal should now display that you are on a new branch, `(branch-name)`, instead of `(master)`.
- Create new files in the branch but using your terminal and the command `touch`, followed by the name of the file.
  - Naming these files based on what they will contain will keep us better organized, and can also help when it comes to search engine optimization, as search engine bots can use file names to find relevant search information.

### Retrieving Files Using the `wget` Command

- We will need a separate folder for storing some image files. Create a directory using `mkdir` and name it `images`.
- Copy the full URL path of the image, navigate (`cd`) into your `images` folder, and type `wget` followed by the image URL.

### Wrapping Up

- Since our new features aren't complete, we want to make sure the branch we're currently working in is stored separately from our `master` branch in our remote repository. To do this:
  - Stage your changes: `git add .`
  - Commit your changes with a message: `git commit -m "add content pages to website"`
  - Push your changes to your remote repository while also setting up tracking between your remote and local branches: `git push -u origin branch-name`
- Use `git fetch --all` when cloning down a remote repository so you'll retrieve all branches for access on your local environment.
