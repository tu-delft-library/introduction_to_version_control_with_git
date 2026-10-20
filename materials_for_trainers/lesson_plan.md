## 9:00 🚀 Prepare for take off - 20'
### Room setup
- Make sure to plug your computer to electricity. Otherwise the display will feed electricity to the laptop and potentially turn itself off.
- Test the microphone
- Write the edu.nl link pointing to `material_for_participants/links.md` document on the whiteboard 
    - Use dark marker on the board (not red)
- Place the list of the participants on a table at the entrance so that they can check their name (roll call)
- [Optional] bring jugs with water and snacks (if you brought any)

### Laptop setup

#### start autopush
Make sure to set up the bash history forwarding before workshop day as explained in `materials_for_trainers/pre_workshop_checklist.md`

Open another Terminal window. Let's call this the `hidden terminal` i.e. NOT to be shown during the workshop.

On the `hidden terminal` forward only the last line of the history to `command.log`
```bash
tail -n 0 -f ~/.bash_history | tee -a <local-repo-directory>/material_for_participants/command.log
```
Open another tab in the `hidden terminal`, `cd` to `<local-repo-directory>` and run autopush every 2-5 seconds
```bash
gitautopush --sleep 5 .
```
#### Open vevox
- Open vevox in different browser tab [TuDelft Vevox](https://tudelft.vevox.com/#/meetings)
- Open `Introduction to Version Control with Git`
- Present and keep it open for later

#### Open slides

Slides work better if you open them in your device: [slides](https://tud365.sharepoint.com/:p:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/Introduction%20to%20version%20control%20with%20Git.pptx?d=w582c916207804aac981699323fe83c38&csf=1&web=1&e=c4zb1b) 

## 9:30 - Participants land - 5'
☕ Reminder them about coffee at the entrance of library

## 9:35 - Housekeeping - 10'
Use [slides](https://tud365.sharepoint.com/:p:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/Introduction%20to%20version%20control%20with%20Git.pptx?d=w582c916207804aac981699323fe83c38&csf=1&web=1&e=c4zb1b) to welcome and introduce the session

Participants will run a small Python program during the day, so check it is installed:
```console
python --version                # on Mac and Linux it may be python3 --version
```
> On Mac and Linux, use `python3` wherever this plan says `python`.
> On Windows (Git Bash), if `python` is not found or opens the Microsoft Store, install Python from python.org (tick *Add Python to PATH*) and reopen Git Bash. 
TODO: add python to pre-workshop email.


## 9:45 - Icebreaker - photos timeline - 5'
- Instructions for the icebreaker on [slides](https://tud365.sharepoint.com/:p:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/Introduction%20to%20version%20control%20with%20Git.pptx?d=w582c916207804aac981699323fe83c38&csf=1&web=1&e=c4zb1b)
- This icebreaker is a good bridge to talk about git as time travel tool

> **REMEMBER TO START AUTOPUSH** instructions above 

## 9:50 - Introduction to version control - 10'
- 🎦 introduce git using [slides](https://tud365.sharepoint.com/:p:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/Introduction%20to%20version%20control%20with%20Git.pptx?d=w582c916207804aac981699323fe83c38&csf=1&web=1&e=c4zb1b) 
- What is version control and why should I use it?
  - Do it for your future self
  - your computer is dead. Your code lives on!
- How does git work -> `changesets` or `snapshots`
- What is a git repo: 
    - folder with files + subfolders + `.git` hidden folder

## 10:00 - Setting up git - 5'

- Open a bash terminal:
    - Windows: Open *Git Bash* from the Windows start menu
    - Mac:  
        - type `command + spacebar` search for `Terminal` and press `Return`
        - type `bash`
    - Linux: Open `Gnome Terminal` or `KDE Konsole` or `xterm`
     
- Navigate to `Desktop`:
```console
cd ~/Desktop
cd "/c/Users/[username]/OneDrive - Delft University of Technology/Desktop"
cd "/c/Users/[username]/OneDrive - Delft University of Technology/Bureaublad"
```
> ✅ 🆘 Everyone found their desktop?
```console
git version
git help
git config --list
git config --global user.name "Name Lastname"
git config --global user.email "netid@tudelft.nl"
git config --global core.editor "nano -w"
```
**CRLF** carriage return line feed. This concept originated from mechanical typewriters to separate the physical actions of moving to the left margin and advancing the paper. In our case it means `how Git handles line endings`

End of a line:
- Windows: Uses CRLF (\r\n) to mark the end of a line. 
- Unix/Linux/macOS: Uses LF (\n).

```console
# For mac and linux
git config --global core.autocrlf input              
# for windows do
git config --global core.autocrlf true  # For compatibility, line endings are converted to Unix style when you commit files.
git config --global init.defaultBranch main # in recent versions of git, main branch is default. But it's better to set this
```
**branches** Git can keep track of multiple lines of development like parallel timelines. These lines are called `branches`. We will work with branches in the next session. For now, it's only necessary to know that we only use one branch and it's called `main` 

```console
git config --list --global
git config --global --edit
```
And finally, let's check python
```console
python --version                # on Mac and Linux it may be python3 --version
```

## 10:05 - Initialize a local Git repository - 5'
We use a tiny Python project with a single file `fall.py`. It replaces the Carpentries `recipes` / `guacamole.md` example.
- `git init` initializes a repository
- Git stores all of its repository data in the `.git` directory

```console
cd Desktop
mkdir fall   # create a new directory for repository
cd fall/     # change to new directory to initialize git repo
ls              # show directory is empty
ls -a           # show directory has no hidden folders. remind about shortcuts . and ..
git init        # initialize git repo
ls              # appears as if nothing has changed
ls -a           # but hidden item .git was created
ls -aF          # .git is a special subfolder. DO NOT TOUCH THIS
ls .git         # some files and subfolders inside .git
```

## 10:10 - “add → commit” cycles - 10'
- Commands: `status, add, commit, log, diff`
- Important: 
    - We will work with a small Python program in this course (a free fall calculator)
    - Code is a text file that is *interpreted* by another program (python). For git it is just a text file, so everything works the same for any other code or text
    - In `nano` type **spaces, not tabs** (Python is picky about indentation). Type slowly to make the amount of spaces is consistent


```console
cd ~/Desktop/fall           # ensure inside fall dir
ls                          # dir is empty
git status                  # status of project: no commits yet!
cd ..                       # let's compare one level up
git status                  # not a git repository
cd fall                     # let's go back inside the fall folder
git status                  # yes! this is our repository
nano fall.py                # add the skeleton of the program
                            # explain: def defines a function, pass means 'do nothing yet'
```
```python
def fall_distance(seconds):
    pass

print(fall_distance(5))
```
```
python fall.py              # runs but prints nothing. Code is just text that python interprets
cat fall.py                 # see content of file 
git status                  # shows untracked file
git add fall.py             # please track this file
git status                  # new file but not committed
git commit -m "Create initial structure for free fall calculator" 
                            # -m flag + good commit messages: "this commit will..."
git status                  # up to date
git log                     # project history in reverse chronological order
                            # explain hash
nano fall.py                # implement the formula
```
We'll do a simple function that computes the distance of an object free falling on earth.
with the formula `distance = 0.5 * g * t^2`
In python, `**` is power. We also use a constant accessible anywhere in the code `GRAVITY` which on earth is 9.81 m/s^2
Finally, we add a line with `print` that shows the output of `fall_distance` computation.

```python
GRAVITY = 9.81
def fall_distance(seconds):
    return 0.5 * GRAVITY * seconds ** 2

print(fall_distance(5))
```
```console
python fall.py         # now it prints something: 122.625
cat fall.py            # see content of file 
git status                  # shows the file was modified
git diff                    # review changes. Explain the output
git commit -m "Implement fall distance formula" # no staged changes
git add fall.py        # we add the file, meaning is 'ready to commit'
git status                  # file is 'staged' -> ready to be committed
git commit -m "Implement fall distance formula"
git log
cat fall.py        # see contents of file
```

## 10:20 - Working directory and staging area - 10'
> **NOTE** there might be confusion about staging area and working tree. Let's use slides to clarify this
- 🎦 clarify staging area using [slides](https://tud365.sharepoint.com/:p:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/Introduction%20to%20version%20control%20with%20Git.pptx?d=w582c916207804aac981699323fe83c38&csf=1&web=1&e=c4zb1b) 
- Working directory -> staging area -> commit history (database)
- Useful ANALOGIES: 
    - Mailing a letter:
        - Staging is like putting letter in envelop
        - Committing is like putting it in the mailbox

- clarify `git diff --staged`
```console
git status
nano fall.py           # make the output readable: replace the print line
```
```python
GRAVITY = 9.81
def fall_distance(seconds):
    return 0.5 * GRAVITY * seconds ** 2

print("After 5 seconds the fall distance is", fall_distance(5), "meters")
```
```console
python fall.py         # the program now behaves differently, not just the text
git diff                    # replaced one line - with new line +
git add fall.py
git diff                    # no output   - diff only compares to working dir
git diff --staged           # changes in staging area
git status
git commit -m "Make output readable" # Commit message: think why
git status
git log
```

## 10:30 - 1 💪 `bio Repository`  - 10'

See `exercises.md`. There is an optional challenge under each numbered exercise.

#### Solution
```console
cd ..     # move out of fall folder
mkdir bio                           # Create a new folder called bio
cd bio                              # step into bio
git init                            # initialise git
nano me.txt                         # create file and add three lines
    My name is [NAME]
    I come from [COUNTRY]
    I love to [HOBBy]
git add me.txt                      # add file
git commit -m "Name, origin and hobby"  # commit changes
nano me.txt                         # modify one line, add a fourth line
    I have a [FIELD] background
git diff me.txt                     # show differences to working directory
git add me.txt                      # stage
git diff                            # no changes to working directory
git diff --staged                   # show difference to staged area
git commit -m "Add background"        # commit changes
git log                             # display git history
```
## 10:40 - Break - 15'


## 10:55 - git HEAD/TAG game - 5'
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
    - Some other people will get a post it with a TAG (e.g. for earth, moon) 
    - The teacher calls ‘git  restore [tag]’. 
        - HEAD marker is passed hand by hand until it reaches the corresponding tag. 


## 11:00 - Git history - 10'
- Commands: `HEAD, HEAD~1, HEAD~2, log --oneline, show, restore, tag`
- HEAD is the *most recent commit*

Let's step back into our `fall` repository
```console
cd ..
pwd                                 # should be in Desktop
cd fall                        # step into fall repository
git status
git log --oneline                   # summarized view
nano fall.py                   # introduce a typo in gravity constant (decimals swapped)
```
```python
GRAVITY = 9.18
def fall_distance(seconds):
    return 0.5 * GRAVITY * seconds ** 2

print("After 5 seconds the fall distance is", fall_distance(5), "meters")
```
```console
python fall.py                 # 114.75 m. Looks plausible! Would you have noticed from the output alone?
git diff HEAD fall.py          # diff of current file and most recent commit. The typo is obvious now
git diff fall.py               # HEAD is default option for git diff
git diff HEAD~1 fall.py        # diff between now and one commit before HEAD
git diff HEAD~2 fall.py        # diff between now and two commits before HEAD
git diff HEAD~3 fall.py        # fails. unknown revision
git log --oneline              # point to HEAD, HEAD~1, HEAD~2, HEAD~3 does not exist
git show HEAD~2 fall.py        # shows changes made on that commit (rather than differences)
git log --oneline                   # shows short hashes
git diff [short_hash] fall.py  # use short hash to point to a specific commit
git status                          # shows modified file
cat fall.py                    # see current version
git restore fall.py            # restores to latest commit
cat fall.py                    # typo is gone
python fall.py                 # correct values are back (4.905 m)
git log --oneline
git restore -s [short_hash] fall.py # -s for source
cat fall.py                    # restored file
python fall.py                 # we can even run the old version: crude output (1 4.905)
git status                     # restored file is not staged!
git restore fall.py            # overwrites working copy with last committed version
git status
cat fall.py
git tag -a formula [short_hash] -m "First working version" # add a tag -> easier than hash
                                    # use the hash of "Implement fall distance formula"
git log --oneline
git restore -s formula fall.py   # -s same as with the hash -> source
python fall.py                   # restored file is in the working directory.
git status                       # BUT restored file is not staged!
```
If we wanted to make this restored version our new latest version, we would need to make a new commit with the restored changes. But for now, we just inspect it, run it and then get go back to the latest commit.
```console
git restore fall.py              # restores to latest commit
git status                       # working tree clean
```



## 11:10 - 💪 Challenges `history` - 10'

TODO adapt these exercises to hands on (maybe using the same bio repository)
Vevox question 3
>The restore command restores files from the repository, overwriting the files in your working directory. Answers 2 and 4 both restore the latest version in the repository of the file data_cruncher.py. Answer 2 uses HEAD to indicate the latest, whereas answer 4 uses the unique ID of the last commit, which is what HEAD means.

> Answer 3 gets the version of data_cruncher.py from the commit before HEAD, which is NOT what we wanted.

> Answer 1 results in an error. You need to specify a file to restore. If you want to restore all files you should use git restore .

Vevox question 4
> The changes to the file from the second echo command are only applied to the working copy, not the version in the staging area. The command git add ketchup.md places the current version of ketchup.md into the staging area.

> So, when `git commit -m "My opinions about red sauce"` is executed, the version of ketchup.md committed to the repository is the one from the staging area and has only one line.

> At this time, the working copy still has the second line (and git status will show that the file is modified). However, git restore ketchup.md replaces the working copy with the most recently committed version of ketchup.md. So, cat ketchup.md will output:

> `I like ketchup.`

## 11:20 - Git ignore - 10'
Emphasize importance of `.ignore` file to keep repository clean.

```console
git status                          # always check the status of git
ls                                  # what is inside this directory
mkdir plots                         # make new directory
touch earth.png moon.png plots/mars.jpg plots/jupiter.jpg   # make dummy plots
ls                                  # lists generated plots
ls plots                            # lists generated plots inside folder
git status                          # images not recommended in git + distracting 
nano .gitignore                     # type lines below (remind . means hidden file)
        *.png
        plots/
cat .gitignore                      # confirm content of .gitignore
git status                          # no plots but yes new .gitignore file
git add .gitignore                  # let's track this file. it won't ignore itself
git commit -m "Ignore png files and the plots folder"
git status                          # all clean
ls                                  # files are in folder but not tracked by git
git add a.png                       # if accidentally added, shows warning
git status --ignored                # status of ignored files
touch plots/pluto.jpg               # new file in ignored folder
git status                          # nothing because plots folder is ignored
mkdir more_plots                    # empty folder
git status                          # nothing! git does not see empty folder
touch more_plots/pluto.jpg           # once there is a file, folder is tracked. This jpg is not inside plots folder
rm -rf more_plots                   # changed my mind. Clean up!
```

## 11:30 - 💪 Challenges `ignore` - 10'

TODO: turn this into a hands on. Inspiration: https://4turesearchdata-carpentries.github.io/GitCoDev/lesson1.html#ignore-untracked-directories

TODO: add hands on. inspiration: https://4turesearchdata-carpentries.github.io/GitCoDev/lesson1.html#marking-the-history-using-tags

Vevox question 5
> The exclamation point operator will include a previously excluded entry.

Vevox question 6
> Answer 1 will ignore only dat files named with one character.
> Answer 2 looks promising BUT it will ignore ALL the .dat files in the repository. 

>Answer 3 is the correct one. If you want to ignore only the .dat files inside a specific folder then you need to specify the full folder path: `pictures/data/location/gps/*.dat` will match every file in pictures/data/location/gps that ends with .dat. The file `pictures/data/location/gps/info.txt` will not be ignored.

> Answer 4 is an exception. Let's say if you ignore all files inside the folder `pictures/data/location/gps/` and then add the exception `!pictures/data/location/gps/info.txt`, it would achieve the goal for the current state of the repository. But it will not guarantee new files of other formats that are not `.dat` will be tracked.


## 11:40 - 💪 Vevox


Challenge `changes` - 10'

Vevox question 1 
> No. Alfredo does not need to make the plots subdirectory a Git repository because the fall repository will track all files, sub-directories, and subdirectory files under the fall directory. Thus, in order to track all information about plots, Alfredo only needed to add the plots subdirectory to the fall directory.

> Additionally, Git repositories can interfere with each other if they are “nested”: the outer repository will try to version-control the inner repository. Therefore, it’s best to create each new Git repository in a separate directory.

Vevox question 2
> git commit -m "my recent changes" would only create a commit if files have already been staged

> git init myfile.txt | git commit -m "my recent changes" would try to create a new repository

> git add myfile.txt | git commit -m "my recent changes" will add file.txt to the staging area and then commit the file. **This is our answer!**

> git commit -m myfile.txt "my recent changes" Would try to commit a file named “my recent changes” with the message myfile.txt


## 11:55 - Check your SSH key - 5'
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
If not, put your red sticky up and we'll help you.
If needed point to instructions in the [carpentries website](https://swcarpentry.github.io/git-novice/07-github.html#create-an-ssh-key-pair)

## 12:00 - Lunch break - 60'

## 13:00 - Create remote repository - 10'
- 🎦 continue mailing letter analogy to introduce remote repositories with [slides](https://tud365.sharepoint.com/:p:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/Introduction%20to%20version%20control%20with%20Git.pptx?d=w582c916207804aac981699323fe83c38&csf=1&web=1&e=c4zb1b) 
- Explain push vs commit: 
    - When we push changes, we’re interacting with a remote repository to update it with the changes we’ve made locally (often this corresponds to sharing the changes we’ve made with others). 
    - Commit only updates your local repository.

> **Let's go to GitHub**

Create a new repository called `fall`
- Public
- Empty: no README, no .gitignore, no license
- Copy SSH link

```console
git remote add origin git@github.com:[username]/fall.git # use SSH link
git remote -v                                               # -v for verbose
git push origin main            # explain push vs commit
```
Git automatically names that source `origin`. So `origin` = "the remote I cloned this from," which is usually your own copy. `origin` is just a name. It is the convention everyone uses, so it is good to stick to it.

Check that the local changes are visible in GitHub.

Let's make another change locally:

```console
nano fall.py            # change gravity to 1.62 -> moon's gravity
```
```python
GRAVITY = 1.62

def fall_distance(seconds):
    return 0.5 * GRAVITY * seconds ** 2

print("After 5 seconds the fall distance is", fall_distance(5),"m")
```
```console
python fall.py             # Moon gravity
git status
git add fall.py
git commit -m "Use Moon gravity"
git log --oneline               # the local HEAD is one commit ahead of origin/main HEAD
git push origin main            # uploads the new commit. Refresh GitHub to see it
```


## 13:10 - 💪  2 GitHub GUI + 3 GitHub Timestamps - 10'
See `exercises.md`. There is an optional challenge under each numbered exercise.

#### `GitHub GUI` solution:

When you click on the left-most button, you’ll see all of the changes that were made in that particular commit. Green shaded lines indicate additions and red ones removals. In the shell we can do the same thing with git diff. In particular, git diff ID1..ID2 where ID1 and ID2 are commit identifiers (e.g. git diff a3bf1e5..041e637) will show the differences between those two commits.

The middle button (with the picture of two overlapping squares or pages) copies the full identifier of the commit to the clipboard. In the shell, git log will show you the full commit identifier for each commit.

The right-most button lets you view all of the files in the repository at the time of that commit. To do this in the shell, we’d need to checkout the repository at that particular time. We can do this with git checkout ID where ID is the identifier of the commit we want to look at. If we do this, we need to remember to put the repository back to the right state afterwards!

#### `GitHub Timestamps` solution:

GitHub displays timestamps in a human readable relative format (i.e. “22 hours ago” or “three weeks ago”). However, if you hover over the timestamp, you can see the exact time at which the last change to the file occurred.

## 13:20 - Pulling a fresh copy of repo - 10'

Experience loosing your local repo and getting your code back from remote:

```console
git status                      # ensure no uncommitted changes
git push origin main            # push changes
git pull origin main            # explain pull from remote
ls -a                           # local files (including the ignored files)
cd ..                           
rm -rf fall/               # lose repository
ls                              # fall directory is gone
git status                      # make sure you are not inside a git repository
git clone git@github.com:[username]/fall.git # NEW COMMAND! clone repository (copy SSH link from github)
cd fall
ls
ls -a                           # notice the difference: no .png files as they were not tracked
python fall.py > output.txt  # the program still runs. We can regenerate anything that was not tracked
git log --oneline               # files and history preserved. Beautiful!
                                # noticed that the tags are missing! If you want to preserve your tags you need to explicitly push them
git tag -a formula [HASH] -m "First working version"
git push --tags
```
Check the tag in GitHub (drop down menu that shows also branches)


## 13:30 - TU Delft FAIR software guidelines - 10'
- 🎦 use [slides](https://tud365.sharepoint.com/:p:/r/sites/ResearchDataServices/Gedeelde%20documenten/Training/Research_Software_Training/lesson_plans/resources/Introduction%20to%20version%20control%20with%20Git.pptx?d=w582c916207804aac981699323fe83c38&csf=1&web=1&e=c4zb1b) 
> Remember to talk about the most common licenses: MIT, Creative Commons, Apache


## 13:40 LAB: Getting started with Collaboration - 30'
see `PRACTICAL_collaboration_exercise.md` file 


## 14:10 - 💪 VEVOX remote Challenges `remotes` - 5'


Vevox question 7
> When we push changes, we’re interacting with a remote repository to update it with the changes we’ve made locally (often this corresponds to sharing the changes we’ve made with others). Commit only updates your local repository.

Vevox question 8
1. Update local
1. Append 100
1. Stage changes
1. Commit changes
1. Update remote
1. Celebrate

## 14:15 - Key points - 10'
- point to the cheat sheet linked in the `links` document
- revise the commands by asking to the class what the commands are 
```console
git config          # configure
git init            # initialize locally
git clone           # download from github
git status          # always check the status
git log             # history of commits
git log --oneline    # a shorter version
git add             # add changes
git commit          # commit locally
git diff            # differences between to commits
git show            # shows changes made on that commit (rather than differences)
git push            # uploads local changes to remote
git pull            # downloads changes from remote to local
```

## 14:25 - Home assignment - 5'
At home, go through the exercise in `PRACTICAL_putting_it_all_together.md` file. It should take less than 1 hour to finish it.

