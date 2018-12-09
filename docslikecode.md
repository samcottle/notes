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
- `git commit`: Commits any **staged** files.
- `git push`: Uploads **committed** files to server (such as GitHub). You'd generally use `git push origin` here, which pushes the file back to the repo you cloned it from.
