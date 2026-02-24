# Solutions to Optional Exercises

## 1. Committing Multiple Files

First we make our changes to the `guacamole.md` and `groceries.md` files:

```console
$ nano guacamole.md
$ cat guacamole.md
```

```
# Guacamole
## Ingredients
* avocado (1.35)
* lime (0.64)
* salt (2)
```

```console
$ nano groceries.md
$ cat groceries.md
```

```
# Market A
* avocado: 1.35 per unit.
* lime: 0.64 per unit
* salt: 2 per kg
```

Now you can add both files to the staging area. We can do that in one line:

```console
$ git add guacamole.md groceries.md
```
Or with multiple commands:
```console
$ git add guacamole.md
$ git add groceries.md
```
Now the files are ready to commit. You can check that using `git status`. If you are ready to commit use:

```console
$ git commit -m "Write prices for ingredients and their source"
```
```
[main cc127c2]
 Write prices for ingredients and their source
 2 files changed, 7 insertions(+)
 create mode 100644 groceries.md
```

## 2: Getting Rid of Staged Changes
After adding a change, `git restore` can not be used directly. Let’s look at the output of `git status`:

```
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   guacamole.md
```
Note that if you don’t have the same output you may either have forgotten to change the file, or you have added it and committed it.

Using the command git restore `guacamole.md` now does not give an error, but it does not restore the file either. Git helpfully tells us that we need to use `git restore --staged` first to unstage the file:

```console
$ git restore --staged guacamole.md
```
Now, git status gives us:

```console
$ git status
```
```
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git git restore <file>..." to discard changes in working directory)
        modified:   guacamole.md

no changes added to commit (use "git add" and/or "git commit -a")
```
This means we can now use `git restore` to restore the file to the previous commit:

```console
$ git restore guacamole.md
$ git status
```
```
On branch main
nothing to commit, working tree clean
```

## 3: Ignoring all data Files in the repository

In the `.gitignore` file, write:

```
**/*.csv
```
This will ignore all the `.csv` files, regardless of their position in the directory tree. You can still include some specific exception with the exclamation point operator.

## 4: The Order of Rules

The `!` modifier will negate an entry from a previously defined ignore pattern. Because the `!*.csv` entry negates all of the previous `.csv` files in the `.gitignore`, none of them will be ignored, and all `.csv` files will be tracked.
