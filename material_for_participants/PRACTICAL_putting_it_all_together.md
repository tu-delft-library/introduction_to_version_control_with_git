# PRACTICAL -  Putting it all together

## Setup
Work in a new folder for this exercise — don't reuse `recipe` or `bio` from earlier
For example, navigate to your `Desktop` and start from there

## Start the repository right 

- Create a folder called `weather-notes` 
- Navigate inside this new directory
- Turn it into a Git repo
- Create `README.md` file using `nano`. Use the template below:
   
   ```
   # Weather notes
   One sentence on what this project is

   ## Usage
   Empty for now
   ```
- Create a `LICENSE` file using `nano`
   - Pick any open license text from https://choosealicense.com and paste it in. 
   - Inside `nano` replace the copyright line with one of these three options. Fill the information between `[]` accordingly.
      1. If software is patented or commercialized: `Copyright (c) [YEAR] Technische Universiteit Delft`
      1. If software is not patented nor commercialized, TU Delft will waive the copyright to authors as long as it is published under open-source license: `Copyright (c) [YEAR] [AUTHOR(S)], Delft, the Netherlands`
      1. If software is kept as in-house development, share with collaborators under proprietary license or agreement only:
      `Copyright (c) [YEAR] Technische Universiteit Delft, [NON-EMPLOYEES], Delft, the Netherlands`


- Stage and commit both files together with the message `Initial commit: add README and LICENSE`


> **Why now, not later?** A repo without a license is technically "all rights reserved" — nobody else can legally reuse your code, even if it's public. Starting with README + LICENSE should become a habit :)

<details>
<summary>🔍 Click here hints! </summary>

- To create a folder use `mkdir folder_name`
- To initialize a repository, navigate to the folder that you want to turn into a repository and use `git init`
- To open a (new) file for editing use `nano name_of_file`
- To stage file use `git add name_of_file`
- To stage multiple files use `git add name_of_file name_of_another_file`
- To commit a file use `git commit -m "commit message"`
</details>



## Working directory → staging → history
- Create `notes.txt` in `nano` and add one line describing this week's weather
```
The sun came out
```
- Check `status`, then stage and commit it with the message `Add first line`
- Open `notes.txt` in `nano` and add a second line to `notes.txt`
```
The air was fresh
```
- Run `diff` to see the *unstaged* changes
- Stage the file
- Run `diff` again — notice it shows nothing (all staged changes are compared differently — use `diff --staged`)
- Commit with the message `Add second line`
- Open `notes.txt` in `nano` and add a third line to `notes.txt`
```
A cloudy afternoon
```
- Run `diff` to see the *unstaged* changes
- Stage and commit with the message `Add third line`

You should now have 4 commits. Run `log --oneline` to confirm.


<details>
<summary>🔍 Click here hints! </summary>

- To open a (new) file for editing use `nano name_of_file`
- To check the status of the git repository use `git status`
- To stage file use `git add name_of_file`
- To commit a file use `git commit -m "commit message"`
- To see the changes in a file use `git diff name_of_file`
</details>

## Time travel: restoring old versions
- Look at your history with `log --oneline`
- Use `show HEAD~1` to view the previous commit's version of `notes.txt`
- Deliberately break the file: Open in nano, delete one line and save
- Run `diff` to see the *unstaged* changes
- Use `restore` to bring back the last **committed** version (discard your uncommitted edit)
- See the contents of the file with `cat notes.txt` to confirm the file is restored
- Now go back further: check out `notes.txt` as it existed at `HEAD~2` into your working directory
- Run `diff` to see the *unstaged* changes
- Restore back to the latest version so you don't lose work
- See the contents of the file with `cat notes.txt` to confirm the file is restored

<details>
<summary>🔍 Click here hints! </summary>

- To restore a file to the latest commit use `git restore name_of_file`
- To restore a file to a SPECIFIC commit use `git restore -s HEAD~[#] name_of_file` or `git restore -s [hash] name_of_file`
</details>

## Keep it clean 

- Create a new empty file named `debug.log` 
- Make a new directory named `data`
- Inside the directory `data` add two files: `raw_dump.csv` and `temperatures.csv`
- Create a file named `.gitignore` with nano 
- Add a rule inside `.gitignore` to ignore all `log` files 
- Add a rule inside `.gitignore` to ignore everything inside `data/`
- Confirm with `status` that the log and csv files are ignored 
- Stage and commit the `.gitignore` file with the message `Ignore all log and data files`

<details>
<summary>🔍 Click here hints! </summary>

- To create an empty file use `touch name_of_file`
- To create a new folder use `mkdir name_of_folder`
- Use the wildcard `*.extension` to indicate all files with a specific extension (e.g. csv, log, png, pdf)
- Use wildcard `name_of_directory/` to indicate all files inside a directory
- To check the status of the local git repo use `git status`
</details>

## Remote, push, and the "lost laptop" scenario
- Create a new empty repository on GitHub (no README/license — you already have those).
- Connect your local repo to it and push all your commits.
- Refresh the GitHub page and confirm every file and all commits made it across.
- **Simulate disaster:** 
   - Navigate to your `Desktop` (parent directory of the folder `weather-notes`)
   - Rename the `weather-notes` folder to `weather-notes-old` (don't delete it yet).
- Clone the repo fresh from GitHub into a new `weather-notes` folder.
- Verify: does the clone have your full commit history (`log --oneline`)? Does it have the README, LICENSE, and `.gitignore`?

- **Ask yourself:** 
   - What files are there in `weather-notes-old` but not in `weather-notes`? 
   - What would you have lost if you had never pushed?
- Once you confirm the cloning was successful, delete `weather-notes-old`


<details>
<summary>🔍 Click here hints! </summary>

- To add a remote repository to an existing local repository use `git remote add origin git@github.com:[USERNAME]/[REPOSITORY].git`
- To push to a remote repository use `git push origin main`
- To navigate one level up use `cd ..`
- To rename a local folder use `mv source_directory target_directory`
- To clone a repository from GitHub use `git clone git@github.com:[USERNAME]/[REPOSITORY].git`
- To delete a directory and everything it contains use `rm -rf directory_path`
</details>


---

<details>
<summary> ⚠️Solution⚠️ </summary>

If for some reason, creating the repository got messy and confusing, you can create a new repository from scratch to be used on our next workshop.

Navigate to your `Desktop`

Copy and paste the commands below in your terminal

```
mkdir weather-notes
cd weather-notes/
git init
touch README.md
touch LICENSE
git add README.md LICENSE 
git commit -m "Initial commit: add README and LICENSE"
echo "The sun came out" > notes.txt 
git add notes.txt 
git commit -m "Add first line"
echo "The air was fresh" >> notes.txt  
git add notes.txt 
git commit -m "Add second line"
echo "A cloudy afternoon" >> notes.txt 
git add notes.txt 
git commit -m "Add third line"
touch debug.log
mkdir data
touch data/raw_dump.csv
touch data/temperatures.csv
echo "*.log" > .gitignore
echo "data/*" >> .gitignore
git add .gitignore
git commit -m "Ignore all log and data files"
```
This should generate a local repository with a commit history. But you still need to add the remote repository:

- Create a new empty repository on GitHub (no README/license — you already have those).
- Connect your local repo to it and push all your commits.
```
git remote add origin git@github.com:<your-user-name>/weather-notes.git
```
Replace `<your-user-name>` with your GitHub user name
```
git remote -v
git push origin main
```
- Refresh the GitHub page and confirm every file and all commits made it across.
</details>