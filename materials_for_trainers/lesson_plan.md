## Tips for the day
- Make sure to plug your computer to electricity. Otherwise the display will feed electricity to the laptop and potentially turn itself off.
- Write the edu.nl link pointing to `links` document on the whiteboard 
    - Use dark marker on the board (not red)
- If you are using a mac, make the terminal not transparent: 
    - Open the terminal
    - Open settings
    - Go to background color
    - Adjust opacity to 100%
- Set your desktop to a color background instead of an image that can be distracting (e.g. a beach or a mountain)
- Ask Paula to print a list of the participants so that they can check their name (roll call)
- Start auto push [TODO] @halfordd step-by-step explanation

## 9:30 - Land - 10'
☕ Coffee/tea 🫖

## 9:40 - Housekeeping - 10'
- ✅ Roll call + 🤝 Code of Conduct
- 🖥 Did everyone:
    - install git
    - install VSCode
    - create a GitHub account
- 🙋 Getting help (🆘 red  ✅ green stickers)

## 9:50 - Icebreaker - 5'
- Instructions for the icebreaker on slides
- When finished ask the group to share some of the answers they got


## 9:55 - Introduction to version control - 10'
- 🎦 introduce git using [slides](https://tud365.sharepoint.com/:p:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/Introduction%20to%20version%20control%20with%20Git.pptx?d=w582c916207804aac981699323fe83c38&csf=1&web=1&e=c4zb1b) 
- What is version control and why should I use it?
  - Do it for your future self
  - your computer is dead. Your code lives on!
- How does git work -> `changesets` or `snapshots`
- What is a git repo: 
    - folder with files + subfolders + `.git` hidden folder

## 10:05 - Preparing Your Working Directory - 5'
- Open a bash terminal:
    - Windows: Open *Git Bash* from the Windows start menu
    - Mac:  
        - type `command + spacebar` search for `Terminal` and press `Return`
        - type `bash`
    - Linux: Open `Gnome Terminal` or `KDE Konsole` or `xterm`
     
- Navigate to `Desktop`:
```console
cd ~/Desktop
cd "/c/Users/[username]/OneDrive - Delft University of Technology\Desktop"
cd "/c/Users/[username]/OneDrive - Delft University of Technology\Bureaublad"
```

## 10:10 - Setting up git - 5'

Important to mention:
- End of a line:
    - Windows: Uses CRLF (\r\n) to mark the end of a line. 
    - Unix/Linux/macOS: Uses LF (\n).
- Git uses branches
    - A branch is a separate timeline
    - You will learn about branches later (in the intermediate course??)
    - We work on the main branch and no more details for now.

```console
git version
git help
git config --list
git config --global user.name "Name Lastname"
git config --global user.email "netid@tudelft.nl"
git config --global core.editor "nano -w"
## For mac and linux
git config --global core.autocrlf input             # auto carriage return line feed 
## for windows do
git config --global TODOTODODODOD                   # TODO
git config --global init.defaultBranch main
git config --list --global
git config --global --edit
```

## 10:15 - Initialize a local Git repository - 10'
- `git init` initializes a repository
- Git stores all of its repository data in the `.git` directory

```console
cd Desktop
mkdir recipes   # create a new directory for repository
cd recipes/     # change to new directory to initialize git repo
ls              # show directory is empty
ls -a           # show directory has no hidden folders. remind about shortcuts . and ..
git init        # initialize git repo
ls              # appears as if nothing has changed
ls -a           # but hidden item .git was created
ls -aF          # .git is a special subfolder. DO NOT TOUCH THIS
ls .git         # some files and subfolders inside .git
```

## 10:25 - “add → commit” cycles - 15'
- Commands: `status, add, commit, log, diff`
- Important: 
    - We will work with a text file in this course. It will work the same with code. 
    - Code is a text file that is *interpreted* by another program (e.g. python)


```console
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

### 10:40 - 💪 Challenge `changes` - 10'
- Go to [TuDelft Vevox](https://tudelft.vevox.com/#/meetings)
- Vevox question 1 and 2


## 10:50 - Break - 10'


## 11:00 - Working directory and staging area - 10'
- 🎦 introduce staging area using [slides](https://tud365.sharepoint.com/:p:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/Introduction%20to%20version%20control%20with%20Git.pptx?d=w582c916207804aac981699323fe83c38&csf=1&web=1&e=c4zb1b) 
- Working directory -> staging area -> commit history (database)
- Useful ANALOGIES: 
    - Mailing a letter:
        - Staging is like putting letter in envelop
        - Committing is like putting it in the mailbox

    - Photo group analogy:
        - `git add` specifies what will go in a snapshot 
        - `git commit` then actually takes the snapshot
        - `git commit -a` is like gathering everyone to take a group photo

```console
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


### 11:10 - 💪 Challenge `staging` - 10'
`bio Repository` challenge explained in `links` document
> * Remember to show the exercise on the screen while giving the instructions

#### Solution
```console
cd ..     # move out of recipes folder
mkdir bio                           # Create a new folder called bio
cd bio                              # step into bio
git init                            # initialise git
nano me.txt                         # create file and add three lines
git add me.txt                      # add file
git commit -m "Add biography file"  # commit changes
nano me.txt                         # modify one line, add a fourth line
git diff me.txt                     # show differences
```


## 11:20 - git HEAD/TAG game - 10'
    HEAD 
    - We use a physical object to represent the HEAD (a ball, a stuff animal, a fruit)
    - Teacher will call HEAD~1, HEAD~5
    - Marker of HEAD starts in one edge of the row
    - The teacher calls ‘git restore HEAD~[X]’. 
        - The HEAD marker is passed hand by hand until it reaches the corresponding HEAD position. 

    TAGS 
    - Marker of HEAD starts in one edge of the row
    - Some people get a paper with a short hash (e.g. f22b25e, b36abfd) 
    - The teacher calls ‘git  restore [hash]’. 
        - HEAD marker is passed hand by hand until it reaches the corresponding hash. 
    - Teacher comments on how hard it is for humans to remember this hash. Enter TAGs 
    - Some other people will get a post it with a TAG (e.g. for guacamole – original, spicy, no onion) 
    - The teacher calls ‘git  restore [tag]’. 
        - HEAD marker is passed hand by hand until it reaches the corresponding tag. 


## 11:30 - Git history - 20'
- Commands: `HEAD, HEAD~1, HEAD~2, log --oneline, show, restore, tag`
- HEAD is the *most recent commit*

```console
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
git restore guacamole.md            # restores to latest commit
git log --oneline
git restore -s [short_hash] guacamole.md # -s for source
cat guacamole.md                    # restored file
git status                          # restored file is not staged!
git restore guacamole.md            # overwrites working copy with last committed version
git status
cat guacamole.md   
git tag -a nana [short_hash] -m "Nana's recipe"   # add a tag -> easier than hash
git log --oneline
git restore -s nana guacamole.md    # -s same as with the hash -> source
git status                          # restored file is not staged!
```

## 11:50 - Break - 10'


### 12:00 - 💪 Challenges `history` - 10'
- Go to [TuDelft Vevox](https://tudelft.vevox.com/#/meetings)
- Vevox question 3 and 4


## 12:10 - Git ignore - 10'
Emphasize importance of `.ignore` file to keep repository clean.

```console
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
git add .gitignore                  # let's track this file. it won't ignore itself
git commit -m "Ignore png files and the pictures folder"
git status                          # all clean
ls                                  # files are in folder but not tracked by git
git add a.png                       # if accidentally added, shows warning
git status --ignored                # status of ignored files
mkdir anotherfolder                 # empty folder
git status                          # nothing! git does not see empty folder
```


### 12:20 - 💪 Challenges `ignore` - 10'
- Go to [TuDelft Vevox](https://tudelft.vevox.com/#/meetings)
- Vevox question 5 and 6

## 12:30 - Lunch break - 60'

## 13:30 - SSH key - 20'
- Why SSH key?
    - go though the option of writing password everytime
    - we can bypass this by adding a key
    - tells github that is safe to communicate with your machine
- Log into GitHub
- Create Secure Shell Protocol (SSH) key
    - SSH key in GitHub is paired to key in your computer
```console
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

```console
ssh -T git@github.com           # test the connection
```
# 13:50 - Create remote repository - 10'

Create a new repository called `recipes`
- Public
- Empty: no README, no .gitignore, no license
- Copy SSH link

```console
git remote add origin git@github.com:[username]/recipes.git # use SSH link
git remote -v                                               # -v for verbose
git push origin main            # explain push vs commit
```
- Explain push vs commit: 
    - When we push changes, we’re interacting with a remote repository to update it with the changes we’ve made locally (often this corresponds to sharing the changes we’ve made with others). 
    - Commit only updates your local repository.
- Show repository in GitHub

### 14:00 - 💪  Challenges `GitHub` - 10'
> * Remember to show the exercise on the screen while giving the instructions
Challenges explained in `links` document:

#### `GitHub GUI` solution:

When you click on the left-most button, you’ll see all of the changes that were made in that particular commit. Green shaded lines indicate additions and red ones removals. In the shell we can do the same thing with git diff. In particular, git diff ID1..ID2 where ID1 and ID2 are commit identifiers (e.g. git diff a3bf1e5..041e637) will show the differences between those two commits.

The middle button (with the picture of two overlapping squares or pages) copies the full identifier of the commit to the clipboard. In the shell, git log will show you the full commit identifier for each commit.

The right-most button lets you view all of the files in the repository at the time of that commit. To do this in the shell, we’d need to checkout the repository at that particular time. We can do this with git checkout ID where ID is the identifier of the commit we want to look at. If we do this, we need to remember to put the repository back to the right state afterwards!

#### `GitHub Timestamps` solution:

GitHub displays timestamps in a human readable relative format (i.e. “22 hours ago” or “three weeks ago”). However, if you hover over the timestamp, you can see the exact time at which the last change to the file occurred.

### 14:10 - 💪 Challenges `remotes` - 10'
- Go to [TuDelft Vevox](https://tudelft.vevox.com/#/meetings)
- Vevox question 7 and 8


## 14:20 - Break - 15'

## 14:35 - TU Delft FAIR software guidelines - 10'
- 🎦 use [slides](https://tud365.sharepoint.com/:p:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/Introduction%20to%20version%20control%20with%20Git.pptx?d=w582c916207804aac981699323fe83c38&csf=1&web=1&e=c4zb1b) 
>* Remember to talk about the most common licenses: MIT, Creative Commons, Apache

## 14:45 - 💪 Challenge `Modify a README` - 15'
`Modify a README` challenge explained in `links` document
- Download the README file from [GitHub](
https://github.com/tu-delft-library/introduction_to_version_control_with_git/blob/main/material_for_participants/README.md)
- Add it to your local recipes repository 
- Open file with nano 
- Complete the tasks included between [] in the README file 
- Add and commit changes to your local recipes repository 


## 15:00 - Pulling a fresh copy of repo - 10'

Experience loosing your local repo and getting your code back from remote:

```console
git status                      # ensure no uncommitted changes
git push origin main            # push changes
git pull origin main            # explain pull from remote
```
- Confirm all files are in remote (visit GitHub)
- Admire the new README file

```console
ls
pwd
cd ..                           
rm -rf recipes/                 # loose repository
git status                      # no git repository here
git clone git@github.com:[username]/recipes.git # NEW COMMAND! clone repository (copy SSH link from github)
cd recipes
ls
ls -a                           # notice the difference: no .png files as they were not tracked
git status
```
Magic!

## 15:10 - Break - 10'

## 15:20 - 💪 Challenge `A new recipe` - 25'
> * Remember to show the exercise on the screen while giving the instructions

`A new recipe` challenge explained in `links` document.
#### solution
```console
nano hummus.md              # add headers ingredients, instructions
git add hummus.md
git commit -m "Add hummus recipe"
git status
nano hummus.md              # add chickpeas, lemon, tahini, garlic
git add hummus.md
git commit -m "Add ingredients to hummus"
nano hummus.md              # add all to food processor
git add hummus.md
git commit -m "Add instructions to hummus"
git log --oneline
git push origin main
```

## 15:45 - Key points - 10'
- point to the cheat sheet linked in the `links` document
- revise the commands by asking to the class what the commands are 
```console
git config          # configure
git init            # initialize locally
git clone           # download from github
git status          # always check the status
git log             # history of commits
git log --online    # a shorter version
git add             # add changes
git commit          # commit locally
git diff            # differences between to commits
git show            # shows changes made on that commit (rather than differences)
git push            # uploads local changes to remote
git pull            # downloads changes from remote to local
```

## 16:55 - Feedback - 5'
Ask participants to fill in the feedback survey



#### pilot
general note -> make desktop single background so that its less distracting than a photo of the beach where we are not right now
remember to clear terminal more often
