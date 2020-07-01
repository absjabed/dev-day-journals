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
