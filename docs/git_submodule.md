# Git submodule

This project is a monorepo for the b3c product.
It aims to keep all other modules together helping developers to rapidly set their environment.
It also holds all global tools related to building, deplying and testing the product.

## Changes on git configuration

```
git config --global diff.submodule log
git config status.submodulesummary 1 # diff always show submodule status
git config submodule.recurse true # pull always update submodules
git config push.recurseSubmodules check # check no pending commits on submodules
```

## Adding a new module

Adding a new git sub module:

```
cd modules
git submodule add <repo>
git commit -am 'Add <module_name> module'
git push
```

### Cloning the monorepo

When you clone, by default you will get only the root directories of each submodules but none of the contents of the submodule, they always start as empty folders.

To initialize the submodules you have to run these 2 commands.

```
git submodule init
git submodule update

OR just
git submodule update --init # combines to 2 commands into one

```

### Updating the monorepo

Running `git pull` when `git config submodule.recurse true` will automatically init and update each submodule on the monorepo.

```
git pull
git submodule update --init --recursive

OR
git pull --recurse-submodules # this should be the default on git config

OR
git pull # make sure you set git config submodule.recurse
```

### Working with submodules

When you update the submodule git will let it into `detached HEAD` state.
This is because git uses the commit id from manifest and will do a checkout of that commit.
To make changes you need to go into the submodule and checkout a new working branch.

Working with submodules is always a two stages process, publish the submodule then publish the monorepo.

```
cd modules/<module_name>
git checkout -b <working_branch>
git commit -am 'new cool stuff'
git push # create a PR to release or main submodule branch
git checkout <release branch>
git pull
cd ..
git add modules/<module_name>
git commit -am 'new changes and submodule ref adjusted'
git push # create a PR to release or main on monorepo
```

### Running a command on all submodules

You can run the same git command on all submodules by using `git submodule foreach` command.

```

git submodule foreach 'git stash' # run git stash on all submodules
git submoduel foreach 'git checkout -b newBranch' # create a new branch on all submodules

```

### References

1. [Git tools - submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules)
