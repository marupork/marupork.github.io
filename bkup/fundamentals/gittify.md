---
layout: default
---

# Gittify

[<<](../)

## Table-Of-Contents

- [Rebase branch to latest develop](#rebase-branch-to-latest-develop)
- [Squash Commits](#squash-commits)
- [Merge branch to develop](#merge-branch-to-develop)
- [Rename remote branch](#rename-remote-branch)
- [Git Branches](#git-branches-cookbook)

## rebase-branch-to-latest-develop

- Rebase develop to latest

    ```console
    feature/A:$ git checkout develop
    develop:$ git pull origin develop
    develop:$ git pull --rebase
    develop:$ git checkout -
    ```

- Rebase branch to develop

    ```console
    feature/A:$ git rebase develop
    ```

- if conflict:
  - fix conflict via intellij or cmd
  - add changed files and continue rebase

      ```console
    git add .
    git add <files-with-conflict>

    git rebase --continue
    ```

- Push changes

    ```console
    feature/A:$ git push -f origin feature/A
    ```

## squash-commits

```console
git rebase -i HEAD~4
    pick, fix
git push -f origin feature/A
```

## merge-branch-to-develop

```console
feature/A:$ git checkout develop
develop:$ git pull origin develop
develop:$ git merge feature/A
develop:$ git push origin develop
```

- Alternative
  - Step 1: Fetch and checkout the branch for this merge request

    ```console
    git fetch origin
    git checkout -b "feature/ABC-123" "origin/feature/ABC-123"
    ```

  - Step 2: Review the changes locally
  - Step 3: Merge the branch and fix any conflicts that come up

    ```console
    git fetch origin
    git checkout "origin/develop"
    git merge --no-ff "feature/ABC-123"
    ```

  - Step 4: Push the result of the merge

    ```console
    git push origin "develop"
    ```

## rename-remote-branch

- Rename the local branch

    ```console
    git branch -m <new_name>
    ```

- Push the `new_name` local branch and reset the upstream branch

    ```console
    git push origin -u <new_name>
    ```

- Delete the `old_name` remote branch

    ```console
    git push origin --delete <old_name>
    ```

## git-branches-cookbook

```console
$ git branch
List local branches
$ git branch -r
List remote-tracking branches
$ git branch -a
List both remote-tracking branches and local branches

$ git branch -r --merged develop
List of remote branches merged into develop
$ git branch -r --merged develop | grep branchName
List of remote branches merged into develop matching the branchName
```

- Reference
  - [Git-Branching-Branches-in-a-Nutshell](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)
  - [Git-Branching-Basic-Branching-and-Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
  - [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)

[<<](../)
