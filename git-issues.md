## Tue 09/01/20
### Modify last git commit or unpushed commit message?
```sh

# Add latest changes:
git add .

# Amending the most recent commit message
git commit --amend -m "New commit message"

```
[Reference](https://docs.github.com/en/github/committing-changes-to-your-project/changing-a-commit-message)

---

## Sat 18/07/20
### Create a New local branch and push it tp remote Git repository and track it.
```sh

# Create a new branch:
git checkout -b feature_branch_name

# Edit, add and commit your files.
git add . && git commit -am "comment on your changes..."

# Push your branch to the remote repository:
git push -u origin feature_branch_name

```
[solution](https://forum.freecodecamp.org/t/push-a-new-local-branch-to-a-remote-git-repository-and-track-it-too/13222)

---

## Wed 17/06/20
### Rename a Local and Remote Git Branch 
```sh
# Rename the local branch to the new name
git branch -m <old_name> <new_name>

# Delete the old branch on remote - where <remote> is, for example, origin
git push <remote> --delete <old_name>

# Or shorter way to delete remote branch [:]
git push <remote> :<old_name>

# Push the new branch to remote
git push <remote> <new_name>

# Reset the upstream branch for the new_name local branch
git push <remote> -u <new_name>

# delete branch locally
git branch -d localBranchName

# delete branch remotely
git push origin --delete remoteBranchName

```
[solution](https://stackoverflow.com/a/30590238/5277438)

---
