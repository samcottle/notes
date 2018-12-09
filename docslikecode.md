# Git for docs

Git works on both text and binary files (images, video, audio, etc.), and treats both as the same. The difference is that binary files can be difficult to merge, and so Git won't even try and merge them (it'll just ask you to choose one over the other).

## Git stages
1. Unstaged - Local change to a file (or added or deleted the file). Use this when additions have been made, but you're unsure whether you want to use them yet. This is basically an unsaved file.
2. Staged - You've marked a local change as something you want to commit/save in Git. Use this when you're pretty sure you want to keep the changes. Basically a saved file; saved using the `git add` command.
3. Committed - You've committed the file, saving this version of it in Git (and should have a description to help you remember what it's about). Use this when you definitely want to keep the changes. Committed using the `git commit` command (along with the description).
4. Pushed - The file has been uploaded to the Git server, so others can access it. Use this when you want to share the changes with others. This is done with the `git push` command.

## Git commands
- `git status`: Useful information, such as which files are **staged**.
- `git add`: Moved files from **unstaged** to **staged**.
- `git commit`: Commits any **staged** files. You'll also need to add a description of what you committed, so `git commit -m "Added new file."` would commit the file with the message "Added new file.".
- `git push`: Uploads **committed** files to server (such as GitHub). You'd generally use `git push origin` here, which pushes the file back to the repo you cloned it from.
- `git log`: Shows you the history of git commits. For an easier to read version, there's `git log --oneline`.
- `git checkout`: Lets you choose which commit you want to work on. Fow example, to work on the most recent version on the `master` branch you'd use `git checkout master`.
- `git tag`: Can be used by itself to see a list of all tags that have been made, or in combination with some arguments to tag a commit (`git tag -a tag_name -m "Description for the tag"`).

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