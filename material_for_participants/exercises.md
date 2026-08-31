
# Exercises


## Vevox 
Fill the interactive poll using this Vevox link: https://vevox.app/181857001

## 1 💪 bio Repository 

- Create a new Git repository on your computer called bio.
    - **tip** remember to step out of your current `recipe` repository
- Write a three-line biography for yourself in a file called `me.txt`, commit your changes
- Modify one line, add a fourth line
- Display the differences between its *modified* state and its original state. 
- Stage the file and display the differences between its *staged* state and its original state.

<details>
<summary>🔍 Click here hints! </summary>

- To create a folder use `mkdir folder_name`
- To initialize a repository, navigate to the folder that you want to turn into a repository and use `git init`
- To open a (new) file for editing use `nano name_of_file`
- To stage file use `git add name_of_file`
- To commit a file use `git commit -m "commit message"`
</details>


## 2 💪 GitHub GUI 

- Browse to your `recipes` repository on GitHub.
- Under the Code tab, find and click on the text that says “XX commits” (where “XX” is some number).
- Hover over, and click on, the **three buttons** to the right of each commit.
- What information can you gather/explore from these buttons?
- How would you get that same information in the shell? 


## 3 💪 GitHub Timestamps 

- Go to the repo you just created on GitHub and check the timestamps of the files.  
- How does GitHub record times, and why?  
- Hover over the timestamp, you can see the exact time at which the last change to the file occurred. 



## 🚀 Optional challenges

These are additional exercises for you to play with 🙂

### Committing Multiple Files
When you make changes, they often belong together as one logical improvement. Git lets you group related edits into a single commit so your project stays consistent. This is something word processors can’t easily do—each suggestion is separate, even if they depend on each other.

The staging area can hold changes from any number of files that you want to commit as a single snapshot.
- Navigate to your recipes repository
- Add some text to `guacamole.md` noting the rough price of the ingredients.
- Create a new file `groceries.md` with a list of products and their prices for different markets.
- Add changes from both files to the staging area and commit those changes.


<details>
<summary>🔍 Click here to see the solution! </summary>

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

</details>

### Getting Rid of Staged Changes
`git restore` can be used to restore a previous commit when unstaged changes have been made, but will it also work for changes that have been staged but not committed? 

Make a change to `guacamole.md`, add that change using `git add`, then use `git restore` to see if you can remove your change.

<details>
<summary>🔍 Click here to see the solution! </summary>

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


</details>

### Ignoring all data Files in the repository
Let us assume you have many `.csv` files in different subdirectories of your repository. For example, you might have:

```console
results/a.csv
data/experiment_1/b.csv
data/experiment_2/c.csv
data/experiment_2/variation_1/d.csv
```
How do you ignore all the `.csv` files, without explicitly listing the names of the corresponding folders?

<details>
<summary>🔍 Click here to see the solution! </summary>

In the `.gitignore` file, write:

```
**/*.csv
```
This will ignore all the `.csv` files, regardless of their position in the directory tree. You can still include some specific exception with the exclamation point operator.

</details>

### The Order of Rules
Given a `.gitignore` file with the following contents:

```console
*.csv
!*.csv
```
What will be the result?

<details>
<summary>🔍 Click here to see the solution! </summary>


The `!` modifier will negate an entry from a previously defined ignore pattern. Because the `!*.csv` entry negates all of the previous `.csv` files in the `.gitignore`, none of them will be ignored, and all `.csv` files will be tracked.

</details>