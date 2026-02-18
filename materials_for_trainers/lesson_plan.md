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

### Code along
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

### Code along - 10'
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

### Challenges `init` - 5'
- TODO
- Go to [TuDelft Vevox](https://tudelft.vevox.com/#/meetings)
- Start poll -> wait for answers -> discuss -> next question

## Perform multiple “add → commit” cycles
- Commands: `status, add, commit, log, diff`
- Important: 
    - We will work with a text file in this course. It will work the same with code. 
    - Code is a text file that is *interpreted* by another program (e.g. python)

### Code along - 20'
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
### Challenges `changes` - 5'
- TODO
- Go to [TuDelft Vevox](https://tudelft.vevox.com/#/meetings)
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

### Code along - 10'
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
### Challenges `staging` - 10'
- TODO
- Go to [TuDelft Vevox](https://tudelft.vevox.com/#/meetings)
- Start poll -> wait for answers -> discuss -> next question

## git HEAD/TAG game - 15'
- Game explained in [resources document](https://tud365.sharepoint.com/:w:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/resources.docx?d=waea671d7fc6a46d5b5c068fc19f41940&csf=1&web=1&e=f2QYgy)

## Git history
- Commands: `HEAD, HEAD~1, HEAD~2, log --oneline, show, restore`
- HEAD is the *most recent commit*

### Code along - 15'
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

### Challenges `history` - 10'
- TODO
- Go to [TuDelft Vevox](https://tudelft.vevox.com/#/meetings)
- Start poll -> wait for answers -> discuss -> next question


## Git ignore
Emphasize importance of `.ignore` file to keep repository clean.

### Type along - 10'
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
### Challenges `ignore` - 10'
- TODO
- Go to [TuDelft Vevox](https://tudelft.vevox.com/#/meetings)
- Start poll -> wait for answers -> discuss -> next question

## Lunch break - 60'

## GitHub - 20'

### Demo steps in GitHub - 20'
For full instructions with images go to [SWC](https://swcarpentry.github.io/git-novice/instructor/07-github.html)
- Log into GitHub
- Create a new repository called `recipes`
    - Public
    - Empty: no README, no .gitignore, no license
- Create Secure Shell Protocol (SSH) key
    - SSH key in GitHub is paired to key in your computer
- Connect local to remote repository
    - Use SSH link

```
ls -al ~/.ssh                   # possible keys id_ed25519/id_ed25519.pub
ssh-keygen -t ed25519 -C "youremail@address" # skip this is key already exists
cat ~/.ssh/id_ed25519.pub 
ssh -T git@github.com
```


```
git remote add origin git@github.com:[username]/recipes.git
git remote -v
```




### GitHub GUI - 10'
- Explore GitHub GUI

## Remote repository

### Type along - 20'
```
git push origin main            # explain push vs commit
git pull                        # explain pull from remote
ls
pwd
cd ..                           
rm -rf recipes/                 # practice loosing repository
git status
git clone git@github.com:halfordd/recipes.git # practice cloning repository
cd recipes
ls
ls -a
git status
```

### Challenges `` - 10'
- TODO
- Go to [TuDelft Vevox](https://tudelft.vevox.com/#/meetings)
- Start poll -> wait for answers -> discuss -> next question

## Break - 15'

## TU Delft FAIR software guidelines - 15'
- TODO add slides for FAIR
- 🎦 use [slides](https://tud365.sharepoint.com/:p:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/Introduction%20to%20version%20control%20with%20Git.pptx?d=w582c916207804aac981699323fe83c38&csf=1&web=1&e=c4zb1b) 

## Modify a README - 30'
- TODO make empty repo from manuel's template-> simplified version -> https://github.com/manuGil/fair-code
- Copy content from template (zip file with README.md, CONTRIBUTING.md, folders)
- Adapt the README template (a little bit at least)

## Fresh copy of remote - 15'
Experience loosing your local repo and getting your code back from remote:
- Push changes
- Confirm all files are in remote
- Delete your local repo
- Clone repository from github

## Break - 15'

## Version control with VSCode
- Some people prefer to use a GUI to work with Git.
- Let's explore that using VSCode

## Demo git operations in VSCode - 15'
- TODO demo script

### Exercise - 20'
Try [GitGraph extension](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph)

## Key points - 15'
* Use the cheat sheet to make sure you revise all the commands
* Use this file to make sure you revise all topics

## Feedback - 5'
* Ask participants to fill in the feedback survey