# TenderMe 

TenderMe is a software designed and developed to help people write their service descriptions. We do this by providing suggestions for the service description and a template for service description.

## Overview


## Components in this repository

* [Frontend (React.js)](app)
* [Backend (Java)](API)


## Contribution guidelines

* # Guidelines for working with Git

## Brief overview of the most important commands

| Command                                                        | Description                                                                                                                                                                        |
|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git status`                                                   | Tells you the current status of your local working copy's "index" (whether you have modifications that are not committed yet).                                                     |
| `git checkout <branch>`                                        | Checks out the branch specified by `<branch>`. **Only do this when `git status` is clean!**                                                                                        |
| `git checkout -b <new_branch>`                                 | Creates a new branch based on the current commit. **Only do this when `git status` is clean!**                                                                                     |
| `git diff` / `git difftool`                                    | Shows all local (uncommitted) modifications.                                                                                                                                       |
| `git pull`                                                     | Grabs the latest commits on the current branch from the remote and attempts to merge them into your local copy. **Only do this when `git status` is clean!**                       |
| `git fetch`                                                    | Grabs information about the latest commits and new branches from the remote **but does not actually change your working copy**.                                                    |
| `git add <file1> <file2> ... <fileN>`                          | Adds all current modifications in the given file(s) to the "index". This is done in preparation for a commit.                                                                      |
| `git commit -m "<Commit message>"`                             | Creates a new commit with the "added" changes.                                                                                                                                     |
| `git commit <file1> <file2> ... <fileN> -m "<commit_message>"` | Creates a new commit only containing the modifications in the given file(s).                                                                                                       |
| `git push`                                                     | Pushes all new commits on the current branch to the remote. This only works when there are no newer commits in the remote already. **Only do this when `git status` is clean!**    |
| `git merge <branch>`                                           | Merges all the commits that are on `<branch>` and not on the current branch into the current branch. This will create a merge commit! **Only do this when `git status` is clean!** |

## Normal developer workflow

(This example is from the POV of a frontend developer.)

1. `git status` to check that you're not having any local modifications that might cause problems down the road. Ideally, you always start with a "pristine" repository.
2. `git checkout master` to go to the `master` branch.
3. `git pull` to receive and merge the latest changes from the remote.
4. `git checkout -b <my_feature_branch>` to create a new feature branch forking off from the latest `master`.
5. `cd app` to get into the frontend groove 😀.
6. `npm install` to update dependencies (optional - this is only needed when there were changes to `package.json` and/or `package-lock.json`).
7. Iterate:
   1. Apply code changes needed for the feature / bugfix you're working on right now.
   2. `git add .` to add the changes to git's "index" (instead of adding the whole `.`, you could add individual files, too).
   3. `git commit -m "Implemented the most awesome feature"` to create a commit with your changes.
   4. Maybe go back to 7.i. and repeat

Now you can **either** push your branch to the remote to have a colleague review your changes and only then merge the branch back into `master` **or** if you're feeling confident, you can integrate your changes back into `master` directly.

### Pushing a new branch

When you created a local branch that doesn't exist in the remote yet, a simple `git push` will fail with a message that looks like this:

> fatal: The current branch my-awesome-feature has no upstream branch.
> To push the current branch and set the remote as upstream, use
> 
>     git push --set-upstream origin my-awesome-feature

Git is really nice because it tells you what to do in most cases 😏 So in this case, just copy/paste the command it proposed to you in order to push the new branch to the remote.

Now, everybody else can `git fetch && git checkout my-awesome-feature` to take a look at your changes.

### Merging a branch back into `master`

1. `git status` to check that you're not having any local modifications that might cause problems down the road. Ideally, you always start with a "pristine" repository.
2. `git checkout <branch> && git pull` to get the latest changes on the feature branch.
3. `git checkout master && git pull` to get the latest changes on the `master` branch, as well.
4. `git merge <branch>` attempts to merge all changes from `<branch>` into the `master` branch by creating a new merge commit. If there are any conflicts, this will not create the commit but leave your working copy in the "merging" state. You can (must) now take a look at the conflicts and resolve them manually. Once all conflicts are resolved, `git add` all files back into the index and `git commit` to proceed with the merge.
5. `git push` to push the merge commit into the remote's `master` branch so that everybody else in the team gets these changes, too.
6. `git delete <branch>` (only if you don't plan to continue working on this branch after has been merged).

## Rules

* **NEVER** overwrite a file with another one (from someone else). To exchange modifications, use `git add` + `git commit` + `git push` on one side and `git pull` on the other side.
* **NEVER** work directly in the `master` branch.
* **NEVER** leave uncommitted work on your PC at the end of the day, or before a weekend.
* **ALWAYS** try to keep your local repository as clean as possible, i.e. don't have dozens of modified files lying around as this greatly complicates merging, pulling, etc.
* **ALWAYS** provide a good, descriptive commit message.
* **ALWAYS** try to have each commit only contain changes related to a specific change. It's better to have a few smaller, well-commented commits than to have just one huge commit with several days of work in it and dozens of potentially unrelated changes mixed together. 


