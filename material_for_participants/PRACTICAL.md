# PRACTICAL -  Putting it all together

TODO add hints

## Setup
Work in a new folder for this exercise — don't reuse `recipe` or `bio` from earlier.
For example, navigate to your `Desktop` and start from there.

## Start the repository right 

1. Create a folder called `weather-notes` 
1. Turn it into a Git repo
1. Before writing any code create two files: `README.md` and `LICENSE`
   - for the `README.md`, use the template below
   
   ```
   # Weather notes

   One sentence on what this project is

   ## Usage

   Empty for now


   ## Copyright

   Copyright (c) 2026, Technische Universiteit Delft

   ```
   - for the `LICENSE` file, pick any open license text (e.g. MIT) from https://choosealicense.com and paste it in

1. Stage and commit both files together with the message `Initial commit: add README and LICENSE`.

> **Why now, not later?** A repo without a license is technically "all rights reserved" — nobody else can legally reuse your code, even if it's public. Starting with README + LICENSE should become a habit :)


## Working directory → staging → history
1. Create `notes.txt` with three lines describing this week's weather.
1. Check `status`, then stage and commit it (`Add first weather notes`).
1. Add a fourth line to `notes.txt`.
1. Run `diff` to see the *unstaged* changes.
1. Stage the file, then run `diff` again — notice it shows nothing (all staged changes are compared differently — use `diff --staged`).
1. Commit with a descriptive message.
1. Add a fifth line to `notes.txt`.
1. Run `diff` to see the *unstaged* changes.
1. Stage and commit with a descriptive message.

You should now have 4 commits. Run `log --oneline` to confirm.

## Time travel: restoring old versions
1. Look at your history with `log --oneline` and note the commit hashes.
1. Use `show HEAD~1` to view the previous commit's version of `notes.txt`.
1. Deliberately break the file: delete two lines and save.
1. Run `diff` to see the *unstaged* changes.
1. Use `restore` to bring back the last **committed** version (discard your uncommitted edit).
1. Now go back further: check out `notes.txt` as it existed at `HEAD~2` into your working directory, look at it, then restore back to the latest version so you don't lose work.

TODO continue here

## Keep it clean 

1. Create two junk files: `debug.log` and `data/raw_dump.csv` (make the `data/` folder).
1. Add a `.gitignore` that ignores `*.log` and everything in `data/`, **except** `data/README.md` (create that small file too, and make sure the ignore rule doesn't hide it — use `!`).
1. Confirm with `status` that the log and csv are ignored but `data/README.md` shows up as untracked.
1. Stage and commit the `.gitignore` and `data/README.md`.

## Remote, push, and the "lost laptop" scenario
1. Create a new empty repository on GitHub (no README/license — you already have those).
1. Connect your local repo to it and push all your commits.
1. Refresh the GitHub page and confirm every file and all commits made it across.
1. **Simulate disaster:** rename your local `weather-notes` folder to `weather-notes-OLD` (don't delete it yet, just in case).
1. Clone the repo fresh from GitHub into a new `weather-notes` folder.
1. Verify: does the clone have your full commit history (`log --oneline`)? Does it have the README, LICENSE, and `.gitignore`?

**Ask yourself:** what would you have lost if you had never pushed?

## Wrap-up — Peer FAIR review
Pair up with your neighbor and swap GitHub repo links. You are now a "future collaborator" who has just stumbled onto your partner's repo and needs to reuse it — you get **2 minutes** to review their repo before switching roles.

Reviewer fills this in about your **partner's** repo (not your own):

| FAIR principle | Question | Partner's repo? |
|---|---|---|
| Findable | Would someone searching for "weather notes analysis" ever find this? | |
| Accessible | Is it actually public / shared somewhere? | |
| Interoperable | Does the README say what format the data is in? | |
| Reusable | Is there a LICENSE telling others what they're allowed to do with it? | |

Then tell your partner, out loud, **one thing you'd need them to fix or clarify** before you could reuse their repo yourself. Switch roles and repeat.


## Optional challenges
- Add a `CITATION.cff` file so your repo can be cited properly
- Look up the TU Delft Research Software Guidelines and check one recommendation against your repo
- Try `git log --oneline --graph --all` and see if you can explain the output to a neighbor

