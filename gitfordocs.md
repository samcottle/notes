# Git for docs

Git works on both text and binary files (images, video, audio, etc.), and generally treats both as the same. It's not great at merging binary files, though, so will just ask you to choose one over the other.

## Git stages

1. **Unstaged** - Local change to a file (or added or deleted the file). Use this when additions have been made, but you're unsure whether you want to use them yet. This is basically an unsaved file.
2. **Staged** - You've marked a local change as something you want to commit/save in Git. Use this when you're pretty sure you want to keep the changes. Basically a saved file; saved using the `git add` command.
3. **Committed** - You've committed the file, saving this version of it in Git (and should have a description to help you remember what it's about). Use this when you definitely want to keep the changes. Committed using the `git commit` command (along with the description).
4. **Pushed** - The file has been uploaded to the Git server, so others can access it. Use this when you want to share the changes with others. This is done with the `git push` command.

## Git commands

- `git status`: Useful information, such as which files are **staged**.
- `git add`: Moved files from **unstaged** to **staged**.
- `git commit`: Commits any **staged** files. You'll also need to add a description of what you committed, so `git commit -m "Added new file."` would commit the file with the message "Added new file.".
- `git push`: Uploads **committed** files to server (such as GitHub). You'd generally use `git push origin` here, which pushes the file back to the repo you cloned it from.
- `git log`: Shows you the history of git commits. For an easier to read version, there's `git log --oneline`.
- `git checkout`: Lets you choose which commit or branch you want to work on. Fow example, to work on the most recent version on the `master` branch you'd use `git checkout master`.
- `git tag`: Can be used by itself to see a list of all tags that have been made, or in combination with some arguments to tag a commit (`git tag -a tag_name -m "Description for the tag"`).
- `git pull`: Pulls all the commits that have been made to the repository. You can *only* use this if you have committed your files.
- `git branch`: Can be used by itself to list branches, or with an argument to create a new branch (when doing this, it won't automatically move you to that branch).
- `git stash`: Creates a new stash, and reverts to the latest commit. Can use the `list` argument to list all the most recent stashes, and the `pop` argument restores the most recent changes.
- `git diff`: Compared two branches, for example `git diff branch-a branch-b`.
- `get merge`: First, change to the branch you want to merge into. Then, merge the branch you want to add. For example, if you're in `branch-a` and want to merge your changes from `branch-b` use `git merge branch-b`.
- `git clone`: Used to clone a remote repo locally. `git clone` is usually followed by a URL for a `reponame.git`.

## Doing stuff in Git

### Renaming files

Best to rename the file using the command line, with `mv`. So to rename `file-1.md` to `file-a.md` you would use `mv file-1.md file-a.md`. The renamed file is treated as a new file, which hasn't yet been **staged** or **committed**, so you'll need to do these after.

### Deleting files

When files are deleted they become **unstaged**. The deletion hasn't yet been **staged** or **committed** in Git, so you'll need to do these after.

### Reverting to other versions

By checking out a previous version with `git checkout previous_checkout_hash`, your local files will be reverted back to that version too. The version you are working on is referred to as HEAD.

**Note:** Don't go back to a previous version and make changes to that. It'll often create nothing but a mess.

### Tagging files

This is commonly used to label a commit as a release. It's used to make a commit easier to find. To checkout a commit with a tag, you'd use `git checkout tags/tag_name`. If using a GitHub (or another GUI-based Git tool), this you can find a tagged release in the **Tags** tab (which is hidden under **Branches**).

### Pulling changes

There are three ways in which a pull is handled:

1. If the remote file is the same as the last pull, the local file will be left as is.
2. If the remote file has changed but the local file is the same (i.e. someone else has pushed updates), the local file is replaced with the remote file.
3. If both the remote and local files have changed, it will try and merge the remote file into the local file. When it can't do this, it's known as a *merge conflict*.

**Note:** Remember that you can *only* use `git pull` if you have committed your files.

### Resolving merge conflicts

When there's a merge conflict you get a bunch of `<<<<<<<<<<` and `>>>>>>>>>>>` markup that corresponds to where the conflict occurs. To resolve this:

1. Update the file locally.
2. `git add .`
3. `git commit -m "With a relevant message"`
4. `git pull`

### Working with branches

Once you've created a branch with `git branch new-branch`, you can switch to it with `git checkout new-branch`.
**Note:** You'll need to commit all your changes before you can move to the new branch (or use `git stash`).

When creating branches, you can use `/`s in the name. This is useful when you want to use naming conventions like `version1/docs` (to distinguish, say, the docs of a feature from the feature itself `version1/newfeature)`. The new branch will be created remotely when you use `git push`.

To delete, use `git branch -d branch-name`. You should only really do this once you've merged the branch.

### Using stash

Is how you "stash" changes if you're not ready to commit yet. You can resume working on a stash by "popping" it. They don't typically use names, but you can add them with `git stash save "stash-name"`.

### Merging branches

Easiest to do this using a GUI tool (GitHub, etc), by creating a pull request. The two ways to do this using a GUI:

1. Merge pull request: Every commit on the new branch becomes a commit on the original branch (i.e. Master).
2. Squash and merge pull request: Simplifies the history by *squashing* down all the commits on the new branch into one commit on the original branch (i.e. Master).

Can also be done using the command line using the commands `git diff` and `git merge`.

### Ignoring files

To exclude any build files from being committed to Git:

1. Create a file called `.gitignore` in the top level of the repo.
2. In this file, list any files or folders you want Git to ignore.
3. Add the file to the repo and commit it.

#### Example `.gitignore` file

```text
# Comments start with a #, and use the format:
folder/file.md

# A * can be used as a wildcard. So to ignore all .txt files:
*.txt

# To ignore an entire folder:
folder/
```

### Forking

This is like branching an entire repo, so you can play with changes without impacting the original project. Changes can then be merged back from the fork to the original repo. It's basically a way of allowing anyone to make changes to an open source project.

**Note:** Forking is a feature of GitHub (or similar tool), not of Git.

To fork in GitHub:

1. Go to the project.
2. Click the **Fork** button.

Then, once you've made the changes you want to merge with the original repo:

1. Click **Create pull request**.
2. Follow the instructions.

## Troubleshooting

### Resetting back to the last unstaged changes

If you've made changes you don't want, you can remove them with `git reset --hard`.

### Overwriting your local version with the remote version

1. `git fetch origin`
2. `git reset --hard origin/remoteBranchName`

### A fallback option

One 'unofficial' way to solve Git issues:

1. Copy changed files to a folder outside the repo.
2. Revert changes back to a point where Git works again.
3. Manually merge the changes back in.

### The 'absolutely nothing else works' option

1. Copy changes to files outside of the repo.
2. Delete the local repo.
3. Clone the folder again, into a new folder.
4. Manually merge the changes back.
5. Go and drink some coffee.
