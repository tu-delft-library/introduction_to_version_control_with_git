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

## 9:30 - Land - 5'
☕ Coffee/tea 🫖

## 9:35 - Housekeeping - 10'
- ✅ Roll call + 🤝 Code of Conduct
- 🖥 Did everyone:
    - install git
    - install VSCode
    - create a GitHub account
- 🙋 Getting help (🆘 red  ✅ green stickers)

## 9:45 - Icebreaker - photos timeline - 5'
- Instructions for the icebreaker on slides
- This icebreaker is a good bridge to talk about timeline

> **REMEMBER TO START AUTOPUSH**

## 9:50 - Introduction to version control - 10'
- 🎦 introduce git using [slides](https://tud365.sharepoint.com/:p:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/Introduction%20to%20version%20control%20with%20Git.pptx?d=w582c916207804aac981699323fe83c38&csf=1&web=1&e=c4zb1b) 
- What is version control and why should I use it?
  - Do it for your future self
  - your computer is dead. Your code lives on!
- How does git work -> `changesets` or `snapshots`
- What is a git repo: 
    - folder with files + subfolders + `.git` hidden folder

## 10:00 - Preparing Your Working Directory - 5'
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

## 10:05 - Setting up git - 5'

```console
git version
git help
git config --list
git config --global user.name "Name Lastname"
git config --global user.email "netid@tudelft.nl"
git config --global core.editor "nano -w"
```
>*CRLF* carriage return line feed. This concept originated from mechanical typewriters to separate the physical actions of moving to the left margin and advancing the paper. In our case it means `how Git handles line endings`

End of a line:
- Windows: Uses CRLF (\r\n) to mark the end of a line. 
- Unix/Linux/macOS: Uses LF (\n).

```console
# For mac and linux
git config --global core.autocrlf input              
# for windows do
git config --global core.autocrlf true  # For compatibility, line endings are converted to Unix style when you commit files.
git config --global init.defaultBranch main
```
Git uses branches
- A branch is a separate timeline
- You will learn about branches later (in the intermediate course??)
- We work on the main branch for now. We will discuss branches in the next module.

```console
git config --list --global
git config --global --edit
```

## 10:10 - Initialize a local Git repository - 10'
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

## 10:20 - “add → commit” cycles - 15'
- Commands: `status, add, commit, log, diff`
- Important: 
    - We will work with a text file in this course. It will work the same with code. 
    - Code is a text file that is *interpreted* by another program (e.g. python)


```console
cd ~/Desktop/recipes        # ensure inside recipes dir
ls                          # dir is empty
git status                  # status of project: no commits yet!
cd ..                       # let's compare one level up
git status                  # not a git repository
cd recipes                  # let's go back inside the recipes folder
git status                  # yes! this is our repository
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
git add guacamole.md        # explain stating area: allows to review before taking a snapshot (commit)
git status                  # file is 'staged' -> ready to be commited
git commit -m "Add ingredients to guacamole recipe"
git log
cat guacamole.md        # see contents of file
```
> **NOTE** there might be confusion about stating area and working tree. We will clarify in the next section.

## 10:35 - 💪 Challenge `changes` - 10'
- Go to [TuDelft Vevox](https://tudelft.vevox.com/#/meetings)
- Vevox question 1 and 2

## 10:45 - Break - 15'

## 11:00 - Working directory and staging area - 10'
- 🎦 clarify staging area using [slides](https://tud365.sharepoint.com/:p:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/Introduction%20to%20version%20control%20with%20Git.pptx?d=w582c916207804aac981699323fe83c38&csf=1&web=1&e=c4zb1b) 
- Working directory -> staging area -> commit history (database)
- Useful ANALOGIES: 
    - Mailing a letter:
        - Staging is like putting letter in envelop
        - Committing is like putting it in the mailbox
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
git diff                    # no output   - diff only compares to working dir   
git diff --staged           # changes in staging area
git status
git commit -m "Modify guacamole to traditional recipe" # Commit message: think why
git status
git log
```



## 11:10 - 1 💪 `bio Repository`  - 10'

See `exercises.md`. There is an optional challenge under each numbered exercise.

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
git diff me.txt                     # show differences to working directory
git add me.txt                      # stage
git diff                            # no changes to working directory
git diff --staged                   # show difference to staged area
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


## 11:30 - Git history - 15'
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
git tag -a traditional [short_hash] -m "Tag for traditional recipe"   # add a tag -> easier than hash
git log --oneline
git restore -s traditional guacamole.md    # -s same as with the hash -> source
git status                          # restored file is not staged!
```

## 11:45 - Break - 15'


## 12:00 - 💪 Challenges `history` - 10'
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
nano .gitignore                     # type lines below (remind . means hidden file)
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
touch pictures/new.jpg              # new file in ignored folder
git status                          # nothing because pictures folder is ignored
mkdir anotherfolder                 # empty folder
git status                          # nothing! git does not see empty folder
touch anotherfolder/file.jpg        # once there is a file, folder is tracked. This jpg is not inside pictures folder
rm -rf anotherfolder                # changed my mind. Clean up!
```


## 12:20 - 💪 Challenges `ignore` - 10'
- Go to [TuDelft Vevox](https://tudelft.vevox.com/#/meetings)
- Vevox question 5 and 6

## 12:30 - Check your SSH key - 5'
- Why SSH key?
    - go though the option of writing password everytime
    - we can bypass this by adding a key
    - tells github that is safe to communicate with your machine

```console
ssh -T git@github.com           # test the connection
```
You should see a message like
```
Hi [yourname]! You've successfully authenticated, but GitHub does not provide shell access.
```
If not, put your red sticky up and we'll help you

## 12:35 - Lunch break - 55'

# 13:30 - Create remote repository - 10'
- 🎦 continue mailing letter analogy to introduce remote repositories with [slides](https://tud365.sharepoint.com/:p:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/Introduction%20to%20version%20control%20with%20Git.pptx?d=w582c916207804aac981699323fe83c38&csf=1&web=1&e=c4zb1b) 
- Explain push vs commit: 
    - When we push changes, we’re interacting with a remote repository to update it with the changes we’ve made locally (often this corresponds to sharing the changes we’ve made with others). 
    - Commit only updates your local repository.
> ** Let's go to GitHub **

Create a new repository called `recipes`
- Public
- Empty: no README, no .gitignore, no license
- Copy SSH link

```console
git remote add origin git@github.com:[username]/recipes.git # use SSH link
git remote -v                                               # -v for verbose
git push origin main            # explain push vs commit
```
Check that the local changes are visible in GitHub

```console
nano guacamole.md 
    # Guacamole
    ## Ingredients
    * avocado
    * lime
    * salt
    * red chilly pepper
    ## Instructions
git status
git add guacamole.md 
git commit -m "Added extra ingredients"
git log --oneline
git push                      # does not work! branch needs an 'upstream'
git push --set-upstream origin main
git push
git status
git pull origin main
git push origin main
git status
```


## 13:40 - 💪  2 GitHub GUI + 3 GitHub Timestamps - 10'
See `exercises.md`. There is an optional challenge under each numbered exercise.

#### `GitHub GUI` solution:

When you click on the left-most button, you’ll see all of the changes that were made in that particular commit. Green shaded lines indicate additions and red ones removals. In the shell we can do the same thing with git diff. In particular, git diff ID1..ID2 where ID1 and ID2 are commit identifiers (e.g. git diff a3bf1e5..041e637) will show the differences between those two commits.

The middle button (with the picture of two overlapping squares or pages) copies the full identifier of the commit to the clipboard. In the shell, git log will show you the full commit identifier for each commit.

The right-most button lets you view all of the files in the repository at the time of that commit. To do this in the shell, we’d need to checkout the repository at that particular time. We can do this with git checkout ID where ID is the identifier of the commit we want to look at. If we do this, we need to remember to put the repository back to the right state afterwards!

#### `GitHub Timestamps` solution:

GitHub displays timestamps in a human readable relative format (i.e. “22 hours ago” or “three weeks ago”). However, if you hover over the timestamp, you can see the exact time at which the last change to the file occurred.

## 13:50 - Pulling a fresh copy of repo - 10'

Experience loosing your local repo and getting your code back from remote:

```console
git status                      # ensure no uncommitted changes
git push origin main            # push changes
git pull origin main            # explain pull from remote
```
- Confirm all files are in remote (visit GitHub)

```console
ls -a                           # local files (including the ignored files)
pwd
cd ..                           
rm -rf recipes/                 # loose repository
git status                      # make sure you are not inside a git repository
git clone git@github.com:[username]/recipes.git # NEW COMMAND! clone repository (copy SSH link from github)
cd recipes
ls
ls -a                           # notice the difference: no .png files as they were not tracked
git status
```
Magic!

## 14:00 - 💪 Challenges `remotes` - 10'
- Go to [TuDelft Vevox](https://tudelft.vevox.com/#/meetings)
- Vevox question 7 and 8


## 14:10 - Break - 15'

## 14:25 - TU Delft FAIR software guidelines - 10'
- 🎦 use [slides](https://tud365.sharepoint.com/:p:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/Introduction%20to%20version%20control%20with%20Git.pptx?d=w582c916207804aac981699323fe83c38&csf=1&web=1&e=c4zb1b) 
>* Remember to talk about the most common licenses: MIT, Creative Commons, Apache


## 14:35 LAB: Putting it all together - 60'
see `PRACTICAL.md` file 

## 15:35 - Key points - 10'
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

## 15:45 - Feedback - 5'
Ask participants to fill in the feedback survey

