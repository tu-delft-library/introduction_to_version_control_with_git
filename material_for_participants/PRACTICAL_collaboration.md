# PRACTICAL: Getting started with Collaboration

> Adapted from *Version Control with Git — Episode 8: Collaborating*, Software Carpentry / The Carpentries, licensed [CC-BY 4.0](https://swcarpentry.github.io/git-novice/LICENSE.html). 

## PART 0: Setting up

### Pick your roles

Get into pairs. Decide who will be:

- **Partner A — the Owner.** This person's GitHub repository (e.g. the `free_fall` repo from earlier exercises) will be the shared project.
- **Partner One — the Collaborator.** This person will clone the Owner's repository and contribute changes to it.

### Granting access (Partner A)

- On GitHub, navigate to your repository's page.
- Click **Settings → Collaborators → Add people**.
- Enter your partner's (Partner One's) GitHub username and send the invite.

**Partner One** should now check [https://github.com/notifications](https://github.com/notifications) or their email, and accept the invitation.

### Cloning the shared repository (Partner One)

- **Partner One** downloads a copy of **Partner A**'s repository.
- Since **Partner One** already has a local repo named `free_fall`, clone into a **different folder** so the two don't collide

```
$ cd ~/Desktop
$ git clone git@github.com:<owner-username>/free_fall.git free_fall-<owner-username>
```

- Replace `<owner-username>` with **Partner A**'s GitHub username.

> **NOTE** if you omit the destination path at the end of `git clone`, Git will clone into a folder matching the repo's name in your current directory — which may overwrite or collide with your own repo of the same name.

## PART 1: A new script

In this part you will build a tiny Python script together. It calculates how long an object takes to hit the ground when dropped from a given height.

The physics is the one you already know from free fall:

```
h = ½ · g · t²    →    t = √(2h / g)
```

> ⚠️ **Watch out:** Follow the instructions carefully to avoid conflicts. We will learn how to solve conflicts on the next session.

### Making and sharing a change (Partner One)

Move into the cloned repository

```
$ cd ~/Desktop/fall-<owner-username>
```
Create a new script named `time.py`

```
$ nano time.py
```
Add a comment describing the script, the gravitational acceleration and the height.

```python
# Time for an object to free fall from a given height

gravity = 9.81
height = 10
```
Save changes and exit nano.

Stage and commit the change

```
$ git add time.py
$ git commit -m "Add constants for free fall time"
```
Confirm there are no uncommitted changes in your working directory

```
$ git status
...
nothing to commit, working tree clean
```
Push the change back to the **Owner's** repository:

```
$ git push origin main
```

Note that you didn't need to create a remote called `origin` yourself — Git names it that automatically when you clone.

### Retrieving the change (Partner A)

Back on **Partner A**'s machine, pull down the new commit:

```
$ git pull origin main
```

Check the repository's commit history with `git log --oneline`. You should now see **Partner One**'s commit.

At this point, three copies of the project are back in sync: the Owner's local repo, the Collaborator's local repo, and the copy on GitHub.

### Checkpoint discussion (both partners)

Before moving on, talk through this together:

> **The basic collaborative workflow** is: `git pull` → make changes → `git add` → `git commit` → `git push`. Why does it matter that you pull *before* you start editing, rather than only before you push?

### Making and sharing another change (Partner A)

Edit `time.py`

```
$ nano time.py
```
Add the calculation at the **end of the file**, after the line that defines `height`

```python
import math

time = math.sqrt(2 * height / gravity)
print("An object dropped from", height, "meters reaches the ground after", time, "seconds")

```
Save changes and exit nano.

Run the script. You should see that the fall takes ~`1.4287928234324 seconds`

```
$ python time.py
```
Stage and commit the change

```
$ git add time.py
$ git commit -m "Add free fall time calculation"
```
Confirm there are no uncommitted changes in your working directory

```
$ git status
...
nothing to commit, working tree clean
```
Push the change back to your remote repository

```
$ git push origin main
```

### Retrieving the change (Partner One)

Back on **Partner One**'s machine, pull down the new commit:

```
$ git pull origin main
```

Check the repository's commit history with `git log --oneline`. You should now see **Partner A**'s commit.

Run the script on your machine too, and check that you get the same result as your partner.



### Making and sharing another change (Partner One)

Edit `time.py`

```
$ nano time.py
```
To make the output more readable, round the value stored in the variable `time` to have only 2 decimals.
Add a new line above `print` to compute a new variable `time_round`. Update the variable name inside the `print` statement

```python
time_round = round(time, 2)
print("An object dropped from", height, "meters reaches the ground after", time_round, "seconds")

```
Save changes and exit nano.

Run the script. You should see the rounded value in the printed output: `1.43 seconds`

```
$ python time.py
```
Stage and commit the change

```
$ git add time.py
$ git commit -m "More readable rounded time value"
```
Confirm there are no uncommitted changes in your working directory

```
$ git status
...
nothing to commit, working tree clean
```
Push the change back to your remote repository

```
$ git push origin main
```

### Retrieving the change (Partner A)

Back on **Partner A**'s machine, pull down the new commit:

```
$ git pull origin main
```

Check the repository's commit history with `git log --oneline`. You should now see **Partner One**'s commit.

Run the script on your machine too, and check that you get the same result as your partner.


* * *

## PART 2: Making the repository more FAIR

### Auditing the repository

Working with your partner, spend a few minutes auditing the `free_fall` repository against the checklist below

| Principle         | Ask yourselves...                                                                      | Look for / add                                                                                                                                                            |
|-------------------|----------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Findable**      | Could a stranger discover this repository and understand what it is at a glance?       | A descriptive repository name and description; a README with a clear title and one-sentence summary at the top                                                            |
| **Accessible**    | Can someone actually get the files and understand how to obtain them?                  | The repo is public (or access is documented); clear clone/install instructions in the README                                                                              |
| **Interoperable** | Does it play well with standard tools and formats, and is it clear what it depends on? | Listed dependencies/requirements (e.g. Python version, modules used); standard file formats and layout (e.g., `.py` for code, `.md` for docs)                              |
| **Reusable**      | Could someone else legally and practically reuse this?                                 | A `LICENSE` file; a `CITATION.cff` (or citation section in the README) so people know how to credit the work; enough documentation to run it without asking you questions |

As you have noticed there are a few **quick wins** you can do to make this repository more FAIR.

### Add a README

Make these changes as **Partner One** contribution, following the same workflow you just practiced:

- Pull from remote
- Create a `README.md` using `nano`
- Copy paste the template below. Inside `nano`, check the suggestions between brackets [] and make changes accordingly.

  ```
  # Free fall

  ## Description
  I often found myself rewriting the same free fall calculation over and over again. Sometimes I got the formula right. Sometimes I forgot a factor of 2.

  So I decided to start a collection of small scripts for my future-self.

  These scripts have been tested under the following circumstances:
  * Earth gravity (g = 9.81 m/s^2)
  * Drop height of 10 meters
  * Drop time of 5 seconds

  [Add one more circumstance you tested, e.g. the moon gravity]

  ## Requirements
  - Python  [Add the minimal version of python]
  - Python modules
     - math


  ## How to run
  Clone this repository locally and run the script from a terminal with `python time.py` or `python distance.py`.


  ## Citation
  Use the citation in the `CITATION.cff` file to acknowledge this work.

  ## Acknowledgements
  - Galileo, for dropping things from towers
  - [Your partner's name]

  ```
- When you are done, remove the text between []
- Save changes and exit nano
- Stage and commit the `README.md`
- Push to remote
- **Partner A** confirm the changes appear on GitHub
- **Partner A** run `git pull` locally
- **Partner A** run `git log --oneline` and confirm you see the `README.md` file locally

### Add a **LICENSE** file

Make these changes as **Partner A** contribution

- Create a `LICENSE` file using nano
- Pick an MIT license from [https://choosealicense.com](https://choosealicense.com) and paste it in.
- Inside `nano` replace the copyright line with one of these three options. Fill the information between `[]` accordingly.

  1. If software is patented or commercialized: `Copyright (c) [YEAR] Technische Universiteit Delft`
  2. If software is not patented nor commercialized, TU Delft will waive the copyright to authors as long as it is published under open-source license: `Copyright (c) [YEAR] [AUTHOR(S)], Delft, the Netherlands`
  3. If software is kept as in-house development, share with collaborators under proprietary license or agreement only: `Copyright (c) [YEAR] Technische Universiteit Delft, [NON-EMPLOYEES], Delft, the Netherlands`
- Save changes and exit nano
- Stage and commit the `LICENSE` file
- Push to remote
- **Partner One** confirm the changes appear on GitHub
- **Partner One** run `git pull` locally
- **Partner One** run `git log --oneline` and confirm you see the `LICENSE` file locally

### 🚀 Optional

#### Add a **CITATION.cff** file

Decide who is going to perform this task:

- Generate a CITATION.cff file using this [website](https://citation-file-format.github.io/cff-initializer-javascript/#/)
- Download the generated file and move it to the repository
- Stage and commit the `CITATION.cff`
- Push to remote
- **Other partner** confirm the changes appear on GitHub
- **Other partner** run `git pull` locally
- **Other partner** run `git log --oneline` and confirm you see the `CITATION.cff` file locally
