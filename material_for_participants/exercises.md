
# Exercises


## Vevox 
- Fill the interactive poll using Vevox: https://vevox.app/
- Enter the ID shown by the instructor on the screen

## 1 💪 bio Repository 

- Create a new Git repository on your `Desktop` called `bio`.
    - **Remember to step out** of your current `free_fall` repository
    - We recommend to make the new repository on your `Desktop`
- Write a three-line biography for yourself in a file called `me.md`, commit your changes
- Add a fourth line (e.g. your field of research or a hobby)
- Display the differences between its *modified* state and its original state. 
- Stage the file and display the differences between its *staged* state and its original state.
- Commit your changes
- Display the git history

<details>
<summary>🔍 Click here for hints! </summary>

- Use `cd ..` to navigate to the parent directory. This should bring you to your `Desktop`
- To create a folder use `mkdir folder_name`
- To initialize a repository, navigate to the folder that you want to turn into a repository and use `git init`
- To open a (new) file for editing use `nano name_of_file`
- To stage file use `git add name_of_file`
- To commit a file use `git commit -m "commit message"`
- To see git history use `git log`
</details>


### 🚀 Optional challenge
When you make changes, they often belong together as one logical improvement. Git lets you group related edits into a single commit so your project stays consistent.

The staging area can hold changes from any number of files that you want to commit as a single snapshot. Let's practice this.

- Navigate to your `bio` repository
- Create a file called `timeline.md`
- Add in `timeline.md` your PhD start date (e.g. september 2026)
- Modify `me.md` with a line `I am a [first/second/third] year PhD student`. Replace the text between `[]` accordingly.
- Since the new line in biography and the timeline are related, commit the changes in a single commit. Do this by adding both files to the staging area BEFORE running the commit command.


<details>
<summary>🔍 Click here for hints!  </summary>


- To staged multiple files, you execute `git add file` multiple times and the changes will be accumulated in the staging area
- Alternatively, add multiple files at the same time using `git add one_file another_file yet_another_file`
</details>

## 2 💪 Workflow and `history`

- Navigate to your `bio` repository
- Open `me.md` in nano 
- Add a new line `I like ketchup`
- Execute `git add me.md`
- Open `me.md` in nano
- Add a new a line `Ketchup enhances pasta`
- Execute `git commit -m "My opinions about red sauce"`
- Look at the contents of `me.md` (e.g. run `cat me.md`)
- Inspect the changes in the working tree with `git diff`
- Execute `git restore me.md`
- Look at the contents of `me.md` (e.g. run `cat me.md`)

Reflections:
- Is the second change `Ketchup enhances pasta` applied to the working copy or the version in the staging area?
- What is committed when you executed `git commit -m "My opinions about red sauce"`?
- What happened when you executed `git restore me.md`?
- What happened to the line `Ketchup enhances pasta`?


### 🚀 Optional challenge: Getting Rid of Staged Changes
`git restore` can be used to restore a previous commit when unstaged changes have been made, but will it also work for changes that have been staged but not committed? 

Make a change to `me.md`, add that change using `git add`, then use `git restore` to see if you can remove your change.

<details>
<summary>🔍 Click here to see the solution! </summary>

After adding a change, `git restore` can not be used directly. Let’s look at the output of `git status`:

```
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   me.md
```
Note that if you don’t have the same output you may either have forgotten to change the file, or you have added it and committed it.

Using the command git restore `me.md` now does not give an error, but it does not restore the file either. Git helpfully tells us that we need to use `git restore --staged` first to unstage the file:

```console
$ git restore --staged me.md
```
Now, git status gives us:

```console
$ git status
```
```
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git git restore <file>..." to discard changes in working tree)
        modified:   me.md

no changes added to commit (use "git add" and/or "git commit -a")
```
This means we can now use `git restore` to restore the file to the previous commit:

```console
$ git restore me.md
$ git status
```
```
On branch main
nothing to commit, working tree clean
```
```console
$ cat me.md
```
The latest modification is gone

</details>


## 3 💪 Undoing the Latest Commit

- Navigate to your `bio` repository
- Open `me.md`
- Change the line `I like ketchup` with `I like [your favorite sauce]` (replace inside square brackets)
- Look at the contents of `me.md` (e.g. run `cat me.md`)
- Stage the file and commit with the message `My favorite sauce`
- Open `me.md` and add a new line `I prefer [coffee/tea]` (choose coffee or tea and remove the square brackets)
- Look at the contents of `me.md` (e.g. run `cat me.md`)
- Stage the file and commit with the message `My warm drink preference`
- Check the status of git (to ensure all local changes are committed)
- Display the git history
- Imagine you decide to delete the last two bits of personal information from git history. 
  - Completely delete the last two commits using a hard reset
- Display the history again. What happened to the lats two commits?
- Check that `me.md` looks similar to this (assuming you finished exercises 1 and 2):
```
My name is [name]
I come from [country]
I love to [hobby]
I have a [field] background
[optional] I am a first year PhD student
I like ketchup
```
- Run `git status`

<details>
<summary>🔍 Click here for hints! </summary>

- To hard reset use `git reset --hard HEAD~N`, replacing `N` with the number of commits you want to remove
</details>


### 🚀 Optional challenge: soft, mixed and hard
`git reset` comes in three flavours: `--soft`, `--mixed` (the default) and `--hard`. They differ in how much they undo. 

For each flavour, answer: is the commit removed from the history? Are the changes still in the staging area? Are the changes still in the working tree?

- In `me.md`, change the second line
- Stage the file and commit
- Display the git history
- Run `git reset --soft HEAD~1`
- Look at `git log --oneline`, `git status` and `git diff --staged`. Where is your change now?
- Commit the change again 
- Run `git reset --mixed HEAD~1` and look at `git status`. Where is your change now?
- Stage and commit the change once more 
- Run `git reset --hard HEAD~1` and look at `git status` and `cat me.md`. Where is your change now?



<details>
<summary>🔍 Click here to see the solution! </summary>

| Flavour | Commit removed from history | Changes in staging area | Changes in working tree |
|---|---|---|---|
| `--soft` | yes | kept (staged) | kept |
| `--mixed` (default) | yes | removed (unstaged) | kept |
| `--hard` | yes | removed | removed ⚠️ |

If you want to redo the commit differently (e.g. with a better message or fewer files), `--soft` or `--mixed` are the safer options. Use `--hard` only when you really want to throw the changes away.

</details>


## 4 💪 Amending history

- Navigate to your `bio` repository
- Add a line to `me.md`: `My favorite food is [your favourite food]`
- Stage the file and commit it with the vague message `wip` (work in progress)
- Display the git history. Note the hash of your last commit
- Replace the message of the last commit with something descriptive, e.g. `Add favorite food`. Do not make a new commit
- Display the history again. How many commits are there? Did the hash change?
- Create a new file `recipes.md` with one line about how to prepare your favorite food
- Stage `recipes.md` and add it to the last commit, keeping **the same message**
- Display the history again
- Run `git show --stat` to see the changes added to the last commit. Is `recipes.md` part of the same commit as the new line in `me.md`?


<details>
<summary>🔍 Click here for hints! </summary>

- To replace the message of the latest commit (with nothing staged) use `git commit --amend -m "new message"`
- To add changes to the latest commit, first stage them with `git add`, then run `git commit --amend`
- Add the flag `--no-edit` to keep the existing commit message. If you use neither `-m` nor `--no-edit`, Git opens nano so you can edit the message
- `git show --stat` lists the files changed in the latest commit
</details>



## 5 💪 Including Specific Files in `gitignore`

- Navigate to your `bio` repository
- Create three empty `.pdf` files using `touch a.pdf b.pdf final.pdf` 
- Create and edit a `.gitignore` file with nano
- Add a line to ignore all the `pdf` files in your repository
- Stage and commit `.gitignore`
- Check the status of all files (including the ignored ones)
- Open `.gitignore` in nano
- Add a line afterwards to ask Git to track the file `final.pdf`
- Check the status of all files (including the ignored ones) 
  - Note that the file `final.pdf` is listed under `Untracked files`
- Add a new line `!*.pdf`
- Check that the contents of `.gitignore` look like this
  ```console
  *.pdf
  !final.pdf
  !*.pdf
  ```
- Check the status of all files (including the ignored ones)
  - Note that all `pdf` files are now listed under `Untracked files`
- Reflect: what is the effect of the last line `!*.pdf` on the ignore operation?

<details>
<summary>🔍 Click here for hints! </summary>

- Use the wildcard `*.extension` to ignore all the files of type `extension`
- Find out what `!` (the exclamation point operator) does in a `.gitignore` file
- To see the status of all files (including ignored ones) use `git status --ignored`

</details>


### 🚀 Optional challenge `gitignore`:  Ignoring all data Files in the repository
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


## 6 💪 GitHub GUI 

- Browse to your `free_fall` repository on GitHub.
- Under the Code tab, find and click on the text that says “XX commits” (where “XX” is some number). You should see the history log.
- Click on, the **three buttons** to the right of each commit.
- What information can you gather/explore from these buttons?
- How would you get that same information in the shell? 


## 7 💪 GitHub Timestamps 

- Go to the repo you just created on GitHub and check the timestamps of the files.  
- How does GitHub record times, and why?  
- Hover over the timestamp, you can see the exact time at which the last change to the file occurred. 