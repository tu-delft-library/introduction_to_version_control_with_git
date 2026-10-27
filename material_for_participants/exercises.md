
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

## 3 💪 Including Specific Files in `gitignore`

- Navigate to your `bio` repository
- Create three empty `.png` files using `touch a.png b.png final.png` 
- Create and edit a `.gitignore` file with nano
- Add a line to ignore all the `png` files in your repository
- Stage and commit `.gitignore`
- Check the status of all files (including the ignored ones)
- Add a line afterwards to ask Git to track the file `final.png`
- Check the status of all files (including the ignored ones) 

<details>
<summary>🔍 Click here for hints! </summary>

- To open a (new) file for editing use `nano name_of_file`
- Use the wildcard `*.extension` to ignore all the files of type `extension`
- Find out what `!` (the exclamation point operator) does in a `.gitignore` file
- To see the status of all files (including ignored ones) use `git status --ignored`

</details>


### 🚀 Optional challenge `gitignore`: The Order of Rules
- Open `.gitignore` in nano
- Add a new line `!*.png`
- Check that the contents of `.gitignore` look like this
```console
*.png
!final.png
!*.png
```
- Check the status of all files (including the ignored ones)
- Reflect: what is the effect of the last line `!*.png` on the ignore operation?

<details>
<summary>🔍 Click here to see the solution! </summary>

The `!` modifier will negate an entry from a previously defined ignore pattern. Because the `!*.png` entry negates all of the previous `.png` files in the `.gitignore`, none of them will be ignored, and all `.png` files will be tracked.

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


## 4 💪 GitHub GUI 

- Browse to your `free_fall` repository on GitHub.
- Under the Code tab, find and click on the text that says “XX commits” (where “XX” is some number). You should see the history log.
- Click on, the **three buttons** to the right of each commit.
- What information can you gather/explore from these buttons?
- How would you get that same information in the shell? 


## 5 💪 GitHub Timestamps 

- Go to the repo you just created on GitHub and check the timestamps of the files.  
- How does GitHub record times, and why?  
- Hover over the timestamp, you can see the exact time at which the last change to the file occurred. 

