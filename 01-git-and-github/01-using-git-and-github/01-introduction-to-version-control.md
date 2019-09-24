# Introduction to Version Control

## Naive Strategy

A naive way of managing file versions is to keep a "latest" copy and a "master" copy. "Latest" would act as the working version in which changes would be made, verified, and then merged into "master". In addition to this "master" would be duplicated and then renamed with an [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date-time label to track when each change occurred, allowing the files to automatically list themselves in ascending order.

The problem here though, is this can get messy very quickly when it comes to merging files together and remembering which versions have been copied and saved. Also when you have multiple people working on the same version of a file, merge conflicts will arise.

Luckily, we have a type of software called a _version control system (VCS)_ that automatically keeps track of this for us. The most popular VCS is called "Git".

## Define the Purpose of a Version Control System

"Version Control System (VCS)" describes a whole group of software. This includes Git, Mercurial, Subversion, and others. Some other web-based applications like Google Docs have embraced the idea of "versions" and have added features like "tracked changes" or "view change history".

The key benefit of version control is that you can experiment and **throw away bad ideas** and _instantly_ get back to your last-known "good" state. Because of the freedom that VCS provides, we can be unafraid to try new and improved coding techniques.

## Identify Benefits of Version Control Systems

Beyond the advantage of being able to safely experiment, there are several other benefits we get when we manage out work with Git:

- Automatically create a backup of your work
- Provide an easy way to undo mistakes and restore a previous version of your work
- Document changes, including a log of what's changed with messages explaining why it was changed
- Keep file names and hierarchies consistent and organized
- Branch off into multiple "sandboxes" that can be experimented with but won't impact each other
- Collaborate with others without disturbing each other's or our own work

## Recognize Useful Git Vocabulary Terms

- **repository** (or **repo** for short): A directory of files that are _tracked_ by Git.
- **track**: When a file is _tracked_ by Git, it means that Git will notice and changes to that file. We call these changes "differences" or "diffs". Git will allow you to choose whether to _add_ the change, or "diff", in order to keep it.
- **diff**: Short for "difference", the "diff" of a file is all the changes that happened in it since the last _commit_. The "diff" of a repo is all the diffs in all the _tracked_ files in the _repo_ that have been made, but which have not yet been _committed_ (sometimes programmers call this "the diffset").
- **commit**: When a diff is decided to be a good thing to save, we _commit_ the diff to the repo's history using the `commit` command. When we make a commit, we are asked to write a "log" message which describes what happened in the diff. Each commit also knows when it happened and what the repo's "diff" was.
- **log**: The record of what happened in each commit.
- **local/remote**: When we start working with a Git repo, we "clone" it from a _remote_ source and have a copy of that directory on our system. We call the repo on our personal system the _local_ repo. (We'll talk more about the "clone" command later.)
- **`master` branch**: You'll learn in advanced Git that a repo can support multiple branches (we called those "sandboxes" earlier). For the moment, just remember this: by default, when you create a Git repo, you will be working on the `master` branch.
- **branch**: The combined history of all the changes of all the files in the repo.

## Conclusion

Version control helps us maintain the overall stability of our code so that we can feel free to explore.

### Resources

[Getting Started – About Version Control](http://git-scm.com/book/en/Getting-Started-About-Version-Control)<br>
[Git Basics – What Is Git?](http://git-scm.com/video/what-is-git)
