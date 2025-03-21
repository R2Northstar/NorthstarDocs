---
description: Core squirrel mods
---

# NorthstarMods

TODO

## Reviewing PRs committing vanilla files

When adding new Squirrel script source files that are from the base game, make sure to commit the unmodified file first.
This process is done to later leverage the power of `git blame` to see who authored a particular code line, which assists with better understanding changes in the codebase.

### 1. Update the PR branch

Before adding vanilla files to `main`, make sure that the corresponding PR is up-to-date.
Adding the vanilla file will cause a merge conflict on the PR, that is expected.

In case you forgot to update the PR first, you can also merge the commit before that into the PR branch manually by using `git merge <commit hash>`.

### 2. Add vanilla file to `main` NorthstarMods

In particular, when pushing on `main` branch, they should be committed as `Respawn` with the email address `respawn@northstar.tf`:

```sh
git -c user.name="Respawn" -c user.email="<respawn@northstar.tf>" commit -m "Add SQUIRREL_FILE.nut from VPK_NAME"
```

### 3. Merge the change in the PR branch

Afterwards, update the PR branch by ignoring the commit from `main` by checking out the PR branch and merging with:

```sh
git merge --strategy=ours main
```

This will merge `main` into the PR branch and always prefer the changes from the PR branch in case of conflict.
