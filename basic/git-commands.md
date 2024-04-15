---
title: "Git commands you need to know!"

subtitle: "Git commands you need to start using today to boost your coding efficiency"

slug: "git-commands-you-need-to-know"

tags: git, version control, git commands, git basics, git tutorial

cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1713202707580/xYs0WPJT2.webp?auto=format

domain: 10xdev.codeparrot.ai

saveAsDraft: false
---

Understanding version control is essential for novice developers navigating the world of coding, and Git is frequently at the forefront of this learning curve. Git is an effective tool for managing source code history, and being proficient with its commands can greatly increase your productivity and self-assurance as a developer. In order to make your trip easier, this blog post will walk you through the key Git commands you should be familiar with, along with explanations and examples that are suitable for beginners.

### Basic Git Commands

Git is based on a few fundamental commands that form the basis for all operations. Here's how to get going:

#### `git init`: 
This command is used when you start a new project and you want Git to track the changes you make to the files in the project. By running git init, you create an invisible folder inside your project that Git uses to store information about what has changed over time.

Example:
Imagine you’ve created a new folder on your computer for your website project. To start tracking changes with Git, you open a command prompt or terminal, navigate to this folder, and type git init. Now, Git is ready to track changes in this folder.

```bash
mkdir new-project
cd new-project
git init
```

#### `git clone [url]`:
To work on an existing repository, use git clone followed by the repository's URL. This command copies all the data from the repository to your local machine.

Example:
You find a project on GitHub that you want to contribute to or study. You can copy the URL provided on GitHub, open your command prompt or terminal, and type git clone followed by the URL. This action downloads everything in that project to your computer, allowing you to work on it locally.

```bash
git clone https://github.com/example/project.git
```

#### `git add [file]`: 
Before changes can be recorded, they must be added to the staging area. git add lets you select specific changes you want to commit. You can add individual files or all changes at once. To add all changes, use `git add .`.

Example:
You’ve just created a new file in your project called index.html and you've made changes to an existing style.css. To let Git know you want to track these changes, you would run git add index.html style.css. Now, Git is aware of these changes, and they're ready to be committed (or saved).

```bash
git add index.html style.css
```

#### `git commit -m “message”`: 
To save your changes, use git commit. The -m option allows you to add a brief description of the commit, providing context for the changes made.

Example:
After adding changes with git add, you would run git commit -m "Add homepage and update styles". The -m followed by a message allows you to add a brief description of what was done, making it easier to remember or understand what was changed later on.

```bash
git add index.html style.css
```

#### `git pull`:
A combination of git fetch and git merge. This command fetches the latest changes from the remote repository and merges them into your local branch.

Example:
To update your current branch with the latest changes from the remote, you would run git pull. This pulls changes and directly merges them.

```bash
git pull origin master
```

### Inspecting a Repository

Understanding what has changed or checking past changes is crucial:

#### `git status`:
Sometimes, you need to check what has been changed or what is ready to be committed. Using git status gives you an overview of everything that’s happening in your project concerning file changes, whether they're tracked or not, and if they're staged for a commit.

Example:
Before deciding to commit, you might run git status to see which files are modified and ready to be committed, and which files are there that Git isn’t tracking.

```bash
git status
```

#### `git log`:
This command is used to view the commit history of the repository. It shows a list of recent commits, including the author, date, and the commit message.

Example:
To see the history of your project, you would run git log. This would display all commits made to the repository in reverse chronological order, providing insight into the changes over time.

```bash
git log
```

#### `git diff`:
Use git diff to see the exact changes made to the files. This command shows the differences between the files in the working directory and the staging area, or between staged changes and the latest commit.

Example:
If you want to see what changes you’ve made to a file before committing, you would run git diff. This would show the line-by-line changes made since the last commit.

```bash
git diff
```

### Branching and Merging

Branching in Git allows you to diverge from the main line of development and continue to work without affecting the main line.

#### `git branch [branch-name]`:
This command is used to create a new branch named [branch-name].

Example:
If you're developing a new feature, you might create a new branch by running git branch feature-x. This keeps your feature work separate from the main code base until it's ready to be merged.

```bash
git branch feature-x
```

#### `git checkout [branch-name]`:
Switches you to the branch [branch-name]. This command lets you navigate between branches created by git branch.

Example:
To switch to the branch you just created, you would run git checkout feature-x.

```bash
git checkout feature-x
```

#### `git merge [branch]`:
Merges the specified branch into the current branch. This command is used to bring changes from one branch into another.

Example:
After completing work on feature-x, and if you're currently on the master branch, you would run git merge feature-x to incorporate the changes from feature-x into master.

```bash
git merge feature-x
```

### Advanced Commands

As you become more comfortable with the basics of Git, you'll likely encounter situations where more advanced commands are useful.

#### `git rebase [branch]`:
Git rebase is used to reapply commits on top of another base tip. This is useful for keeping your branch up to date with the master or main branch without creating merge commits.

Example:
If your feature branch is behind the master branch, you might run git rebase master while on your feature branch. This will move your entire branch to begin on the tip of the master branch.

```bash
git rebase master
```

#### `git stash`:
Saves your local modifications away and reverts the working directory to match the HEAD commit. Useful for quickly switching contexts without committing half-done work.

Example:
If you need to switch branches but don't want to commit your current changes, you could run git stash to save them. Later, you can use git stash pop to reapply the stashed changes.

```bash
git stash
git stash pop
```

#### `git fetch`:
This command downloads commits, files, and refs from a remote repository into your local repo.

Example:
Running git fetch origin would pull the latest changes from the origin remote (typically where you cloned from) without merging them into your local files.

```bash
git fetch origin
```

#### `git cherry-pick [commit]`:
This command is used to apply the changes introduced by some existing commits from one branch into another branch. It's useful for pulling in specific changes without merging or pulling in all changes from another branch.

Example:
Suppose a colleague has made a commit on the develop branch that fixes a bug, and you want to apply that fix to your feature branch:

```bash
git cherry-pick 4a2b6f
```

Here 4a2b6f is the commit hash (identifier) of the commit you want to apply to your branch.


#### `git bisect`:
Use git bisect to find the specific commit that introduced a bug. Git will automatically mark the good (bug-free) and bad (buggy) commits, performing a binary search to quickly pinpoint the problematic commit.

Example:
If you know a recent commit has caused a regression in your code:

```bash
git bisect start
git bisect bad       
git bisect good 1234abcd
```

Git will then check out a commit halfway between the good and bad commits. You test this commit, tell Git if it's good or bad, and continue until Git isolates the bad commit.

#### `git reflog`:
Sometimes, you might lose commits or branches after complex Git operations like rebase. The git reflog is used to record when the tips of branches and other references were updated in the local repository. It's a safety net that allows you to see all your past actions and can help you recover "lost" commits.

Example:
To see your recent operations and find a commit you might have lost:

```bash
git reflog
```

You’ll see a list of recent actions (like commits, rebases, etc.) with their respective commit hashes. From there, you can check out or reset to any of those commits if needed.

### Conclusion

In conclusion, mastering these essential Git commands can significantly enhance your development workflow. From basic setups to advanced maneuvers, each command plays a critical role in efficient project management. Keep practicing to fully leverage Git’s capabilities and streamline your coding process.

