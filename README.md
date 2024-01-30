_This entire page is a 5 minute read._

# Preface

This is a beginner reference/tutorial for `git`. I will include only things that are necessary for the user to start using `git`. I will avoid mentioning complex topics or scenarios.

After reading this entire document, the user should be ready to start using `git` locally, and should be able to contribute to remote repositories as well.

# Basic Concepts

## Repository

`git` stores your project's entire history, all its branches and commits, in a hidden `.git` directory at the root of your project. This directory contains everything `git` needs to track your project.

## Working Tree

This is your working directory, your project folder, which holds all your project files in their _current_ state.

## Staging Area (Index)

The staging area is a _step_ between your working tree and the `git` repository. When you add new files to your working tree, or make changes to existing files that are being tracked, `git` doesn't automatically _absorb_ these changes. `git` will know that you've added new files (`untracked files`), or made changes to files that are being tracked (`changes not staged for commit`), but you need to explicitly tell `git` which changes you want to include in the next commit by adding them to the staging area using `git add`.

## Commit

Once you've added changes to the staging area, you can commit them to your `git` repository using `git commit`. This creates a new commit with the changes that you had `staged`. Commits are snapshots of your project at a particular point in time, and they become part of your project's history. You can `checkout` a commit (discussed later) to see exactly what your project looked like at that point in time.

## Remote

In `git`, a `remote` refers to a copy of a `git` repository that is hosted on a server or other location, separate from your local repository (local to your computer). Remotes are essentially references to the repository stored on other machines, which can be on your local network or on the internet. Remote repositories are often used for collaboration, backup, and sharing code with others.

By convention, the word "origin" is used to refer to the `remote` repository, however, it can be called anything at all. It is also possible to have multiple `remote` repositories linked to your local repository.

<!-- give example with gitlab and github as remotes -->

## What Is Github/Gitlab?

To keep things simple, I'm going to say that these are platforms, where you can store your code, your repositories. There are other alternative platforms as well.

# How to Initialize a git Repository

```shell
git init
```

# How to Add Files to the Staging Area

## Add Individual Files

```shell
git add file1.txt file2.txt
```

## Add All Files

```shell
git add . # method 1
git add -A # method 2
git add --all # method 3

```

# How to Commit Changes

Before you can `commit` a change, there must be a change in the staging area. For example, it could be a new file that has been added to the staging area, or it could be a change to a file that is already being tracked by `git`, part of the repository.

Commit messages are important. Read how to write better commit messages [here](https://www.freecodecamp.org/news/how-to-write-better-git-commit-messages/).

## Method 1

```shell
git commit -m "Add margin."
```

## Method 2

```shell
git commit -am "Add margin."
```

This will `stage` all changes and write a `commit` message all in one step.

## Method 3

```shell
git commit
```

After you type this command, the default terminal editor will open up. You will have to type a commit message, save it, then exit the editor. If you do not save a commit message, no changes will be committed.

# How to Check the Status of Your Working Tree

This will show you if there are any changes in the `git` repository, and if any new files (`untracked files`) have been added.

```shell
git status
```

# How to Switch Branches

In `git` speak, you switch branches by 'checking them out.'

## How to Checkout a New Branch

This is the same as creating a new branch. The branch will 'branch out' from your currently checked out branch.

```shell
git checkout -b BRANCHNAME
```

## How to Checkout a Pre-existing Branch

```shell
git checkout BRANCHNAME
```

# How to Handle Remote Repositories

## How to a Add "Remote"

<details>
<summary>You can get the link to your repository from your repository's main view.</summary>
<img src='./images/repo-link.png'>
</details><br>

```shell
git remote add origin git@github.com:USERNAME/REPOSITORYNAME.git
```

## How to Push Your Local Branch

```shell
git push --set-upstream origin BRANCHNAME
```

- `BRANCHNAME` is the local branch you want to push to the remote repository.
- It is assumed that you have `checked out` this branch.

## How to Fetch Remote Changes

### fetch

`fetch` will fetch all the new branches, tags, commits from `remote`, but will not _apply_ them or merge the changes. No local changes will occur.

```shell
git fetch
```

### pull

`pull` on the other hand will do a `git fetch` and then apply the changes (if there are any) to the branch that is checked out. Therefore, `git pull` is a combination of `git fetch` followed by `git merge`.

```shell
git pull
```

<!-- # Example git Workflow

```shell
git init
git add .
git commit -m "First commit."
``` -->

# Useful Aliases

## gitlogr

This alias will display the `git` commit history in a stylized fashion, including commit author names. Feel free to rename this alias to your liking.

### How to add this alias to your shell permanently

📝 This is for Linux or macOS.

1. On a new line, add the alias to your `.zshrc` or `.bashrc`.
2. Save.
3. Close the terminal currently used, and then open a new terminal.
4. While inside a folder that is tracked by `git`, type `gitlogr` to see the commit history.
5. Exit the commit history view by pressing `q`.

```shell
alias gitlogr="git log --all --graph --decorate --oneline --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'"
```
