# PRACTICAL -  Putting it all together

## Setup
Work in a new folder for this exercise — don't reuse `recipe` or `bio` from earlier
For example, navigate to your `Desktop` and start from there

## Start the repository right 

- Create a folder called `weather-notes` 
- Turn it into a Git repo
- Create `README.md` file using `nano`. Use the template below:
   
   ```
   # Weather notes

   One sentence on what this project is

   ## Usage

   Empty for now
   ```
- Create a `LICENSE` file using `nano`
   - pick any open license text from https://choosealicense.com and paste it in. 
   - Inside `nano` replace:
      - `[year]` with the current year 
      - `[fullname]` with `Technische Universiteit Delft`
- Stage and commit both files together with the message `Initial commit: add README and LICENSE`


> **Why now, not later?** A repo without a license is technically "all rights reserved" — nobody else can legally reuse your code, even if it's public. Starting with README + LICENSE should become a habit :)

<details>
<summary>🔍 Click here hints! </summary>

- To create a folder use `mkdir folder_name`
- To initialize a repository, navigate to the folder that you want to turn into a repository and use `git init`
- To open a (new) file for editing use `nano name_of_file`
- To stage file use `git add name_of_file`
- To commit a file use `git commit -m "commit message"`
</details>



## Working directory → staging → history
- Create `notes.txt` with three lines describing this week's weather
- Check `status`, then stage and commit it (`Add first weather notes`)
- Add a fourth line to `notes.txt`
- Run `diff` to see the *unstaged* changes
- Stage the file
- Run `diff` again — notice it shows nothing (all staged changes are compared differently — use `diff --staged`)
- Commit with a descriptive message
- Add a fifth line to `notes.txt`
- Run `diff` to see the *unstaged* changes
- Stage and commit with a descriptive message

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
- Look at your history with `log --oneline` and note the commit hashes
- Use `show HEAD~1` to view the previous commit's version of `notes.txt`
- Deliberately break the file: delete two lines and save
- Run `diff` to see the *unstaged* changes
- Use `restore` to bring back the last **committed** version (discard your uncommitted edit)
- Now go back further: check out `notes.txt` as it existed at `HEAD~2` into your working directory, look at it, then restore back to the latest version so you don't lose work

<details>
<summary>🔍 Click here hints! </summary>

- To restore a file to the latest commit use `git restore name_of_file`
- To restore a file to a SPECIFIC commit use `git restore -s HEAD~[#] name_of_file` or `git restore -s [hash] name_of_file`
</details>

## Keep it clean 

- Create a new file `debug.log` 
- Make a new directory named `data`
- Inside the folder `data` add two files: `raw_dump.csv` and `README.md`
- Add a `.gitignore` that ignores `*.log` and everything in `data/`, **except** `data/README.md`
- Confirm with `status` that the log and csv are ignored but `data/README.md` shows up as untracked
- Stage and commit the `.gitignore` file
- Stage and commit the `data/README.md` file

<details>
<summary>🔍 Click here hints! </summary>

- To create a file without nano use `touch name_of_file`
- To create a new folder use `mkdir name_of_folder`
- To add an exception in `.gitignore` use `!` in front of the file name you want to track
- To check the status of the local git repo use `git status`
</details>

## Remote, push, and the "lost laptop" scenario
- Create a new empty repository on GitHub (no README/license — you already have those).
- Connect your local repo to it and push all your commits.
- Refresh the GitHub page and confirm every file and all commits made it across.
- **Simulate disaster:** rename your local `weather-notes` folder to `weather-notes-OLD` (don't delete it yet, just in case).
- Clone the repo fresh from GitHub into a new `weather-notes` folder.
- Verify: does the clone have your full commit history (`log --oneline`)? Does it have the README, LICENSE, and `.gitignore`?

**Ask yourself:** what files are there in `weather-notes-OLD` but not in `weather-notes`. What would you have lost if you had never pushed?


<details>
<summary>🔍 Click here hints! </summary>

- To add a remote repository to an existing local repository use `git remote add origin git@github.com:[USERNAME]/[RESPOSITORY].git`
- To push to a remote repository use `git push origin main`
- To rename a local folder use `mv source_directory target_directory`
- To clone a repository from GitHub use `git clone git@github.com:[USERNAME]/[RESPOSITORY].git`
</details>

## Wrap-up — Peer FAIR review
Pair up with your neighbor and swap GitHub repo links. You are now a "future collaborator" who has just stumbled onto your partner's repo and needs to reuse it — you get **2 minutes** to review their repo before switching roles.

Reviewer fills this in about your **partner's** repo (not your own):

| FAIR principle | Question | Partner's repo? |
|---|---|---|
| Findable | Would someone searching for "weather notes analysis" ever find this? | |
| Accessible | Is it actually public / shared somewhere? | |
| Interoperable | Does the README say what format the data is in? | |
| Reusable | Is there a LICENSE telling others what they're allowed to do with it? | |

Then tell your partner, **one thing you'd need them to fix or clarify** before you could reuse their repo yourself. Switch roles and repeat.



