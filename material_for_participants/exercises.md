
# Exercises


## Vevox 
- Fill the interactive poll using Vevox: https://vevox.app/
- Enter the ID shown by the instructor on the screen

## 1 💪 bio Repository 

- Create a new Git repository on your computer called `bio`.
    - **Remember to step out** of your current `free_fall` repository
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
- To move a file to a different location use `mv source_path target_path`
- To stage file use `git add name_of_file`
- To commit a file use `git commit -m "commit message"`
- To see git history use `git log`
</details>


### 🚀 Optional challenge
When you make changes, they often belong together as one logical improvement. Git lets you group related edits into a single commit so your project stays consistent.

The staging area can hold changes from any number of files that you want to commit as a single snapshot. Let's practice this.

- Navigate to your `bio` repository
- Create a file called `timeline.md`
- Add to it some of your PhD start date (e.g. september 2026)
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
- Inspect the changes in the working directory with `git diff`
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
  (use "git git restore <file>..." to discard changes in working directory)
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


</details>


## 3 💪 Undoing the Latest Commit

Make a mistake on purpose, then undo it safely.

There are two ways to do this. 
1. Hard reset: means deleting the last commit from history. This modifies your commit history as if the commit never happened.
2. Revert: It is like an "undo" operation. It applies the reverse operation from the latest commit (removes what was added, and/or adds what was removed).

### Hard reset:
Imagine you are trying out some ideas and you commit two experiments that you immediately regret. They only exist on your computer (you have not pushed them), so you can erase them completely.

- Navigate to your `free_fall` repository and check that `git status` is clean
- Change `time = 5` to `time = 60` in `distance.py`. Stage the file and commit with the message `Try one minute`
- Change `gravity = 9.81` to `gravity = 24.79` (Jupiter!). Stage the file and commit with the message `Try Jupiter`
- Display the history with `git log --oneline`. You should see your two experiments on top
- Run `python distance.py`. Is this what you want?
- Delete both experiments using a hard reset, going back to the commit you had before them
- Display the history again. Where did the two commits go?
- Check that `distance.py` is back to normal: run `cat distance.py` and `python distance.py` (it should print `After 5 s the free fall distance on Earth is 122.625 m`)
- Run `git status`

> ⚠️ `git reset --hard` also throws away any uncommitted changes in your working directory. Always run `git status` before using it.

Reflections:
- How many commits did you remove? How did you tell Git how far back to go?
- What is the difference between `git restore distance.py` and `git reset --hard HEAD~2`?
- Why is it a bad idea to hard reset commits that you have already pushed to a remote?

<details>
<summary>🔍 Click here for hints! </summary>

- `HEAD~1` is the commit before `HEAD`, `HEAD~2` is two commits before `HEAD`, and so on
- Count how many experiments are on top of your `git log --oneline`: that is the number of steps you need to go back
- To hard reset use `git reset --hard HEAD~N`, replacing `N` with the number of commits you want to remove
</details>

### Reversing:
- Delete the line `distance = 0.5 * gravity * time ** 2` from `distance.py`
- Run `python distance.py` — what happens?
- Stage `distance.py` and commit with the message `oops: accidentally deleted the formula`
- Undo the commit using `git revert --no-edit HEAD`
- Run `python distance.py` again — does it work now?
- View the commit graph for all branches

> Reversing a commit this way is safe when you've already pushed to remote. If you haven't pushed yet, a hard reset to the previous commit removes the commit entirely.

### 🚀 Optional challenge: soft, mixed and hard
`git reset` comes in three flavours: `--soft`, `--mixed` (the default) and `--hard`. They differ in how much they undo. Let's find out how!

- In `distance.py`, change `time = 5` to `time = 10`. Stage the file and commit with the message `Try ten seconds`
- Run `git reset --soft HEAD~1`. Look at `git log --oneline`, `git status` and `git diff --staged`. Where is your change now?
- Stage and commit the change again. Run `git reset --mixed HEAD~1` and look at `git status`. Where is your change now?
- Stage and commit the change once more. Run `git reset --hard HEAD~1` and look at `git status` and `cat distance.py`. Where is your change now?

For each flavour, answer: is the commit removed from the history? Are the changes still in the staging area? Are the changes still in the working directory?

<details>
<summary>🔍 Click here to see the solution! </summary>

| Flavour | Commit removed from history | Changes in staging area | Changes in working directory |
|---|---|---|---|
| `--soft` | yes | kept (staged) | kept |
| `--mixed` (default) | yes | removed (unstaged) | kept |
| `--hard` | yes | removed | removed ⚠️ |

If you want to redo the commit differently (e.g. with a better message or fewer files), `--soft` or `--mixed` are the safer options. Use `--hard` only when you really want to throw the changes away.

Even `--hard` is not completely final: `git reflog` lists the places where `HEAD` has been recently, including the commits you "deleted". For a while you can still go back to one of them with `git reset --hard [hash]`.
</details>


## 4 💪 Amending history

Sometimes you notice a small mistake right after committing: a sloppy commit message, or a file you forgot to add. If you have not pushed yet, you can fix the latest commit with `git commit --amend` instead of making a new commit.

- Navigate to your `bio` repository
- Add a line to `me.md`: `My favourite food is [your favourite food]`
- Stage the file and commit it with the vague message `wip` (work in progress)
- Display the history with `git log --oneline`. Note the hash of your last commit
- Replace the message of the last commit with something descriptive, e.g. `Add favourite food`. Do not make a new commit
- Display the history again. How many commits are there? Did the hash change?
- Create a new file `recipes.md` with one line about how to prepare your favourite food
- Stage `recipes.md` and add it to the last commit, keeping the same message
- Run `git log --oneline` and `git show --stat`. Is `recipes.md` part of the same commit as the new line in `me.md`?

Reflections:
- Why did the hash of the commit change after amending?
- Why shouldn't you amend a commit that you have already pushed?

<details>
<summary>🔍 Click here for hints! </summary>

- To replace the message of the latest commit (with nothing staged) use `git commit --amend -m "new message"`
- To add changes to the latest commit, first stage them with `git add`, then run `git commit --amend`
- Add the flag `--no-edit` to keep the existing commit message. If you use neither `-m` nor `--no-edit`, Git opens nano so you can edit the message
- `git show --stat` lists the files changed in the latest commit
</details>


### 🚀 Optional challenge: Which tool should I use?
You now know three ways to modify history: `reset`, `revert` and `amend`. For each situation, decide which one you would use:

1. You made a typo in the message of your latest commit. You have not pushed it.
2. You pushed a commit yesterday and your teammates have already pulled it. Today you discover that it contains a bug.
3. You accidentally committed a debugging `print` (and nothing else) and you have not pushed it. You want it gone completely.
4. You just committed, but forgot to include a file that belongs in this commit. You have not pushed it.
5. A commit from three weeks ago, already pushed, introduced a bug.

<details>
<summary>🔍 Click here to see the solution! </summary>

1. **amend**: `git commit --amend -m "corrected message"`
2. **revert**: others already have the commit, so do not rewrite history. `git revert [hash]` adds a new commit that undoes it
3. **reset**: `git reset --hard HEAD~1` removes the commit entirely
4. **amend**: stage the file and run `git commit --amend --no-edit`
5. **revert**: `git revert [hash]` also works for commits that are not the latest one

Rule of thumb: if the commit only exists on your computer you can rewrite history (`reset`, `amend`). If it is already on the remote, use `revert`.
</details>


## 5 💪 Including Specific Files in `gitignore`

- Navigate to your `bio` repository
- Create three empty `.png` files using `touch a.png b.png final.png` 
- Create and edit a `.gitignore` file with nano
- Add a line to ignore all the `png` files in your repository
- Stage and commit `.gitignore`
- Check the status of all files (including the ignored ones)
- Open `.gitignore` in nano
- Add a line afterwards to ask Git to track the file `final.png`
- Check the status of all files (including the ignored ones) 
  - Note that the file `final.png` is listed under `Untracked files`
- Add a new line `!*.png`
- Check that the contents of `.gitignore` look like this
  ```console
  *.png
  !final.png
  !*.png
  ```
- Check the status of all files (including the ignored ones)
  - Note that all `png` files are now listed under `Untracked files`
- Reflect: what is the effect of the last line `!*.png` on the ignore operation?

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