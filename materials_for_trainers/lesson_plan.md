## Land - 10'
☕ Coffee/tea 🫖

## Installation check, housekeeping - 15'
- ✅ Roll call + 🤝 Code of Conduct
- 🖥 Did everyone:
    - install git
    - install VSCode
    - create a GitHub account
- 🙋 Getting help (🆘 red  ✅ green stickers)

## Icebreaker - 5'
A short icebreaker from [resources document](https://tud365.sharepoint.com/:w:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/resources.docx?d=waea671d7fc6a46d5b5c068fc19f41940&csf=1&web=1&e=f2QYgy)


## Introduction to version control - 10'
- 🎦 introduce git using [slides](https://tud365.sharepoint.com/:p:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/Introduction%20to%20version%20control%20with%20Git.pptx?d=w582c916207804aac981699323fe83c38&csf=1&web=1&e=c4zb1b) 
- What is version control and why should I use it?
  - Do it for your future self
  - your computer is dead. Your code lives on!
- How does git work -> `changesets` or `snapshots`
- What is a git repo: 
    - folder with files + subfolders + `.git` hidden folder

## Preparing Your Working Directory - 5'
- Users with Windows 10 will probably save the data in `OneDrive` Desktop.  
    - First make a symbolic link to make our lives easier.
    - `ln -s "/c/Users/[username]/OneDrive\ -\ Delft\ University\ of\ Technology\Desktop" "Desktop"`

## Setting up git - 5'
Important to mention:
- End of a line:
    - Windows: Uses CRLF (\r\n) to mark the end of a line. 
    - Unix/Linux/macOS: Uses LF (\n).
- Git uses branches. 
    - We work on the main branch and no more details for now.

### Live coding
```
git version
git help
git config --list
git config --global user.name "Name Lastname"
git config --global user.email "netid@tudelft.nl"
git config --global core.editor nano
git config --global core.autocrlf input
git config --global init.defaultBranch main
git config --list --global
```

## Initialize a local Git repository
- `git init` initializes a repository
- Git stores all of its repository data in the `.git` directory

### Live coding - 10'
```
cd Desktop
mkdir recipes   # create a new directory for repository
cd recipes/     # change to new directory to initialize git repo
ls              # show directory is empty
ls -a           # show directory has no hidden folders
git init        # initialize git repo
ls              # appears as if nothing has changed
ls -a           # but hidden item .git was created
ls -aF          # .git is a special subfolder. DO NOT TOUCH THIS
ls .git         # some files and subfolders inside .git
```

### Challenge `init` - 5'
- Go to [TuDelft Vevox](https://tudelft.vevox.com/#/meetings)
- Vevox question 1
- Start poll -> wait for answers -> discuss -> next question

## Perform multiple “add → commit” cycles
- Commands: `status, add, commit, log, diff`
- Important: 
    - We will work with a text file in this course. It will work the same with code. 
    - Code is a text file that is *interpreted* by another program (e.g. python)

### Live coding - 20'
```
cd ~/Desktop/recipes        # ensure inside recipes dir
ls                          # dir is empty
git status                  # status of project
nano guacamole.md           # add headers
                            # explain headers in .md
    # Guacamole
    ## Ingredients
    ## Instructions
ls                          # confirm file created                          
cat guacamole.md            # see content of file 
git status                  # shows untracked file
git add guacamole.md        # please track this file
git status                  # new file but not committed
git commit -m "Create initial structure for a guacamole recipe" 
                            # -m flag + good commit messages: "this commit will..."
git status                  # up to date
git log                     # project history in reverse chronological order
                            # explain hash
ls
nano guacamole.md           # add ingredients
                            # explain lists in .md
    # Guacamole
    ## Ingredients
    * avocado       
    * lemon
    * salt
    ## Instructions
cat guacamole.md            # see content of file 
git status                  # “no changes added to commit”
git diff                    # review changes. Explain the output
git commit -m "Add ingredients to guacamole recipe" # no staged changes
git add guacamole.md        # explain stating area: like framing for a photo
git commit -m "Add ingredients to guacamole recipe"
git log
```
### 💪 Challenge `changes` - 5'
- Continue with the same vevox
- Vevox question 2
- Start poll -> wait for answers -> discuss -> next question

## Break - 15'
## Working directory and staging area
- Working directory -> staging area -> commit history (database)
- Useful ANALOGIES: 
    - Mailing a letter:
        - Staging is like putting letter in envelop
        - Committing is like putting it in the mailbox

    - Photo group analogy:
        - `git add` specifies what will go in a snapshot 
        - `git commit` then actually takes the snapshot
        - `git commit -a` is like gathering everyone to take a group photo

### Live coding - 10'
```
git status
nano guacamole.md           # change lemon for lime
    # Guacamole
    ## Ingredients
    * avocado       
    * lime
    * salt
    ## Instructions
git diff                    # replaced one line - with new line +
git add guacamole.md
git diff                    # no output        
git diff --staged           # changes in staging area
git status
git commit -m "Modify guacamole to traditional recipe"
git status
git log
```
### 💪 Challenge `staging` - 10'
`bio Repository` challenge explained in collaborative document
- Create a new Git repository on your computer called bio.
- Write a three-line biography for yourself in a file called me.txt, commit your changes
- Modify one line, add a fourth line
- Display the differences between its updated state and its original state. 

## git HEAD/TAG game - 15'
- Game explained in [resources document](https://tud365.sharepoint.com/:w:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/resources.docx?d=waea671d7fc6a46d5b5c068fc19f41940&csf=1&web=1&e=f2QYgy)

## Git history
- Commands: `HEAD, HEAD~1, HEAD~2, log --oneline, show, restore`
- HEAD is the *most recent commit*

### Live coding - 25'
```
git status
git log --oneline                   # summarized view
nano guacamole.md                   # add line below instructions
    # Guacamole
    ## Ingredients
    * avocado
    * lime
    * salt
    ## Instructions
    An ill-considered change
git diff HEAD guacamole.md          # diff of current file and most recent commit
git diff guacamole.md               # HEAD is default option for git diff
git diff HEAD~1 guacamole.md        # one commit before HEAD
git diff HEAD~2 guacamole.md        # two commits before HEAD
git show HEAD~2 guacamole.md        # shows changes made on that commit (rather than differences)
git diff [long_hash] guacamole.md   # another way to reference a commit
git log --oneline                   # shows short hashes
git diff [short_hash] guacamole.md  # use short hash to point to a specific commit  
git status                          # shows modified file
git log --oneline
git restore -s [short_hash] guacamole.md # -s for source
cat guacamole.md                    # restored file
git status                          # restored file is not staged!
git restore guacamole.md            # overwrites working copy with last committed version
git status
cat guacamole.md                       
```
## Break - 15'

### 💪 Challenges `history` - 10'
- Continue with the same vevox
- Vevox question 3 and 4
- Start poll -> wait for answers -> discuss -> next question


## Git ignore
Emphasize importance of `.ignore` file to keep repository clean.

### Live coding - 10'
```
git status                          # always check the status of git
ls                                  # what is inside this directory
mkdir pictures                      # make new directory
touch a.png b.png c.png pictures/cake1.jpg pictures/cake2.jpg   # make dummy pictures
ls                                  # lists generated pictures
ls pictures                         # lists generated pictures inside folder
git status                          # images not recommended in git + distracting 
nano .gitignore                     # type lines below
        *.png
        pictures/
cat .gitignore                      # confirm content of .gitignore
git status                          # no pictures but yes new .gitignore file
git add .gitignore                  # let's track this file
git commit -m "Ignore png files and the pictures folder"
git status                          # all clean
ls                                  # files are in folder but not tracked by git
git add a.png                       # if accidentally added, shows warning
git status --ignored                # status of ignored files

```
### 💪 Challenges `ignore` - 10'
- Continue with the same vevox
- Vevox question 5 and 6
- Start poll -> wait for answers -> discuss -> next question

## Lunch break - 60'

## Remote repository

### SSH key - 20'

- Log into GitHub
- Create Secure Shell Protocol (SSH) key
    - SSH key in GitHub is paired to key in your computer
```
ls -al ~/.ssh                   # possible keys id_ed25519/id_ed25519.pub
ssh-keygen -t ed25519 -C "email_used_in_github@address.com" # skip this if key exists
cat ~/.ssh/id_ed25519.pub       # prints content of key to terminal
ssh -T git@github.com           # test the connection
```
- If your connection is already set up: you're done. 
- Otherwise, we add the key to GitHub.
    - Copy output of terminal (using mouse to select the text)
    - Go to GitHub:
        - Click on profile icon -> `Settings` -> `SSH and GPG keys` -> `New SSH key`
        - Paste your SSH key into field -> `Add SSH key` 

```
ssh -T git@github.com           # test the connection
```
### Create remote repository - 15'

- Create a new repository called `recipes`
    - Public
    - Empty: no README, no .gitignore, no license
    - Copy SSH link

```
git remote add origin git@github.com:[username]/recipes.git # use SSH link
git remote -v                                               # -v for verbose
git push origin main            # explain push vs commit
```
- Show repository in GitHub

### 💪  Challenges `GitHub` - 10'
Challenges explained in collaborative document:
- `GitHub GUI`
    - Browse to your recipes repository on GitHub.
    - Under the Code tab, find and click on the text that says “XX commits” (where “XX” is some number).
    - Hover over, and click on, the three buttons to the right of each commit.
    - What information can you gather/explore from these buttons?
    - How would you get that same information in the shell? 

- `GitHub Timestamps` 
    - Go to the repo you just created on GitHub and check the timestamps of the files.  
    - How does GitHub record times, and why?  
    - Hover over the timestamp, you can see the exact time at which the last change to the file occurred. 

### 💪 Challenges `remotes` - 10'
- Continue with the same vevox
- Vevox question 7 and 8
- Start poll -> wait for answers -> discuss -> next question


## Break - 15'

## TU Delft FAIR software guidelines - 15'
- 🎦 use [slides](https://tud365.sharepoint.com/:p:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/Introduction%20to%20version%20control%20with%20Git.pptx?d=w582c916207804aac981699323fe83c38&csf=1&web=1&e=c4zb1b) 

## 💪 Challenge `Modify a README` - 15'
`Modify a README` challenge explained in collaborative document
- Download the README file from [GitHub](
https://github.com/tu-delft-library/introduction_to_version_control_with_git/blob/main/material_for_participants/README.md)
- Add it to your local recipes repository 
- Open file with nano 
- Complete the tasks included between [] in the README file 
- Add and commit changes to your local recipes repository 

## Live coding - 10'

Experience loosing your local repo and getting your code back from remote:

```
git status                      # ensure no uncommitted changes
git push origin main            # push changes
git pull origin main            # explain pull from remote
```
- Confirm all files are in remote (visit GitHub)
- Admire the new README file

```
ls
pwd
cd ..                           
rm -rf recipes/                 # loose repository
git status                      # no git repository here
git clone git@github.com:halfordd/recipes.git # clone repository
cd recipes
ls
ls -a                           # notice the difference: no .png files as they were not tracked
git status
```
Magic!

## 💪 Challenge `A new recipe` - 15'
`A new recipe` challenge explained in collaborative document.
- Add another recipe file to your local repository (e.g. `hummus.md`, `pesto.md`) 
- Edit to the new file with ingredients and instructions 
- Add and commit changes 
- Push changes to the remote repository 
- Confirm that you see the latest changes in GitHub 

## Break - 15'

## Version control with VSCode
- Some people prefer to use a GUI to work with Git.
- Let's explore that using VSCode

## Demo git operations in VSCode - 15'
- Open VSCode
- Open folder -> recipes folder
- Open `guacamole.md` from explorer
- Make a change (e.g. smash avocado) and save
- Go to git tab (left)

## 💪 Exercise `GitGraph` - 20'
Try [GitGraph extension](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph)

## Key points - 15'
* Use the cheat sheet to make sure you revise all the commands
* Use this file to make sure you revise all topics

## Feedback - 10'
* Ask participants to fill in the feedback survey